# Run SSH Server (sshd) on Termux

install openssh

    pkg install openssh

get current user name

    whoami

will be something like `u0_a123`

get ip address

    ifconfig | grep -C 2 wlan | grep inet

ifconfig output parsing is an hassle

...SHOWTIME!

    sshd

now you can connect with

    ssh -p 8022 u0_a123@192.168.6.66 

Though, no, you can't. Because you don't have no password.

But you CAN setup a password on termux. Just do a:

    passwd

You can also make it more interesting and use a public key. Same old dance:

    ssh-keygen

...on the client-side host and generate a new public/private key pair. ED25519 is pretty fashionable now, as an encyption scheme, so you'll be likely getting a `~/.ssh/id_ed25519.pub` public key and a `~/.ssh/id_ed25519` private one.

somehow copy/paste/send the `id_ed25519.pub` file contents to the tail of the `~/.ssh/authorized_keys` file in the server-side host and you're pretty much done.

    cat ~/download/id_ed25519.pub >> ~/.ssh/authorized_keys

There you go:

    ssh -p 8022 u0_a123@192.168.6.66

...and enjoy.
