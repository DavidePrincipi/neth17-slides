---
title: Moving to the next NethServer UI
css: 'css/custom.css,css/font-awesome.min.css'
scripts: 'scripts/custom.js'
revealOptions:
    transition: 'none'
---

<i class="fa fa-plane" aria-hidden="true"></i>

# Moving to the next NethServer UI

[@davideprincipi](https://twitter.com/davideprincipi) - #neth17

Note:

  Again past, present, future of NethServer 

  I will focus on the UI development, and we will se why it's so important



---

## What we've done

~ 50 modules <!-- .element: class="fragment" -->

~ 120 RPMs <!-- .element: class="fragment" -->

6 years <!-- .element: class="fragment" -->

Note:

  "Give you some numbers...

  Counted modules from yum groups output

  Counted RPMs from GitHub repositories

---

### Anatomy of NethServer

|   |    | |
| - | ------ | ------------------------ |
| 3 | Web UI | Server Manager ⇨ <b>Nethgui</b> |
| 2 | Configuration manager | DB, events, templates, actions ⇨ <b>e-smith</b> |
| 1 | Upstream distro | <span class="fragment strike" data-fragment-index="2">CentOS 6</span> <b class="fragment fade-in" data-fragment-index="2">CentOS 7</b> |

ns6 ⇨ ns7 (2016) major distro update <!-- .element: class="fragment" data-fragment-index="2" -->

Note:

  Implementation replacement

---

<!-- .slide: data-transition-speed="slow" data-transition="slide-out" -->

### https&#58;//nethserver:980

* Nethgui framework (PHP)  <!-- .element: class="fragment" -->

* Apache web server  (mod_php) <!-- .element: class="fragment" -->

* e-smith API (signal-event, config setprop...)  <!-- .element: class="fragment" -->

* sudo privilege escalation (srvmgr ⇨ root)  <!-- .element: class="fragment" -->

Note:

  "Let's dig layer 3 a little bit deeper...

  home-made framework, requires PHP only programming, strict rules ->
  consistent UI behavior

  traditional synchronous web stack, client always request first, then
  server responds

---

## Why moving away

Backup config <!-- .element: class="fragment" -->

Accounts provider <!-- .element: class="fragment" -->

-----

* learning curve is too steep for developers <!-- .element: class="fragment" -->

* people don't read the docs, they love guided procedures (wizards) <!-- .element: class="fragment" -->
  <span class="fragment">but they are <u>too difficult to develop</u></span>

Note:

  "We look at two case studies / lessons we learned

  BC: non-standard UI (file upload still not implemented at that time) - difficult for the devs

  AP: non-trivial concept, requires difficult configuration decisions - difficult for the sysadmin

---

<i>Making sysadmin's life easier with Open Source</i> <!-- .element: class="fragment fade-out" data-fragment-index="1" -->

making developer's life easier <!-- .element: class="fragment" data-fragment-index="1" -->

-----
### goal <!-- .element: class="fragment" data-fragment-index="2" -->

using standard tools <!-- .element: class="fragment" data-fragment-index="2" -->

Note: rewording the NethServer mission statement...

---

<!-- .slide: data-transition-speed="slow" data-transition="slide-out" -->

### targets

* decrease development times <!-- .element: class="fragment" -->

* increase number of developers <!-- .element: class="fragment" -->

Note:

  "At Nethesis we settled to seek the alternative

---

## What we're doing

July '17 &ndash; knocking on another door<br>https&#58;//nethserver:9090 <!-- .element: class="fragment" -->

Note:

  "Who's there?"

---

### Cockpit

* Free Software project sponsored by Red Hat <!-- .element: class="fragment" -->
* available from upstream repositories <!-- .element: class="fragment" -->
* available on other distributions too <!-- .element: class="fragment" -->

Note:

  following project since 2015, listened to Stef Walter's talk at CentOS dojo 2017

  ``yum install cockpit``

  other distros == standard

---

### Cockpit - the "web shell"

* embedded web server <!-- .element: class="fragment" -->
* spawns user-privileged process (the "bridge") <!-- .element: class="fragment" -->
* fast web socket message transport <!-- .element: class="fragment" -->
* Patternfly UI framework (HTML + CSS) <!-- .element: class="fragment" -->
* JavaScript framework agnostic <!-- .element: class="fragment" -->


Note:

  PolicyKit and sudo privilege escalation

  Cockpit runs its own web server that talks to the "bridge"

  Patternfly == (RHEL) standard components

  AngularJS / prominent, well-known JS framework from Google


---

<!-- .slide: data-transition-speed="slow" data-transition="slide-out" -->

### <i class="fa fa-hand-paper-o" aria-hidden="true"></i> Hurdles on my way

* learn new JavaScript tools <!-- .element: class="fragment" -->
* learn asynchronous programming <!-- .element: class="fragment" -->

Note:

   "BUT learning curve is smooth here: there is plenty of documentation resources available

---

## Why Cockpit

* Aiming to standardization <!-- .element: class="fragment" -->

* Teaming <!-- .element: class="fragment" -->

* Bonus: multi-server interface <!-- .element: class="fragment" -->

Note: 

  Settle a bastion host and access multiple servers from it through the Cockpit UI

---

> Cockpit has a beautiful architecture, tightly integrated with the underlying
system and allows managing multiple servers from the same interface.

> It is light fast and I love the way it handles user privileges. <!-- .element: class="fragment" -->
<br>[davidep](http://community.nethserver.org/t/what-do-you-think-about-cockpit/973/5)
Jun&nbsp;'15

Note:

  "I strongly believe Cockpit meets our needs, so...

---

<!-- .slide:  data-transition-speed="slow" data-background-size="contain" data-background="./img/cockpit1.png" -->

Note:



---

<i class="fa fa-github-square" aria-hidden="true"></i> [nethserver/nethserver-cockpit](https://github.com/NethServer/nethserver-cockpit)

``# yum --enablerepo=nethserver-testing install nethserver-cockpit`` <!-- .element: class="fragment" -->

---

## What we'll do

* write the docs

* share code and ideas

* gather feedback

Note:

  "Today is not 2011, we now have a community that helps on getting the right track

---

### Ideas for ns7

https&#58;//nethserver:<u>980</u>/<span class="fragment strike" data-fragment-index="2">cockpit/</span>

1. embed Cockpit modules in Server Manager<br>reverse HTTP proxy: ``cockpit/`` ⇨ port 9090
2. develop new NS modules on Cockpit <!-- .element: class="fragment fade-in" data-fragment-index="1" -->
3. switch to Cockpit on feature parity <!-- .element: class="fragment fade-in" data-fragment-index="2" -->
   <span class="fragment fade-in" data-fragment-index="3">(?)</span>

---

### Ideas for ns8

|   |    |  |
| - | ------ | ------------------------
| 3 | Web UI | Server Manager <span class="fragment fade-in" data-fragment-index="2">⇨ Cockpit</span>
| 2 | Configuration manager | DB, events, templates, actions <span class="fragment fade-in" data-fragment-index="3">⇨ Ansible</span>
| 1 | Upstream distro | CentOS 8 <span class="fragment fade-in" data-fragment-index="1">(?)</span>

Note:

  "ns8 fully compliant with upstream on all of three layers

  CentOS 8 - Release date unknown (~18 months ?)

  We proved Cockpit can be the foundation of Server Manager UI

  Plans for pushing Ansible on Fedora Server: it could be our configuration management layer too...



---

<i class="fa fa-plane" aria-hidden="true"></i>

[@davideprincipi](https://twitter.com/davideprincipi) - #neth17
