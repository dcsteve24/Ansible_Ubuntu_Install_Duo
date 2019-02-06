# Ansible_Ubuntu_Install_Duo_SSH_2FA
Installs SSH and Duo 2FA on SSH sessions. The duo is set to secure, so will not allow logins if connection to Duo cannot be made. Change this to safe if needed.

This has been tested on Ubuntu 16 and Ubuntu 18.

# Warning:
This will replace /etc/duo/login_duo.conf.

Running this only configures duo 2fA for SSH sessions. If you require 2FA for PAM logins as well, you will need to make additional changes.

# How To Use:
This play is expected to be placed in your root ansible folder; default of /etc/ansible/

When downloaded, the following edits will need to be made:

1. Edit ./playbooks/install_duo_ssh.yml - Add the user you SSH/sudo with and change the hosts as needed for your enviornment.
2. Edit ./roles/install_duo_ssh/templates/login_duo.conf.j2 - Enter your specific ikey, skey, and host entries. Change the failmode to reflect your desired action; defaults as secure.

When all the information has been changed for your enviornment, run the play. I typically run this play with ansible-playbook -kK --ask-vault-pass path_to_sssd_auth.yml
