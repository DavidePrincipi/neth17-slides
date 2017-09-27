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

---

## What we've done

~ 50 modules / 120 RPMs <!-- .element: class="fragment" data-fragment-index="1" -->

6 years <!-- .element: class="fragment" data-fragment-index="2" -->

---

### Anatomy of NethServer

|   |    | |
| - | ------ | ------------------------ |
| 3 | Web UI | Server Manager ⇨ <b>Nethgui</b> |
| 2 | Configuration manager | DB, events, templates, actions ⇨ <b>e-smith</b> |
| 1 | Upstream distro | <span class="fragment strike" data-fragment-index="2">CentOS 6</span> <b class="fragment fade-in" data-fragment-index="2">CentOS 7</b> |

ns6 ⇨ ns7 (2016) major distro update <!-- .element: class="fragment" data-fragment-index="2" -->

---

<!-- .slide: data-transition-speed="slow" data-transition="slide-out" -->

### https&#58;//nethserver:980

* Nethgui framework (PHP)  <!-- .element: class="fragment" -->

* Apache web server  (mod_php) <!-- .element: class="fragment" -->

* e-smith API (signal-event, config setprop...)  <!-- .element: class="fragment" -->

* sudo privilege escalation (srvmgr ⇨ root)  <!-- .element: class="fragment" -->

---

## Why moving away

Accounts provider <!-- .element: class="fragment" -->

Backup config <!-- .element: class="fragment" -->

-----

* people don't read the docs/forum <!-- .element: class="fragment" -->

* people love guided procedures (wizards) <!-- .element: class="fragment" --> <span class="fragment">but they are <u>too difficult to develop</u></span>

---

<i>Making sysadmin’s life easier with Open Source</i> <!-- .element: class="fragment fade-out" data-fragment-index="1" -->

making developer’s life easier <!-- .element: class="fragment" data-fragment-index="1" -->

-----
### goal <!-- .element: class="fragment" data-fragment-index="2" -->

using standard tools <!-- .element: class="fragment" data-fragment-index="2" -->

Note: rewording the NethServer mission...

---

<!-- .slide: data-transition-speed="slow" data-transition="slide-out" -->

### targets

* decrease development times <!-- .element: class="fragment" -->

* increase number of developers <!-- .element: class="fragment" -->

---

## What we're doing

July '17 &ndash; knocking on another door<br>https&#58;//nethserver:9090 <!-- .element: class="fragment" -->

---

### Cockpit

* Free Software project sponsored by Red Hat <!-- .element: class="fragment" -->
* available from upstream repositories <!-- .element: class="fragment" -->
* available on other distributions too <!-- .element: class="fragment" -->

Note: 
  
  following project since 2015, met developer Stef Walter at FOSDEM'17
  
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

---

## Why Cockpit

* Aiming to standardization <!-- .element: class="fragment" -->

* Teaming <!-- .element: class="fragment" -->

* Bonus: multi-server interface <!-- .element: class="fragment" -->

Note:

  I strongly believe Cockpit meet our needs
  

---

> Cockpit has a beautiful architecture, tightly integrated with the underlying
system and allows managing multiple servers from the same interface.

> It is light fast and I love the way it handles user privileges. <!-- .element: class="fragment" -->
<br>[davidep](http://community.nethserver.org/t/what-do-you-think-about-cockpit/973/5)
Jun&nbsp;'15


---

<!-- .slide:  data-transition-speed="slow" data-background-size="contain" data-background="./img/cockpit1.png" -->

---

<i class="fa fa-github-square" aria-hidden="true"></i> [nethserver/nethserver-cockpit](https://github.com/NethServer/nethserver-cockpit)

``# yum --enablerepo=nethserver-testing install nethserver-cockpit`` <!-- .element: class="fragment" -->

---

## What we'll do

* write the docs

* share code and ideas

* gather feedback

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

---

<i class="fa fa-plane" aria-hidden="true"></i>

[@davideprincipi](https://twitter.com/davideprincipi) - #neth17