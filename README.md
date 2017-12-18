
## Centos7 Ansible PHP Playbook Install and Configuration


You can clone this repository and run `vagrant up` to start machine with provisioning.

Box & installation info:

- Centos 7
- Php 7.1.12
- Nginx 1.12
- Shared folder path `/var/www` to /var/www`
- Vhosts file creator in `ansible/roles/nginx/tasks/nginx-vhosts.yml`
- IP: 11.0.0.2

You can change shared folder path in `Vagrantfile`

If you add a vhost template or new vhost task in nginx-vhosts.yml please commit it.

In playbook.yml there're two lines commented out, these are for manual provisioning. If you want another zero configured machine to provisioned, you can follow below steps and uncomment below lines to run it. 


```
#- hosts: '{{ server.hostname }}'
#  remote_user: '{{ server.remote_user }}'

- hosts: 'all'
```

* Add below configuration to connect your vagrant machine from anywhere

```
# vim ~/.ssh/config

// Add
Host vagrant-centos7
    Hostname 11.0.0.2
    Port 22
    User vagrant
    IdentityFile VAGRANTBOX_INSTALLED_PATH/.vagrant/machines/default/virtualbox/private_key
```

* Use vagrant user for connections 

* Generate ~/.ansible/hosts file and add host list ( IP or /etc/hosts domain)
```
[centos7]
vagrant-centos7
```

* Run `ansible all -m ping` and check response for connection. 

Output sample:
```
vagrant-centos7 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
###### NOTE: you can check connection with `ansible all -a "ls -laht ~"` it must give you a list of files of your home directory


* Enter the ansible directory and run `ansible-playbook playbook.yml` and provisions will be started

