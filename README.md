staenker.apt-sources-baseline
=========
[![Ansible Galaxy](http://img.shields.io/badge/AnsibleGalaxy-staenker.apt--sources--baseline-blue.svg?style=flat)](https://galaxy.ansible.com/list#/roles/2126)

Sets the contents of /etc/apt/sources.list a secure server should use as a
baseline.

A secure source is a source officially supported by the distribution and security
updates are provided for each package from the source. According to the ubuntu
documentation only sections main and restricted qualify for a secure source.

Apt sources used as a baseline are stored in the configuration file
`/etc/apt/sources.list`. Baseline means, that additional sources might be added
by placing a file with the source definition in the directory
`/etc/apt/sources.list.d`.

Support for Debian is currently not implemented. It will be as soon as I start
working with debian servers again(which might never happen or next week) or some
generous person provides a pull request containing the required extensions and
refactorings.

Requirements
------------

A Ubuntu based system is enough

Role Variables
--------------

 * country_code, default: de, examples: "de", "se", "us", ...
 * apt_release_code, default: trusty, examples: "precise", "trusty", "utopic", "vivid"
 * sections, default: 'main restricted', examples: "main", "main restricted"

A quick reminder on:

* Country Codes:
    * Should be default country code based.
    * Take this page to verify your guess: http://repogen.simplylinux.ch
* Ubuntu Apt Release codes:
    * precise => 12.04
    * trusty => 14.04
    * utopic => 14.10
    * vivid => 15.04 pre alpha
* Sections
    * You should not use anything other than:
        * "main"
        * "main restricted"
    * If you are absolutely sure about what you are doing:
        * "main restricted universe" => INSECURE
        * "main restricted universe multiverse" => INSECURE

Dependencies
------------

none

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: staenker.apt-sources-baseline, country_code: se, apt_release_code: trusty }
Will generate the following content in /etc/apt/sources.list

    deb http://se.archive.ubuntu.com/ubuntu/ trusty main restricted
    deb http://se.archive.ubuntu.com/ubuntu/ trusty-security main restricted
    deb http://se.archive.ubuntu.com/ubuntu/ trusty-updates main restricted

License
-------

Apache License, Version 2.0

Author Information
------------------

Awesome dude
