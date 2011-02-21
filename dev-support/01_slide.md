!SLIDE center
# Sysadmin for Dev Support
## To be or not to be the pinguin

![To be or not to be the pinguin](to-be-or-not-to-be-the-pinguin.jpg)

!SLIDE bullets
# Tryphon
## Radio, Web and free software

* Boxes
* Applications
* Services 

## Consulting

* [puppet, dev support, ...](http://www.tryphon.eu/services)

!SLIDE bullets
# Context

* Many projects
* Many (old) "servers"
* Many services
* Few people

!SLIDE bullets
# Avoid

* Big centralized services
* Unmanaged servers
* Jungle

!SLIDE bullets incremental
# Root idea
## VM per project

* Simple configuration for each project
* Several VMs by project (staging, customers)

!SLIDE bullets
# Examples
## Rails project

* git
* hudson / ccontrolrb
* postgresql / mongo
* unstable instance<br/>(passenger, bundler)
* trac

!SLIDE bullets
# Examples
## Java project

* git/svn
* hudson
* postgresql
* unstable instance<br/>(tomcat)
* trac

!SLIDE bullets
# Examples
## Debian project

* git
* buildbot
* pbuilder
* trac
* debarchiver

!SLIDE bullets
# Examples
## Staging instance

* passenger / tomcat
* postgresql / mongo

!SLIDE bullets
# Architecture
## Hosts

* VM farms
* Admin server<br/>(dns, puppetmaster, vpn, ...)
* Switch

!SLIDE smbullets
# Architecture
## User View

* project1.acmee.priv
* project2.acmee.priv
* project2-staging.acmee.priv
* project3.acmee.priv
* project3-customer1.acmee.priv

!SLIDE bullets
# Examples
## Others

* Staging VMs for customers
* Shared tools :<br/>OSM server, Oracle server

!SLIDE bullets
# Architecture
## Network

* VLAN for dev
* VLAN for staging
* VLAN for customers (?)
* VLAN**s**
* vpn

!SLIDE bullets incremental
# Simplicity

* 1 usage / context by VM
* No big services
* Simple tools
* Simple configurations
* Simple authentication

!SLIDE bullets
# Flexibility
## Follow project 

* Live ... and dead
* New project anytime
* Isolate software choices
* Shutdown useless VMs

!SLIDE bullets incremental
# Scalability
## Grow with project

* From 1 user<br/>git, no instance (128MB)
* 10 users<br/>hudson, db, unit tests, java instance (2GB)
* to huge machines to process customer data (10GB)
* RAM and disks to grow

!SLIDE bullets
# Deployment
## Configuration management

* puppet/chef/...
* Shared configurations between nodes
* No way without (?)

!SLIDE bullets
# Deployment
## Puppet

<pre>
node 'audiobank.tryphon.priv' {
  include common
  include audiobank::dev
}

class audiobank::dev {
  include git::local
  git::repository { audiobank: }
  git::repository { "audiobank-client": }

  include trac::local
  trac::project::local { audiobank: }
  trac::project::local { "audiobank-client": }

  include audiobank
  include buildbot::audiobank
}
</pre>

!SLIDE bullets
# Deployment
## Configuration management

* 1 minute to describe a classic node
* Few minutes to create and deploy
* Ticket management

!SLIDE bullets
# Deployment
## Stay up to date

* Manage, no surrender
* Security upgrades ...
* Rebuild VMs

!SLIDE bullets
# Hosting
## @home or datacenter ?

* Xen farms
* vpn
* git
* low activity
* 16Go/2TB/4cores : 50€ HT ...

!SLIDE bullets
# Monitoring

* A lot of (simple) services
* "Public" status view
* Notify teams
* ... find application errors

!SLIDE bullets
# Security

* Access by hosts
* Admin or not
* Read-only public access (?)
* Staging networks (invitee network)

!SLIDE bullets
# Backup
## On dom0

* "All" with lvm/snapshot

## Inside VMs

* Host by host
* Service by service
* easy to find and restore

!SLIDE bullets
# Unstable/Staging/Prod

* Follow project phases
* Unstable updated by CI
* Staging for milestones

!SLIDE bullets
# Unstable instance

* A tool for sysadmin
* Detect earlier
* Like unit tests environment

!SLIDE bullets
# Authentication

* Basic : PAM + puppet
* OpenId for customers
* LDAP for big teams

!SLIDE bullets
# Databases

* Easy for unstable
* Strict for staging
* Ruthless for prod

!SLIDE bullets
# Databases
## Manage

* Create empty databases :<br/>templates, permissions
* Make easy dumps/restores
* Help for scripts, capistrano, ...

!SLIDE bullets
# External services
## For dev and customers

* [GitHub](http://github.com)
* [LightHouse](http://lighthouseapp.com)
* [BaseCamp](http://basecamphq.com)

!SLIDE bullets
# Externel dev team
## Can be simple

* detect low collaborations
* use git/dsc
* "public" read-only repositories

!SLIDE bullets
# External services
## For deployments

* [Hoptoad](http://hoptoadapp.com)
* [New Relic](http://newrelic.com)
* [MadMini](http://madmimi.com) (mail)

!SLIDE bullets
# Questions ?

* [Tryphon Services](http://www.tryphon.eu/services)
* [@tryphon](http://twitter.com/tryphon)

<div id="license">
  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">
    <img alt="Contrat Creative Commons" style="border-width:0" src="http://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png" />
  </a>
  <br/>
  <span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/InteractiveResource" property="dct:title" rel="dct:type">
    Sysadmin for Dev Support
  </span> 
  by
  <a xmlns:cc="http://creativecommons.org/ns#" href="http://tryphon.eu" property="cc:attributionName" rel="cc:attributionURL">Tryphon</a>
  <br/>
  Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">Creative Commons by-nc-sa 3.0 license</a>.
</div>
