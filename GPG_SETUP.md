Setting up GPG for Git
======================

If you want to use the GPG feature within `git`, there are a few steps for you to follow. These steps are described at many places, but a reminder never hurts.

Generating a new key
--------------------

If you don't have any GPG key yet, you can generate it from a terminal (or Git Bash for Windows) using the following command:

    $ gpg --gen-key
	
Follow the wizard and answer the questions about your identity (name, email address). It's advised to leave the default values, but if you wish extra security, chose a keysize of 4096.
Once generated, you can export your keys via the following commands:

    $ gpg --export --armor user@example.com > public.asc
	$ gpg --export-secret-keys -o private.gpg user@example.com
	$ gpg --output revokecert.asc --gen-revoke user@example.com

This will output three different files:

* `public.asc` contains your public key. Copy its content and [send it to GitHub](https://help.github.com/articles/adding-a-new-gpg-key-to-your-github-account/) or any other git service you use
* `private.gpg` contains your private key. This one needs to be put on a safe place. You must **avoid publishing somewhere at all cost**
* `revokecert.asc` contains a certification for revoking your keys. Simply put, you'll need it only if your keys gets compromised
	
Importing an existing key
-------------------------

If you already have a GPG key that you wish to use for signing your commits, you must first import it to your system (if it's not present).

Check which keys you already have:

    $ gpg --list-secret-keys

If your key is not in there, you can import it:

    $ gpg --import myprivatekey.gpg
	
Check it has been imported:

    $ gpg --list-secret-keys --keyid-format LONG
	
Copy the ID of your private key and register this key in `git-identity`:

    $ git identity --define-gpg <identity name> <gpgkeyid>

Additional resources
--------------------

Here are some interesting resources you might want to read if you wish to go deeper on GPG with git:

* [Generating a new GPG key](https://help.github.com/articles/generating-a-new-gpg-key/)
* [Adding a new GPG key to your GitHub account](https://help.github.com/articles/adding-a-new-gpg-key-to-your-github-account/)
* [Installing your GPG key in git](https://help.github.com/articles/telling-git-about-your-gpg-key/)
