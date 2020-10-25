---
published: true
layout: post
title: "Calamares Password Weakness"
---
Systems installed by Calamares up to and including Calamares 3.1 have a weaker password salt than they should. This weakness is important if an attacker has a way to obtain the password hash. The Calamares team believes that installed systems should be as secure as possible, and therefore considers this weakness important.

Users are advised to reset their password on installed systems by using the password(1) utility, which will provide a stronger salt and hence a better password hash. This applies to all user accounts created during the installation of the system: the user's own account and to the root account, if the root account has a password.

<!--more-->


## Weakness

During system installation, Calamares creates a regular user -- for example, *bob* -- and sets the password for that user. Often, Calamares also sets a password for the root user.

When setting the password, Calamares uses a [predictable "salt"](https://cwe.mitre.org/data/definitions/760.html). This means that an attacker knows the salt for user *bob*, and also for user *root*. If the attacker can obtain the password hash (usually stored in `/etc/shadow`) then the knowledge of the salt can help the attacker prepare for a password cracking attempt.

## Impact

This weakness does not weaken the password security for logins on a single system. It does weaken the password if an attacker can obtain the password hash through some other means.

The predictable salt also means that passwords on different machines may be hashed with the same salt. This means that all *root* accounts installed by Calamares share the same salt, and that an attacker who can obtain `/etc/shadow` from many installed machines can use the predictable salt to build a rainbow table for *root* in advance.

Users added to the system after installation do not have this password weakness.
Users whose password has been changed with passwd(1) do not have this password weakness.

## Verification

To check if your installed system contains weakly-salted passwords, examine the `/etc/shadow` file for users with a salt equal to the username. Here is a way to use grep(1) to check:

    sudo grep -E '^([_[:alnum:]]*):\$6\$\1' /etc/shadow
    bob:$6$bob$dlQW5o8zM34dk2hQ:12345:0:99999:1:::

Any user with a salt (the part following `$6$` until the next `$`) equal to the username is weakly-salted.

## Mitigation

Users are advised to reset their password on installed systems by using passwd(1):

    user@system$ passwd
    Changing password for user.
    (current) UNIX password: 
    Enter new UNIX password: 
    Retype new UNIX password: 

When changing the password, the installed Linux system generates a new, random, salt for the password hash and the password is no longer affected by this weakness. Users may also want to reset the root password on the system if it is vulnerable, with `sudo passwd`.

Some Linux systems store a backup of `/etc/shadow` in `/etc/shadow-` . If this is the case, the weakly-salted passwords are still stored. Users are encouraged to change passwords **twice** for each affected account in order to overwrite the weakly-salted backup copy.

## Fixes

Existing DVDs, USB sticks, etc. with Calamares as system installer will
continue to be vulnerable to this password weakness.
Since Calamares is a system installer, it is usually not
available on the installed system, and it is not necessary
to update Calamares on any installed system.

Distributions using Calamares as system installer are strongly
advised to update to Calamares 3.1.1, which no longer creates
user password hashes with a predictable salt.

## Credits

Thanks to Bart Haan for finding the original password weakness
an Philip M&uuml;ller for extensive testing in Manjaro.


