.. _section-role-griffin-watchee:

Role **griffin_wathee**
================================================================================

Ansible role for convenient installation of the client part for custom Griffin 
monitoring tool.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/griffin_watchee>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-griffin-watchee>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-griffin-watchee>`__


Description
--------------------------------------------------------------------------------

This role attempts to keep the things as simple as possible and performs only
basic installation of the system. The is a monitoring stack based on following
free tools:

* `Telegraf <https://docs.influxdata.com/telegraf/v1.12/>`__

.. note::

    This role supports the :ref:`template customization <section-overview-customize-templates>` feature.


Requirements
--------------------------------------------------------------------------------

Python3 with pip3 utility should already be installed on target system.


Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.


Managed files
--------------------------------------------------------------------------------

This role directly manages content of following files on target system:

* ``/etc/telegraf/telegraf.conf``


Role variables
--------------------------------------------------------------------------------

There are following internal role variables defined in ``defaults/main.yml`` file,
that can be overriden and adjusted as needed:

.. envvar:: hm_griffin_watchee__deb_url_telegraf

    Location of Telegraf Debian package with custom PostgreSQL output plugin.

    * *Datatype:* ``string``
    * *Default:* ``https://telegrafreleases.blob.core.windows.net/linux/telegraf_1.11.3~with~pg-1_amd64.deb``

.. envvar:: hm_griffin_watchee__uninstall_list

    List of role-related packages, that will be removed from target system.

    * *Datatype:* ``list of strings``
    * *Default:* ``[]``

.. envvar:: hm_griffin_watchee__install_list

    List of role-related packages, that will be installed on target system.

    * *Datatype:* ``list of strings``
    * *Default:* (please see YAML file ``defaults/main.yml``)

.. envvar:: hm_griffin_watchee__apt_force_update

    Force APT cache update before installing any packages ('yes','no').

    * *Datatype:* ``enum (yes, no)``
    * *Default:* ``no``

.. envvar:: hm_griffin_watchee__dbname

    Configurations for database for storing monitoring metrics - database name.

    * *Datatype:* ``string``
    * *Default:* ``griffin``

.. envvar:: hm_griffin_watchee__dbuser

    Configurations for database for storing monitoring metrics - database user.

    * *Datatype:* ``string``
    * *Default:* ``griffin``

.. envvar:: hm_griffin_watchee__dbpswd

    Configurations for database for storing monitoring metrics - database password.

    * *Datatype:* ``string``
    * *Default:* ``griffin``


Additionally this role makes use of following built-in Ansible variables:

.. envvar:: ansible_lsb['codename']

    Debian distribution codename is used for :ref:`template customization <section-overview-customize-templates>`
    feature.


Installation
--------------------------------------------------------------------------------

To install the role `honzamach.griffin_watchee <https://galaxy.ansible.com/honzamach/griffin_watchee>`__
from `Ansible Galaxy <https://galaxy.ansible.com/>`__ please use variation of
following command::

    ansible-galaxy install honzamach.griffin_watchee

To install the role directly from `GitHub <https://github.com>`__ by cloning the
`ansible-role-griffin <https://github.com/honzamach/ansible-role-griffin-watchee>`__
repository please use variation of following command::

    git clone https://github.com/honzamach/ansible-role-griffin-watchee.git honzamach.griffin_watchee

Currently the advantage of using direct Git cloning is the ability to easily update
the role when new version comes out.


Example Playbook
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers_griffin_watchee]
    localhost

Example content of role playbook file ``playbook.yml``::

    - hosts: servers_griffin_watchee
      remote_user: root
      roles:
        - role: honzamach.griffin_watchee
      tags:
        - role-griffin-watchee

Example usage::

    ansible-playbook -i inventory playbook.yml


License
--------------------------------------------------------------------------------

MIT


Author Information
--------------------------------------------------------------------------------

Jan Mach <honza.mach.ml@gmail.com>
