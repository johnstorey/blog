---
layout: post
title: "Drupal Access Grants"
date: 2014-07-09 15:25:19 -0700
comments: true
categories: drupal
---
It's been quite a while since this blog has been posted too -- or existed! Apparently the VPS hosting it was killed in a cleanup at some point in the past. I've lost some posts. Oops!

But we are back, and today is a topic on one of my favorite topics -- coding Drupal. In this case, Drupal 7.

# Access and Access Grants

The last time I tried to customize the permission rules in Drupal was in Drupal 6, and grants were not an option. Instead there was the node access system, and various modules you could use to customize them. IIRC, I ended up using taxonomy access lite, which allowed me to customize access based on the tag on the content type. If any code denied access to a piece of content, even if 10 other modules said 'allow', the access was not granted. On top of that, the node access system seemed fairly fragile.

The experience sucked.

As part of a Drupal application in the health care industry I had to put some interesting rules around CRUD access to a content type, Prescription. Specifically the interesting requirements were

> Create a content type 'Prescription'.
> Give it a reference to an associated Nurse writing the Prescription.
> Give it a reference to an associated Doctor, who can alter and approve the prescription. 
> Make the Prescription private to the client organization on the web application.
> Within that organization, only let the Doctor and Nurse referenced by a Prescription view it.

It was the last one that got me thinking. I started research, and found that Drupal 7 has hook_node_access_records() and hook_node_grants(). A little time with a debugger and watching changes to the node_access table opened up a clean, simple implementation of the requirements.

# How Access Grants Work

Here is how things work. All access to a node in Drupal must pass permission checks according to the settings in the node_access table. So while you are developing, keeping an eye on this table is a wise idea.

When you do nothing, a row is created in that table that allows anyone to view that content type. But we aren't going to "do nothing" -- we are going to make our own rules.

When you implement hook_node_access_records(), it will be called every time a node is saved. You have the opportunity to change what is going into the node_access table at this point. While you can read the details at [hook_node_access_records](https://api.drupal.org/api/drupal/modules%21node%21node.api.php/function/hook_node_access_records/7), here is a simple one that modifies the access grant for a Prescription content type.

	function mymodule_node_access_records($node) {
	  $grants = array() ;

	  if ($node->type == 'prescription') {
	    $grants[] = array(
	      'realm' = 'all',
	      'gid' => 0,
	      'grant_view' => 0,
	      'grant_update' => 1,
	      'grant_delete' => 0,
	      'priority' => 1,
	    );
	   }
	 return $grants;
	}

The interesting points here are the 'realm' and 'gid' parameters. Together, with the $node->id field, comprise the key of the node access table. Combined, the realm and gid are a unique grant for the node. There values are abritrary, but the gid must be an integer.

So the above says if someone has the realm 'all' and gid '0', don't let them see the node in question, let them update it, and don't let them delete it.

Once grants are checked, if they pass, then the base node access system -- the one you usually modify on the permissions tab -- are checked. If *both* pass then the node is presented to the user.

Now you get pretty flexible here. In my situation I made some custom permissions, named the realms after them, and made two entries in the $grants array. In them I used, in turn, the user id of the Doctor and Nurse referenced by the Prescription. Now I had two rows in the node access table for the Prescription. One for the Doctor and one for the Nurse.

But how about the check when viewing the node? 

## hook_node_grants

This is the other side of the equation. When the user attempts to access the node for any CRUD operation, hook_node_grants is called in your module. Read the documentation here: [hook_node_grants](://api.drupal.org/api/drupal/modules%21node%21node.api.php/function/hook_node_grants/7).

Basically you are returning an array whose key is the realm from hook_node_access_records, and whose value is the gid. If a record in the node_access table matches the node id, the realm, and the gid, the access permissions for the operation in that row are used.

Let's say a user has the 'custom view prescription' permission. You might write the hook like this

	function mymodule_node_grants($account, $op) {
	  $grants = array();

	  if (user_acces('custom view prescription', $account)) {
	    $grants['custom view prescription'] = array($account->uid);
	  }

	  return $grants;
	}

This code specifies to Drupal that, subject to the current permissions settings, the current user has the grant 'custom view prescription'-uid. What that means was defined by a call to hook_node_access_records when the node was created.

# So What?

When you take the time to think about it, I just very simply outlined a very small amount of code that implements a highly customized permissions system that, out of the box, Drupal does not support. Once I understood the interplay of the systems, this took about 2 hours to write and to write tests.

Grants, unlike custom access modules, even works with Views. This is a very flexible system that puts the ability to create all sorts of custom access patterns for your Drupal applications, meaning the complexity of the solutions you are able to provide just greatly increased.

Oh, and what about the standard access patterns? Well, after checking grants, Drupal still checks the regular access patterns. So if by some horrible mistake a doctor in one hospital is somehow associated with the prescription of another hospital, a smple separation of content into private organic groups denies the inappropriate access. 

This was the result of a delightful Saturday afternoon with the Drupal documentation, a book on Safari Books Online, and a debugger. Some days just go nice.

Now back to running the engineering department. Annual reviews are due in a week ...
