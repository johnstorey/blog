---
layout: post
title: "Emacs Dired Nodes"
date: 2012-12-06 07:09
comments: true
categories: emacs
---

# Dired mode in Emacs.

As part of my current attempt to revive old / acquire new Emacs skills, these are notes to myself on some of the neat things you can do with dired mode. This effort is motivated by the fact I now develop locally on OS-X, remotely on an Ubuntu VM, and plan to dual-boot the new Macbook Pro. Also, occasionally, I pair program with one of my guys on their VM or machine.

So I've cleaning up my github account with my dotfiles so that I can more easily move my environment between machines and use the same tools, such as Emacs.

Emacs has too much beauty to grok fully while remembering to find time to breathe, so this is a subset of notes gathered from several sources.

<table border="1" class="nrm" style="border:solid 1px #000000;border-collapse:collapse;margin:.5ex; width: 100%">
  <caption>Dired Commands</caption>
  <tr>
    <td align="center" valign="top" style="border:solid thin #808080; padding: .5ex; width: 20%;">
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;M-x&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;find-dired-mode&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;M-x&nbsp;hl-line-mode&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;highlights&nbsp;current&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;line&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<enter>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      go&nbsp;into&nbsp;a&nbsp;directory&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;^&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;leave&nbsp;a&nbsp;directory&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C-s&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      change&nbsp;arguments&nbsp;to&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ls&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;inserts&nbsp;directory&nbsp;
      &nbsp;under&nbsp;cursor&nbsp;into&nbsp;&nbsp;current&nbsp;buffer.
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;buffer&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;k&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;deletes&nbsp;directory&nbsp;&nbsp;<br />
      from&nbsp;current&nbsp;buffer&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;T&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;touch&nbsp;current&nbsp;file&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;R&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;rename&nbsp;file&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;S&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;symlink&nbsp;file&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Z&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;compress&nbsp;or&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;uncompress&nbsp;file&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;D&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;mark&nbsp;for&nbsp;deletion&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;X&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;expunge&nbsp;file&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;m&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mark&nbsp;file&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;u&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;unmark&nbsp;file&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;U&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;unmark&nbsp;all&nbsp;files&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C-t&nbsp;C-t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      Incrementally&nbsp;search<br />
      &nbsp;through&nbsp;all&nbsp;files&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;%&nbsp;g&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      mark&nbsp;files&nbsp;based&nbsp;on&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a&nbsp;regexp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      mark&nbsp;all&nbsp;directories
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;copy&nbsp;marked&nbsp;(or&nbsp;&nbsp;&nbsp;<br />
      &nbsp;current)&nbsp;items&nbsp;to&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kill&nbsp;ring&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
  <tr>
    <td align="center" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C-x&nbsp;C-q&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </td>
    <td align="left" valign="top"  style="border:solid thin #808080; padding: .5ex" >
      &nbsp;&nbsp;wdired.&nbsp;All&nbsp;file&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names&nbsp;are&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
      &nbsp;&nbsp;editable.&nbsp;Commit&nbsp;&nbsp;<br />
      &nbsp;&nbsp;&nbsp;with&nbsp;'C-c&nbsp;C-c'&nbsp;&nbsp;&nbsp;
    </td>
  </tr>
</table>

## Primary sources:
- [http://emacsmovies.org/blog/2012/12/04/dired/](http://emacsmovies.org/blog/2012/12/04/dired/)
- [http://ergoemacs.org/emacs/file_management.html](http://ergoemacs.org/emacs/file_management.html)
