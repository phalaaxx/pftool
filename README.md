pftool
======

Set of tools/configuration files for easy postfix management of small postfix installations


Installation
------------

Install mandatory components:

	apt-get install postfix dovecot-imapd dovecot-pop3d

Install optional components. These are used for SPF and Postgrey policy checking:

	apt-get install postgrey postfix-policyd-spf-python opendkim opendkim-tools

Configure postfix and dovecot
-----------------------------

	pftool --setup

Edit /etc/postfix/main.cf and make any necessary changes to it. At the very least make sure to edit the *myhostname* configuration parameter.

Usage
-----

In order to use postfix in this configuration it is only necessary to create system accounts for use by postfix:

	useradd -m -s /bin/false -d /home/user/mail/user@example.com user@example.com
	useradd -m -s /bin/false -d /home/user1@example1.com user1@example1.com
	passwd user@example.com
	passwd user1@example1.com

Finally generate postfix mappings for the new account:

	pftool -u

Security considerations
-----------------------

Make sure to use /bin/false as default user shell for email users. If a user also needs to have shell access to the server it's a good idea to use separate system users for shell and email.
It's also a good idea to configure ssh to only allow access to users who are members of a specific group (for example: ssh).
