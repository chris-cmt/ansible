# Ansible
Ansible playbooks and testing all sorts of different things

# Install notes

https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-debian

### From WSL
```
chill@DESKTOP-DTRFTAM:~$ ssh-keygen -t ed25519 -C "Ansible User"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/chill/.ssh/id_ed25519): /home/chill/.ssh/ansible
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/chill/.ssh/ansible
Your public key has been saved in /home/chill/.ssh/ansible.pub
```

## Copy 
```
ssh-copy-id -i .ssh/ansible.pub admin@192.168.178.60
ssh-copy-id -i .ssh/ansible.pub admin@192.168.178.221
```

## Test
```
ssh -i ~/.ssh/ansible admin@192.168.178.221
ssh -i ~/.ssh/ansible admin@192.168.178.60
```

## Create an Alis to speed up the ammount of time you need to enter your password
```
alias ssha='eval $(ssh-agent) && ssh-add'

chill@DESKTOP-DTRFTAM:~$ ssh-add
chill@DESKTOP-DTRFTAM:~/git/ansible$ ssha
Agent pid 6881
Enter passphrase for /home/chill/.ssh/id_ed25519:
Identity added: /home/chill/.ssh/id_ed25519 (chill default)
```

# Ansible
```
### Ansible commands
ansible all -m gather_facts

ansible all --list-hosts

ansible all -m ping

### Apt update
ansible all -m apt -a update_cache=true --become --ask-become-pass

### Install something
ansible all -m apt -a name=vim-nox --become --ask-become-pass

### Apt upgrade
ansible all -m apt -a upgrade=dist --become --ask-become-pass

### Ansible oneliner for apt update and upgrade
ansible all -i inventory -m ansible.builtin.apt -a "update_cache=yes upgrade=dist" -b

### Ansible one liner for apt update, upgrade and reboot
ansible all -i inventory -m ansible.builtin.apt -a "update_cache=yes upgrade=dist" -b && ansible all -i inventory -m ansible.builtin.reboot -b


### Ansible playbook for patching and reboot
ansible-playbook -i inventory playbooks/patching-reboot.yml 


```


