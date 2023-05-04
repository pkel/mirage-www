---
updated: 2013-10-15
author:
  name: Amir Chaudhry
  uri: http://amirchaudhry.com
  email: amirmc@gmail.com
subject: Overview of MirageOS
permalink: overview-of-mirage
---

This page provides background information. If you're new to MirageOS and
want to jump straight in, we recommend the tutorials starting from the
[installation instructions](https://mirage.io/docs/install)!

### What is MirageOS and why is it important?

<a href="http://www.berndnaut.nl/images/NimbusNP3web.jpg"><img style="float:right; margin-left: 15px; margin-bottom: 15px;" src="/graphics/nimbus-np3-smilde.jpg"></img></a>

Most applications that run in the cloud aren't optimised to do so.
They inherently carry assumptions about the underlying operating
system with them, including vulnerabilities and bloat.
Compartmentalisation of large servers into smaller [virtual
machines](http://en.wikipedia.org/wiki/Virtual_machine) has enabled
many new businesses to get started and achieve scale. This has been
great for new services but many of those virtual machines are
single-purpose and yet they contain largely complete operating systems
which themselves run applications like web-servers. This means a large
part of the footprint is unused and unnecessary, which is both costly
and a security risk (due to the larger attack surface).

MirageOS represents a new approach where only the necessary components
of the OS are included and compiled along with the application into a
[unikernel](http://queue.acm.org/detail.cfm?id=2566628). This
results in highly efficient and extremely lean
[appliances](http://en.wikipedia.org/wiki/Virtual_appliance), with a
much smaller attack surface.  These appliances can be deployed
directly to the cloud and embedded devices, with the benefits of
reduced costs and increased security and scalability.

### How does MirageOS work?

<a href="http://www.xenproject.org/developers/teams/hypervisor.html"><img style="float:left; margin-right: 15px;" src="/graphics/Xen-Panda-Ecosystem-1.png"></img></a>

MirageOS is a 'library operating system' for constructing secure,
high-performance network applications across a variety of cloud
computing and mobile platforms. It works by treating the [Xen
hypervisor](http://www.xenproject.org/developers/teams/hypervisor.html)
as a stable hardware platform, allowing us to focus on
high-performance protocol implementations without worrying about
having to support the thousands of device drivers found in a
traditional OS.

Code can be developed in a high-level functional programming language
(OCaml) on a desktop OS such as Linux or Mac OSX, and is then compiled
into a fully-standalone, specialised unikernel. These unikernels run
directly on Xen hypervisor APIs. Since the Xen powers most public
clouds such as [Amazon EC2](http://aws.amazon.com/ec2), [Rackspace
Cloud](http://www.rackspace.com/cloud/), and many others, MirageOS lets
your servers run more cheaply, securely and faster in any Xen based
cloud or hosting service.

MirageOS is based around the [OCaml language](http://ocaml.org), with
syntax extensions and [50+ libraries](https://github.com/mirage) which
map directly to operating system constructs when being compiled for
production deployment. As such, MirageOS includes clean-slate functional
implementations of protocols ranging from TCP/IP, DNS, SSH, Openflow
(switch/controller), HTTP, XMPP and Xen inter-VM transports.


### Where will MirageOS be useful?

<a href="http://www.flickr.com/photos/radnezeoz/7343684238/"><img style="float:right; margin-left: 15px;" src="/graphics/cumulous-cruisin.jpg"></img></a>

An example of a current MirageOS appliance is this website which is a
completely self-hosted site, deployed on the public cloud and running
directly on the Xen hypervisor (in this case, on Amazon EC2). Such
appliances could be auto-configured and deployed directly to the
public cloud (e.g. Rackspace or Amazon EC2) or pushed to embedded
devices. There is also
[http://decks.openmirage.org](http://decks.openmirage.org), where
separate MirageOS appliances are being used to present slides for
conferences.  These are both cases of how MirageOS is being used right
now and below are examples of things we can do in the future.

#### Self-scaling architecture

We can create auto-scaling web-servers with very small footprints.
These would be cheaper to run than current solutions due to the small
size but they would also be highly elastic. If a sudden spike in
traffic occurs, the web-servers can be configured to create and deploy
copies of themselves to service the demand. This auto-scaling happens
so quickly that an incoming connection can trigger the creation of new
server and the *new server* can then handle that request before it
times out (which is on the order of milliseconds). When the demand
dies down again, these web-servers can automatically shut themselves
down. Since these machines boot fast we can be more elastic, raising
and lowering capacity to precisely meet demand and therefore only
spending what we actually need when we really need it.

#### Deployment to embedded devices

<a href="http://www.flickr.com/photos/lukew/6171377827/"><img style="float:left; margin-right: 15px;" src="/graphics/device-love.jpg"></img></a>

Using MirageOS, we can also create appliances that can run on embedded
devices. Such appliances can be deployed into small devices that are
scattered around your home, for example in plant pots to measure
moisture levels to chemical sensors in your fridge, which tell you
exactly what has gone off.  You could access the data from these
sensors via a web-sever appliance, which is also deployed locally in
your home on a device like a [Raspberry
Pi](http://www.raspberrypi.org).  Installing additional applications
into your Raspberry Pi appliance can be a a simple 1-click operation,
allowing you to share your data or compare with others.  Creating a
home-based network like this ensures you're not affected by any
upstream connectivity issues and that your data remains within your
control.

This same scenario can be deployed into a enterprise environment where
sensors around a building can monitor environmental conditions, adjust
lighting and many other things. When additional computation is
required, more appliances can automatically be created on a cloud
provider for the short duration that they're needed.

Overall, MirageOS provides substantial benefits in terms of increased
efficiency and safety and is ideal for deploying to both the public
cloud and embedded devices. Together with
[Irmin](http://nymote.org/software/irmin) and
[Signpost](http://nymote.org/software/signpost), MirageOS forms a core
piece of the
[Nymote/MISO toolstack](http://amirchaudhry.com/brewing-miso-to-serve-nymote)
to power the coming wave of
[Internet of Things devices](http://en.wikipedia.org/wiki/Internet_of_Things).

