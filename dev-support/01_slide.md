!SLIDE center
# Sysadmin for Dev Support

<!-- TODO -->

!SLIDE bullets
# Context

* many projects
* many (old) "servers"
* many services
* few people

!SLIDE bullets incremental
# Root idea
## VM per project

* simple configuration for each project
* several VMs by project (staging, customers)

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

* passenger
* or tomcat 
* postgresql / mongo

!SLIDE bullets
# Architecture
## Hosts

* xen farms
* admin
* switch

!SLIDE smbullets
# Architecture
## VMs

* project1.acmee.priv
* project2.acmee.priv
* project2-staging.acmee.priv
* project3.acmee.priv
* project3-customer1.acmee.priv

!SLIDE bullets
# Examples
## Others

* Stagings for customers
* Shared tools :<br/>OSM server, Oracle server

!SLIDE bullets
# Architecture
## Network

* VLAN for dev
* VLAN for staging
* VLAN for customers (?)
* vpn

!SLIDE bullets incremental
# Simplicity

* 1 use / context by VM
* no big services
* simple tools
* simple configurations
* simple authentication

!SLIDE bullets
# Flexibility
## Follow project 

* live ... and dead
* new project anytime
* isolate software choices
* shutdown useless VMs

!SLIDE bullets incremental
# Scalability
## Grow with project

* from 1 user<br/>git, no instance (128MB)
* 5 users<br/>hudson, db, unit tests, java instance (2GB)
* to huge machines to process customer data (10GB)
* RAM and disks to grow

!SLIDE bullets
# Deployment
## Configuration management

* puppet/chief/...
* shared configurations between nodes
* no way without (?)

!SLIDE bullets
# Deployment
## Puppet

<pre>
node 'chouette.dryade.priv' {
  include common
  include chouette::dev
}

class chouette::dev {
  include git::local
  git::repository { "chouette": }
  git::repository { "acceptance-tests": }

  include trac::local
  trac::project::local { chouette: }
  trac::project::local { "acceptance-tests": }

  include chouette::development
  include hudson::chouette
}
</pre>

!SLIDE bullets
# Deployment
## Configuration management

* 1 minute to describe a classic node
* few minutes to create and deploy

!SLIDE bullets
# Deployment
## Keep upgrade

* Manage, no surrender
* Security upgrades ...
* Lock

!SLIDE bullets
# Hosting
## @home or datacenter ?

* xen farms
* vpn
* git
* 16Go/2TB/4cores : 50€ HT ...

!SLIDE bullets
# Monitoring

* a lot of (simple) services
* "public" status view
* notify teams

!SLIDE bullets
# Security

* read-only public access
* staging networks (invitee network)

!SLIDE bullets
# Backup

* "all" : lvm/snapshot sur dom0
* service by service : inside vms

!SLIDE bullets
# Unstable/Staging/Prod

* follow project phases
* unstable updated by CI
* staging for milestones

!SLIDE bullets
# Unstable instance

* a tool for sysadmin
* detect earlier
* like unit tests environment

!SLIDE bullets
# Authentication

* Basic : PAM + puppet
* OpenId for customers
* LDAP, ...

!SLIDE bullets
# Databases

* easy for unstable
* strict for staging
* ruthless for prod

!SLIDE bullets
# Databases
## Manage

* create empty databases :<br/>templates, permissions
* make easy dumps/restores

!SLIDE bullets
# External services
## Dev and customers

* GitHub
* LightHouse
* BaseCamp

!SLIDE bullets
# Externel dev team

* detect low collaborations
* use git/dsc
* "public" read-only repositories

!SLIDE bullets
# External services
## Deployments

* [Hoptoad](http://hoptoadapp.com)
* [New Relic](http://newrelic.com)
* [MadMini](http://madmimi.com) (mail)

!SLIDE bullets
# Questions

* http://www.tryphon.eu/services

<div id="license">
  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">
    <img alt="Contrat Creative Commons" style="border-width:0" src="http://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png" />
  </a>
  <br/>
  <span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/InteractiveResource" property="dct:title" rel="dct:type">
    Sysadmin for Dev Support
  </span> 
  par 
  <a xmlns:cc="http://creativecommons.org/ns#" href="http://tryphon.eu" property="cc:attributionName" rel="cc:attributionURL">Tryphon</a>
  <br/>
  Mis à disposition selon les termes de la <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">licence Creative Commons by-nc-sa 3.0</a>.
</div>
