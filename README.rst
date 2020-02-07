.. _section-role-griffin-watchee:

Role **griffin_watchee**
================================================================================

.. note::

    This documentation page and role itself is still work in progress.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/griffin_watchee>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-griffin-watchee>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-griffin-watchee>`__

Ansible role for convenient installation of the client part for custom Griffin
monitoring tool.

This role attempts to keep the things as simple as possible and performs only
basic installation of the system. The is a monitoring stack based on following
free tools:

* `Telegraf <https://docs.influxdata.com/telegraf/v1.12/>`__

**Table of Contents:**

* :ref:`section-role-griffin-watchee-installation`
* :ref:`section-role-griffin-watchee-dependencies`
* :ref:`section-role-griffin-watchee-usage`
* :ref:`section-role-griffin-watchee-variables`
* :ref:`section-role-griffin-watchee-files`
* :ref:`section-role-griffin-watchee-author`

This role is part of the `MSMS <https://github.com/honzamach/msms>`__ package.
Some common features are documented in its :ref:`manual <section-manual>`.


.. _section-role-griffin-watchee-installation:

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


.. _section-role-griffin-watchee-dependencies:

Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have dependency on this role.


.. _section-role-griffin-watchee-usage:

Usage
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

    # Run everything:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml


.. _section-role-griffin-watchee-variables:

Configuration variables
--------------------------------------------------------------------------------


Internal role variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. envvar:: hm_griffin_watchee__deb_url_telegraf

    Location of Telegraf Debian package with custom PostgreSQL output plugin.

    * *Datatype:* ``string``
    * *Default:* ``https://telegrafreleases.blob.core.windows.net/linux/telegraf_1.11.3~with~pg-1_amd64.deb``

.. envvar:: hm_griffin_watchee__install_packages

    List of packages defined separately for each linux distribution and package manager,
    that MUST be present on target system. Any package on this list will be installed on
    target host. This role currently recognizes only ``apt`` for ``debian``.

    * *Datatype:* ``dict``
    * *Default:* (please see YAML file ``defaults/main.yml``)
    * *Example:*

    .. code-block:: yaml

        hm_griffin_watchee__install_packages:
          debian:
            apt:
              - syslog-ng
              - ...

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


Built-in Ansible variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. envvar:: ansible_lsb['codename']

    Debian distribution codename is used for :ref:`template customization <section-overview-role-customize-templates>`
    feature.


.. _section-role-griffin-watchee-files:

Managed files
--------------------------------------------------------------------------------

.. note::

    This role supports the :ref:`template customization <section-overview-role-customize-templates>` feature.

This role manages content of following files on target system:

* ``/etc/telegraf/telegraf.conf`` *[TEMPLATE]*


.. _section-role-griffin-watchee-author:

Author and license
--------------------------------------------------------------------------------

| *Copyright:* (C) since 2019 Honza Mach <honza.mach.ml@gmail.com>
| *Author:* Honza Mach <honza.mach.ml@gmail.com>
| Use of this role is governed by the MIT license, see LICENSE file.
|
