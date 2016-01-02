[]: {{{1

    File        : README.md
    Maintainer  : Felix C. Stegerman <flx@obfusk.net>
    Date        : 2013-11-09

    Copyright   : Copyright (C) 2013  Felix C. Stegerman
    Version     : 0.0.1

[]: }}}1

## Description
[]: {{{1

  autossh-init - AutoSSH init script

[]: }}}1

## Usage
[]: {{{1

(Assuming user is 'autossh', but can be changed in /etc/default/autossh)

    $ sudo adduser --system --group --shell /bin/false --home /var/lib/autossh --disabled-password autossh

  Generate public key for user and add restrictions:

    $ sudo su -s /bin/bash autossh
    autossh$ cd ~
    autossh$ ssh-keygen
    autossh$ echo -n 'command="/bin/false",no-pty,no-agent-forwarding,no-user-rc,no-X11-forwarding '| cat - ~/.ssh/id_rsa.pub > /tmp/tmp_id_rsa.pub && mv /tmp/tmp_id_rsa.pub ~/.ssh/id_rsa.pub

  Copy key to the server via SSH:

    autossh$ ssh-copy-id remote-user@myserver.com

  Add script to init.d and edit defaults:

    $ sudo cp -i autossh.init /etc/init.d/autossh
    $ sudo update-rc.d autossh defaults

    $ sudo cp -i autossh.default /etc/default/autossh
    $ sudo vim /etc/default/autossh

    autossh$ ssh autossh@remote FAIL  # confirm fingerprint
    # alternatively -- and less securely! -- you can disable
    # StrictHostKeyChecking in the autossh_opts

    $ service autossh start

  Debian/Ubuntu:

    # Install Debian package development tools and helper programs for debian/rules
    $ sudo apt-get install debhelper

    # Build package
    $ dpkg-buildpackage -uc -j -b
    # package can be found on level up

    # Install package
    $ sudo dpkg -i ../autossh-init*deb

    # After installing the program will automatically restart

[]: }}}1

## TODO

  * improve output?
  * tests?

## License
[]: {{{1

  GPLv2 [1].

[]: }}}1

## References
[]: {{{1

  [1] GNU General Public License, version 2
  --- http://www.opensource.org/licenses/GPL-2.0

[]: }}}1

[]: ! ( vim: set tw=70 sw=2 sts=2 et fdm=marker : )
