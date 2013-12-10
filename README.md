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

  local & remote:

    $ adduser --system --group --shell /bin/false \
      --home /var/lib/autossh --disabled-password autossh

  local:
  
    $ su - autossh -s /bin/bash

    autossh$ ssh-keygen
    # <<PUBKEY>> below is the contents of ~/.ssh/id_rsa.pub here

  remote:

    autossh$ vim ~/.ssh/authorized_keys
    # on a single line, add:
    #   command="/bin/false",no-agent-forwarding,no-pty,no-X11-forwarding,permitopen="intern.toll:3306",permitopen="localhost:11211",permitopen="intern.toll:27017",permitopen="localhost:80",from="8.137.99.26,8.137.97.4" <<PUBKEY>>

  local:

    $ cp -i autossh.init /etc/init.d/autossh
    $ update-rc.d autossh defaults

    $ cp -i autossh.default /etc/default/autossh
    $ vim /etc/default/autossh

    autossh$ ssh autossh@remote FAIL  # confirm fingerprint
    # alternatively -- and less securely! -- you can disable
    # StrictHostKeyChecking in the autossh_opts

    $ service autossh start

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
