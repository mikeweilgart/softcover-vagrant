# softcover-vagrant

A Vagrantfile for use with Softcover

Vagrantfile and README originally prepared 29 October 2015 by Mike Weilgart

## Instructions for using the Vagrantfile:

0. If you haven't installed vagrant and virtualbox, do so.
1. Put the Vagrantfile in a folder by itself.  (It's okay to have this README in the same folder.)
2. cd into that folder.  Then run the following:

    vagrant up

This will take roughly an hour and a half, as it will first download a minimal basebox, then
install ALL software needed to run softcover, including the several GB worth of tex packages.
Do it with a good internet connection.  Run it as `time vagrant up` if you're curious how long
it will take.

3. Log in to the vagrant box:

    vagrant ssh

You are now logged in to the vagrant box.  Don't do your work yet, though!

The point of Vagrant is a *disposable, reproducible* virtual environment.  You don't want to
run a 90 minute command every time you need to refresh your environment!  So we'll repackage
this vagrant box for later reuse.

4. If you want other packages to be available on your system each time you `vagrant up`,
install them now.  For example:

    sudo apt-get -y install vim
    sudo apt-get -y install git

5. Do the following to make your vagrant box as small and clean as possible for repackaging:

    sudo apt-get clean
    sudo dd if=/dev/zero of=/EMPTY bs=1M
    sudo rm -f /EMPTY
    cat /dev/null > ~/.bash_history && history -c && exit

6. Do the following (on your host system, of course) to repackage your box:

    vagrant package --output softcover-ubuntu-14.04.box

7. Do the following to add the box to your system in vagrant and make it usable:

    vagrant box add softcover-ubuntu-14.04 softcover-ubuntu-14.04.box

After you've done this the softcover-ubuntu-14.04.box file will not be used again.
You can delete it safely, or save it if you want.

8. Make a new folder where you will have the new vagrant box, cd into it and then:

    vagrant init softcover-ubuntu-14.04

You can now vagrant up and vagrant destroy all you want, and
softcover and asciidoc will be fully usable from the moment you vagrant ssh.
The directory on your host computer where the Vagrantfile is stored will be accessible
from the guest as `/vagrant` and I recommend keeping all softcover project directories in there.

## Acknowledgements

The following web pages were extremely helpful in preparing the Vagrantfile
and these installation instructions:

- http://blog.hostilefork.com/mobi-pdf-epub-softcover-ubuntu/
- https://scotch.io/tutorials/how-to-create-a-vagrant-base-box-from-an-existing-one
