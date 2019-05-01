# Ansible_Ubuntu_Install_Duo_SSH_2FA
Installs Duo 2FA on logins for both PAM and SSH. The duo is set to safe, so will allow logins if connection to Duo cannot be made. Change this to secure if needed.

This uses a template for common-auth based on sssd authentication. Edit that template as needed... You will probably need to understand PAM logic.

This has been tested on Ubuntu 16 and Ubuntu 18.

# Warning:
This will make edits to the following:
  - /etc/duo/pam_duo.conf
  - /etc/ssh/sshd_config
  - /etc/pam.d/common-auth

# How To Use:
This play is expected to be placed in your root ansible folder; default of /etc/ansible/

When downloaded, the following edits will need to be made:

1. Edit ./playbooks/Install_Duo.yml - Add the user you SSH/sudo with and change the hosts as needed for your enviornment.
2. Edit ./roles/install_duo/vars/main.yml - Enter your specific ikey and host entries. Change the defaults as needed or desired.
3. Edit ./roles/install_duo/vars/secrets.yml - Enter your skey and encrypt it after saving the file with ansible-vault encrypt path_to_file

When all the information has been changed for your environment, run the play. I typically run this play with ansible-playbook -kK --ask-vault-pass path_to_Install_Duo.yml

# Requirements
N/A

# Role Variables

| Variable  | Location | Required | Default | Description
| ------------- | ------------- | ------------- | ------------- | ------------- |
| commonauth_conf | ./roles/install_duo/defaults/main.yml | Yes | /etc/pam.d/common-auth | Path the PAM common-auth file |
| duo_host  | ./roles/install_duo/vars/main.yml | Yes  | N/A | The host API entry as given by Duo |
| ikey | ./roles/install_duo/vars/main.yml | Yes | N/A | The ikey entry as given by Duo |
| pam_duo_conf | ./roles/install_duo/defaults/main.yml | Yes | /etc/duo/pam_duo.conf | Path to the Duo PAM configuration file |
| skey | ./roles/install_duo/vars/secrets.yml | Yes | N/A | The skey as given by Duo |
| sshd_conf | ./roles/install_duo/defaults/main.yml | Yes | /etc/ssh/sshd_config | Path to the sshd configuration |

# Author Information
Steven Craig, 27Jan19
Edited 01May19 - Drastic overhaul on structure
