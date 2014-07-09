---
layout: post
title: "Adventures in Drupal Services endpoints"
date: 2012-02-14 10:06
comments: true
categories: drupal
---


Adventures with Drupal Services

If you are writing a web services interface on top of Drupal 7, you might be tempted to do something like use menu callbacks. The menu system in Drupal really is just a bunch of code that is called and spits back HTML for you. It's common to write your own menu code that takes and spits back whatever you want. Now that I think of it, this is probably how the Drupal Services module is written way down. There is certainly no immediately obvious reason not to do it that way.

These are some notes I found while getting a simple services module written. They, like my current knowledge, are incomplete. In many areas I have yet to fathom why they are like this. My concern is limited to the use of the REST Server in the Services 3 code.

# More than CRUD.

All this section comes from reading the code in services/servers/rest_server/includes/RESTServer.inc., particularly the method __resolveController()__. This method is the source of the most common error when writing your own services -- __Cannot find controller__. It is worth your time to read the code and get a sense of how it works.

Services has CRUD hardwired into it. It assumes the following CRUD methods:

-  retrieve
-  create
-  update
-  delete

Now this is clearly not enough to make a pretty, full featured REST API. So Services 3 allows you to add in two other types of API endpoints.

## Actions.

According to the README for the REST server for services, actions

<quote>
are performed directly on the resource type, not an individual resource.
</quote>

An example is given of telling a search engine to reindex itself. This does not act on any particular piece of content, but rather works across all the content at one time.

For my purposes I wanted to use more descriptive names on my endpoints than, say, 'create' so I only used actions. But I could have easily given an alias to the create endpoint in the code. In retrospect I should have gone that way but we'll look at code using actions for everything in this post.

## Targeted Actions.

These are like actions, something that does not fit in the default CRUD API layout. The difference is that these work on an particular piece of content. For example, an endpoint might tell Drupal to append some content to an entity.

POST http://example.com/api/entity/123/append/run%20concluded

This hypothetical call would append the string "run concluded" to some field on the entity with etid 123.

I did not use targeted actions, so they won't be in the code in this post, but the idea is prett simple.

## Relations.

Relations are a little different in that they retrieve content related to the content in question. For example, you might want an API to get a list of all files associated with a particular entity. You might want it to read like this

GET http://example.com/api/entity/243/filelist

Pretty simple when you understand it. These terms are all used in the documentation, but how to create anything other than the basic CRUD endpoints in your custom code is not explained. We'll be showing you how to create custom actions (discerned from studying how the code works) here. Presumably relations are not all that different, but I will not swear to it. 

## Why all the different types?

I can only assume that there is some REST specification of which I am unaware. It seems fine to me to make them all 'actions', which is much like saying 'menu callbacks'. The code for the REST server would be simplified, as would writing hooks for it. But Greg Dunlap has been doing Services for quite some time, and I have faith that he led a total rewrite of the framework for a reason. So for now I am concerning myself with what is, rather than why it is that way.

(brief pause as plane is landing and I need to shut off the laptop.)

# Some code -- finally!

At the end of the day, the best thing turns out to study the __resolveController()__ method in __RESTServer.inc__, as explained above. Then look at the implementations of __hook_services_resources()__ in the directory __services/resources__. They will show you how to declare actions.

With all this background, we can finally do the actual simple part: write the code.

## Hooks away!

Some days I love Drupal's hook system. It makes coding so pleasurable. Other times I wonder about bootstrap costs. But that's another story.

First, let's declare a simple api with actions only and no CRUD. Here are some custom entry points for the 'drupalchat' endpoint. Also notice that the 'messagecreate' endpoint takes a 'struct' type of parameter, which is populated by Services with payload data for a POST call. For the sake of simplicity we'll not comment on the standard access callback.

<code>
/**
 * Implements hook_services_resources().
 */
function chat_rest_services_resources() {
  $resources['drupalchat'] = array();
  $resources['drupalchat']['actions'] = array(
    'messagecreate' => array(
      'help' => 'Send a new chat message.',
      'callback' => '_chat_rest_send_msg',
      'access callback' => 'chat_rest_access',
      'access arguments' => array('create'),
      'access arguments append' => TRUE,
      'args' => array(
        array(
          'name' => 'data',
          'type' => 'struct',
          'description' => 'Recipient user id and message to send.',
          'source' => 'data',
          'optional' => FALSE,
        ),
      ),
    ),
    'newmessages' => array(
      'help' => 'Get any new chat messages.',
      'callback' => '_chat_rest_retrieve',
      'access callback' => 'chat_rest_access',
      'access arguments' => array('new'),
      'access arguments append' => TRUE,
    ),
    'updatebuddylist' => array(
      'help' => 'Get currently buddy list status.',
      'callback' => '_chat_rest_buddylist',
      'access callback' => 'chat_rest_access',
      'access arguments' => array('new'),
      'access arguments append' => TRUE,
    ),
  );
  
  return $resources;
}
</code>

Lastly, define the endpoints to be shown in the Services configuration page.

<code>
function chat_rest_default_services_endpoint() {
  $endpoint = new stdClass;
  $endpoint->disabled = FALSE; // endpoint disabled initially
  $endpoint->name = 'drupalchat';
  $endpoint->title = 'Drupalchat REST API';
  $endpoint->server = 'rest_server';
  $endpoint->path = 'js-api';
  $endpoint->authentication = array(
    'drupalchat' => array(
      'alias' => '',
      'actions' => array(
        'messagecreate' => array(
          'enabled' => 1,
        ),
        'newmessages' => array(
          'enabled' => 1,
        ),
        'updatebuddylist' => array(
          'enabled' => 1,
        ),
      ),
    ),
  );

  // TODO turn this debug to 0
  $endpoint->debug = 1; 
  $endpoints[] = $endpoint;
  return $endpoints;
}
</code>

That's it! Declaring a custom Services endpoint (or here, 3)  really is not that difficult once you understand how to do it.
