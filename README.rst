
servicez
********

.. image:: https://gitlab.com/constrict0r/servicez/badges/master/pipeline.svg
   :alt: pipeline

.. image:: https://travis-ci.com/constrict0r/servicez.svg
   :alt: travis

.. image:: https://readthedocs.org/projects/servicez/badge
   :alt: readthedocs

Ansible role to manage system services.

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/avatar.png
   :alt: avatar

Full documentation on `Readthedocs
<https://servicez.readthedocs.io>`_.

Source code on:

`Github <https://github.com/constrict0r/servicez>`_.

`Gitlab <https://gitlab.com/constrict0r/servicez>`_.

`Part of: <https://gitlab.com/explore/projects?tag=doombot>`_

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/doombot.png
   :alt: doombot

**Ingredients**

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/ingredient.png
   :alt: ingredient


Contents
********

* `Description <#Description>`_
* `Usage <#Usage>`_
* `Variables <#Variables>`_
   * `services <#services>`_
   * `services_disable <#services-disable>`_
   * `configuration <#configuration>`_
* `YAML <#YAML>`_
* `Attributes <#Attributes>`_
   * `item_expand <#item-expand>`_
   * `item_path <#item-path>`_
* `Requirements <#Requirements>`_
* `Compatibility <#Compatibility>`_
* `License <#License>`_
* `Links <#Links>`_
* `UML <#UML>`_
   * `Deployment <#deployment>`_
   * `Main <#main>`_
* `Author <#Author>`_

Description
***********

Ansible role to manage system services.

This role performs the following actions:

* Ensure the requirements are installed.

* Ensure the current user can obtain administrative (root)
   permissions.

* If the **services_disable** variable is defined, stop and disable
   the services listed on it.

* If the **configuration** variable is defined, stop and disable the
   *services_disable* listed on it.

* If the **services** variable is defined, enable and start the
   services listed on it.

* If the **configuration** variable is defined, enable and start the
   services listed on it.



Usage
*****

* To install and execute:

..

   ::

      ansible-galaxy install constrict0r.servicez
      ansible localhost -m include_role -a name=constrict0r.servicez -K

* Passing variables:

..

   ::

      ansible localhost -m include_role -a name=constrict0r.servicez -K \
          -e "{services: ['mosquitto', 'nginx']}"

* To include the role on a playbook:

..

   ::

      - hosts: servers
        roles:
            - {role: constrict0r.servicez}

* To include the role as dependency on another role:

..

   ::

      dependencies:
        - role: constrict0r.servicez
          services: ['mosquitto', 'nginx']

* To use the role from tasks:

..

   ::

      - name: Execute role task.
        import_role:
          name: constrict0r.servicez
        vars:
          services: ['mosquitto', 'nginx']

To run tests:

::

   cd servicez
   chmod +x testme.sh
   ./testme.sh

On some tests you may need to use *sudo* to succeed.



Variables
*********

The following variables are supported:


services
========

List of services to enable and start.

This list can be modified by passing a *services* array when including
the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.servicez -K -e \
       "{services: [mosquitto, nginx]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.servicez
         services:
           - mosquitto
           - nginx

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{services: [mosquitto, nginx]}"


services_disable
================

List of services to stop and disable.

This list can be modified by passing a *services_disable* array when
including the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.servicez -K -e \
       "{services_disable: [mosquitto, nginx]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.servicez
         services_disable:
           - mosquitto
           - nginx

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{services_disable: [mosquitto, nginx]}"


configuration
=============

Absolute file path or URL to a *.yml* file that contains all or some
of the variables supported by this role.

It is recommended to use a *.yml* or *.yaml* extension for the
**configuration** file.

This variable is empty by default.

::

   # Using file path.
   ansible localhost -m include_role -a name=constrict0r.servicez -K -e \
       "configuration=/home/username/my-config.yml"

   # Using URL.
   ansible localhost -m include_role -a name=constrict0r.servicez -K -e \
       "configuration=https://my-url/my-config.yml"

To see how to write  a configuration file see the *YAML* file format
section.



YAML
****

When passing configuration files to this role as parameters, it’s
recommended to add a *.yml* or *.yaml* extension to the each file.

It is also recommended to add three dashes at the top of each file:

::

   ---

You can include in the file the variables required for your tasks:

::

   ---
   services:
     - ['mosquitto', 'nginx']

If you want this role to load list of items from files and URLs you
can set the **expand** variable to *true*:

::

   ---
   services: /home/username/my-config.yml

   expand: true

If the expand variable is *false*, any file path or URL found will be
treated like plain text.



Attributes
**********

On the item level you can use attributes to configure how this role
handles the items data.

The attributes supported by this role are:


item_expand
===========

Boolean value indicating if treat this item as a file path or URL or
just treat it as plain text.

::

   ---
   services:
     - item_expand: true
       item_path: /home/username/my-config.yml


item_path
=========

Absolute file path or URL to a *.yml* file.

::

   ---
   services:
     - item_path: /home/username/my-config.yml

This attribute also works with URLs.



Requirements
************

* `Ansible <https://www.ansible.com>`_ >= 2.8.

* `Jinja2 <https://palletsprojects.com/p/jinja/>`_.

* `Pip <https://pypi.org/project/pip/>`_.

* `Python <https://www.python.org/>`_.

* `PyYAML <https://pyyaml.org/>`_.

* `Requests <https://2.python-requests.org/en/master/>`_.

If you want to run the tests, you will also need:

* `Docker <https://www.docker.com/>`_.

* `Molecule <https://molecule.readthedocs.io/>`_.

* `Setuptools <https://pypi.org/project/setuptools/>`_.



Compatibility
*************

* `Debian Buster <https://wiki.debian.org/DebianBuster>`_.

* `Debian Raspbian <https://raspbian.org/>`_.

* `Debian Stretch <https://wiki.debian.org/DebianStretch>`_.

* `Ubuntu Xenial <http://releases.ubuntu.com/16.04/>`_.



License
*******

MIT. See the LICENSE file for more details.



Links
*****

* `Github <https://github.com/constrict0r/servicez>`_.

* `Gitlab <https://gitlab.com/constrict0r/servicez>`_.

* `Gitlab CI <https://gitlab.com/constrict0r/servicez/pipelines>`_.

* `Readthedocs <https://servicez.readthedocs.io>`_.

* `Travis CI <https://travis-ci.com/constrict0r/servicez>`_.



UML
***


Deployment
==========

The full project structure is shown below:

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/deploy.png
   :alt: deploy


Main
====

The project data flow is shown below:

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/main.png
   :alt: main



Author
******

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/author.png
   :alt: author

The Travelling Vaudeville Villain.

Enjoy!!!

.. image:: https://gitlab.com/constrict0r/img/raw/master/servicez/enjoy.png
   :alt: enjoy


