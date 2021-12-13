# brew-group: set the brew group name and permissions

Syntax:

    brew-group [group [path]]

Options:

  * group: default is "admin"

  * path: default is "/usr/local"

Example:

    brew-group
    brew-group admin
    brew-group admin /usr/local


This command is useful for solving this brew error message:

    Warning: The /usr/local directory is not writable.
    Even if this directory was writable when you installed Homebrew,
    other software may change permissions on this directory.

When you run `brew-group`, the script will set the directory
to the group `admin` and the permissions to be writable.


## Details

Homebrew expects to manage all of the `/usr/local` directory.
If any other tool or script changes anything within `/usr/local`,
then Homebrew may be affected, and may prompt you to fix things.

For single-user systems, brew docs recommend commands such as:

    chown $USER /usr/local
    chmod 755 /usr/local

For multi-user systems like ours, we modify the group, not the user:

    chgrp admin /usr/local
    chmod 775 /usr/local


## Group details

We use the "admin" group, which is a default administrator group on OS X.

If you have a multi-user system and you want any staff to be able to use
brew, then you'll likely want to use the typical "staff" group on OS X.

If you want better security, or want to control exactly which users are
able to use brew, then you may want to create a "brew" group with users.
