git-identity
============

You often use Git in different contexts, like at work and for open-source
projects. You may then want to use different user names/email pairs to identify
yourself.

This is not an important part of your work, and setting this up should be really
fast. That's where `git-identity` comes in: setting up your identity information only takes one command with it.

*Note:* Identities are stored in the global git config. Using an identity copies the setting in the local repo git configuration. If you are changing the global config for one identity does *NOT* propagate the changes to the local repos. You will have use `git identity --update` in the repo folder to update the identity.

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

    $ git identity --define <identity name> <user name> <user email> [<ssh-file>] [<gpgkeyid>]

Add a GPG key to the identity (see GPG specific information below)

	$ git identity --define-gpg <identity name> <gpgkeyid>
	Added GPG key DA221397A6FF5EZZ to [default] user <user@example.org> (GPG key: DA221397A6FF5EZZ)

Add a SSH key to the identity

	$ git identity --define-ssh <identity name> <ssh-file>
	Added SSH key id_rsa_anotheraccount to [default] user <user@example.org> (SSH key: id_rsa_anotheraccount)

Print the current identity:

    $ git identity
    Current identity: [default] user <user@example.org>

Change identity:

    $ git identity user2
    Using identity: [default2] user2 <user2@example.org>

Update identity:

    $ git identity --update
    Using identity: [user] First Last <user_new_email@example.com> (SSH key: id_rsa_user_new_key)
    These are the changes:
    1,2c1,2
    <   core.sshcommand ssh  -i ~/.ssh/id_rsa_user
    <   user.email user@example.com
    ---
    >   core.sshcommand ssh  -i ~/.ssh/id_rsa_user_new_key
    >   user.email user_new_email@example.com

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

Priniting the local settings

    $ git identity --current-settings
    core.sshcommand ssh -i ~/.ssh/id_rsa_user
    user.email user@example.com
    user.identity user
    user.name First Last

Setting up GPG
--------------

More information about how to use GPG with `git-identity` may be found in [GPG_SETUP.md](GPG_SETUP.md)

Setting up SSH
--------------

If you have a valid SSH key associate to the agent you do not have to do anything beside `git identity --define-ssh <identity name> <ssh-file>`.

This sets  `core.sshCommand="ssh -i ~/ssh/ssh-file"` in the local git config when using that identity

### Creating a new identity 

    ssh-keygen -t rsa -b 4096 -C "yourname@yourdomain" -f ~/.ssh/id_rsa_anotheraccount
    ssh-add id_rsa_anotheraccount

### Debugging a ssh connection problem 

    git identity --define-ssh <identity name> <ssh-file> <verbosity>

With `verbosity=1` it will use `ssh -v`.
With `verbosity=2` it will use `ssh -vvv`.