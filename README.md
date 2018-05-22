git-identity
============

You often use Git in different contexts, like at work and for open-source
projects. You may then want to use different user names/email pairs to identify
yourself.

This is not an important part of your work, and setting this up should be really
fast. That's where `git-identity` comes in: setting up your identity information only takes one command with it.

Installing
----------

Simply link or copy the `git-identity` in a directory that's in your `PATH`, Git
will pick it up and make it available as `git identity`.

    $ ln -s git-identity ~/bin/git-identity

Under Windows, go to System > Advanced System Parameters > Environment Variable. Find the "Path" entry under *system variables* and add the path to where you downloaded `git-identity`.

Then you may setup a default identity with the following command (see Usage for more information):

    $ git identity --define default Me me@example.org

To get bash completion, just source the `git-identity.bash-completion` file
in your initialization scripts, such as `.bashrc`.

To get zsh completion, move the `git-identity.zsh-completion` file to a location present in your `$FPATH`, renaming the file to `_git-identity`.

You can also use [basher](https://github.com/basherpm/basher) to install git-identity:

    $ basher install madx/git-identity

Usage
-----

Add an identity:

    $ git identity --define <identity name> <user name> <user email>

Add a GPG key to the identity (see GPG specific information below)

	$ git identity --define-gpg <identity name> <gpgkeyid>
	Added GPG key DA221397A6FF5EZZ to [default] user <user@example.org> (GPG key: DA221397A6FF5EZZ)

Print the current identity:

    $ git identity
    Current identity: [default] user <user@example.org>

Change identity:

    $ git identity user2
    Using identity: [default2] user2 <user2@example.org>

List all identities:

    $ git identity --list
    Available identities:
    [default] user <user@example.org>
    [default2] user2 <user2@example.org>

Listing raw identities:

    $ git identity --list-raw
    default
    default2

Deleting an identity:

    $ git identity --remove <identity name>

Printing the raw identity (for use in scripts)

    $ git identity --print
    $ git identity --print <identity name>

Setting up GPG
--------------

More information about how to use GPG with `git-identity` may be found in [GPG_SETUP.md](GPG_SETUP.md)
