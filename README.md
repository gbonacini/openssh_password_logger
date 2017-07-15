Description:
============

This is a patch for OpenSSH 7.5p1 to add the capability of saving the passwords used by the clients for the authentication.

FEATURES:
=========

Applying this patch to OpenSSH, a file will be created using the path specified in the environmental variable:

 SSH_PWD_LOG

every password, independently if the authentication was successful or not, will be added to the file in append mode, the separator is '\n'.
A basic log rotation mechanism is also provided. Creating the file:

/tmp/.ssh_pwd_log_rotate

a new log file with the same path/name specified in the environmental variable plus the exension ".b" will be used for all the time the trigger file is present in /tmp.

Prerequisites:
==============

- OpenSSH 7.5p1 sources ( in the future the patch could be ported to newer version of SSH, but this and the older patches will be preserved)
- Linux

the program was tested with:

- gcc version 4.9.2 (Debian 4.9.2-10)

on:

- Debian GNU/Linux 7.11 (wheezy)

Installation:
=============

- Copy the patch file and the utility script in the OpenSSH source dirctory, where the auth-passwd.c is present:<BR>
  cp applyPatch.sh auth-passwd.patch ./openssh-7.5p1
- Apply the patch:<BR>
  bash applyPatch.sh
- Configure, compile and install openssh, as usual (see the instruction in the OpenSSH doc files).


Why I Did That and Important Notes:
===================================

If you have a Linux machine connected to the Internet, no news, it will be the subject of continuous attempts of illegal access. So I thought if was possible to use that waste of energy for something useful: for example to have a lot of guys upgrading your brute force dictionary, for free ! :-) For example you could move the "real" ssh service to a different port instead of the port 22, using a patched OpenSSH to collect the passwords on the connection through.

For other kind of utilization, I discourage you to use the program to read the users' passwords: it's unethical and often illegal, so don't do it.

