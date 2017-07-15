Description:
============

This is a patch for OpenSSH 7.5p1 to add the capability of saving the passwords used by the clients for the authentication.

FEATURES:
=========

Applying this patch to OpenSSH, a file will be created using the path specified in the environmental variable:

 SSH_PWD_LOG

every password, independently if the authentication was successful or not, will be added to the file in append mode, the separator is '\n'.
A basic log rotation mechanism, is also provided, creating the file:

/tmp/.ssh_pwd_log_rotate

A new log file with the same path/name specified in the environment plus the exension ".b" will be used for all the time the trigger file is present in /tmp.

Prerequisites:
==============

- OpenSSH 7.5p1 sources ( in the future the patch cold be ported in newer version of SSH, but this and the older patches will be preserved)
- Linux

the program was tested with:

- gcc version 4.9.2 (Debian 4.9.2-10)

on:

- Debian GNU/Linux 7.11 (wheezy)

Installation:
=============

- copy the patch file and the utility script in the OpenSSH source dirctory, where the auth-passwd.c is present
  cp applyPatch.sh auth-passwd.patch ./openssh-7.5p1
- Compile the program:
  bash applyPatch.sh
- Configure, compile and install openssh, as usual (see the instruction in the OpenSSH doc files).


Why I did that and Important Notes:
===================================

If you have a Linux machine conected to the Internet, no news, it will be subjected continuously to attempts of illegal access. So I thought if was possible to use that waste of energy for something useful: for example to have a lot of guys upgrading your brute force dictionary, for free ! :-) For example you could move the "real" ssh service to a fifferent port using a patched OpenSSH to collect the passwords.

For other kind of utilization, I discorage you to use the program to read the user password: it's unethical and often illegal, so don't do it.

