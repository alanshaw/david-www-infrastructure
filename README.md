# david-www-infrastructure

[Ansible](http://www.ansible.com/) playbook for deploying the [david-dm.org](https://david-dm.org/) website.

Originally built for Ubuntu Server 14.04.1 LTS.

## Updating an existing deployment

1. [Install Ansible](http://docs.ansible.com/intro_installation.html) on your local machine
2. Have an existing user add your public ssh key to `/home/ansible/.ssh/authorized_keys` on the server so when you run ansible, you're able to login  as the ansible user
3. Obtain the SSL certificate and key for david-dm.org:
    * `provision/david-www/files/ssl/david-dm.org.key`
    * `provision/david-www/files/ssl/david-dm.org.crt`
4. Obtain existing production configuration for the site and copy into place:
    * `provision/david-www/files/configs/production.json`
5. Run ansible

    ```sh
    ansible-playbook -v -i provision/dev provision/playbook.yml
    ```

    (Replace `provision/dev` with the environment you want to provision)

## Setting up a new deployment

* Create the machine
* Add ansible user:

```sh
sudo adduser ansible
```

* Make ansible an sudoer by adding the following line to `/etc/sudoers`:

```
ansible ALL=(ALL) NOPASSWD:ALL
```

* Install `openssh-server`

```sh
sudo apt-get install openssh-server
```

* Add **your** public key to `/home/ansible/.ssh/authorized_keys`
* Optionally: disable password authentication by changing `#PasswordAuthentication yes` to `PasswordAuthentication no` in `/etc/ssh/sshd_config` and restart:
* If you've disabled password authentication you'd best also add your public key to `~/.ssh/authorized_keys` for the user you logged in as originally
* If you've disabled password authentication, restart the ssh service:
    ```sh
    sudo restart ssh
    ```
* Done, follow instructions for [Updating an existing deployment](#updating-an-existing-deployment)