
Variouse Ansible scripts (only one atm..) to setup local Ubuntu (14.04/16.04) development machine. 

## Instsall Ansible 

- Install Ansible if you haven't.

```
sudo apt-get update
sudo apt-get install -y --no-install-recommends software-properties-common python-software-properties wget
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

Note: 
1. It sounds obviouse, but you can't install Ansible using Ansible..
2. `software-properties-common` is needed to install command `apt-add-repository`,which is need to add ansible ppa.
3. `wget` is installed so that you can download the playbook.
4. Drop the `sudo` if you are already running as `root`, that is the case when you running a docker container by default.
5. You can also use [this dockerfile](https://github.com/pierrchen/docker-ubuntu1604-ansible/blob/master/Dockerfile) to build a Docker image with Ansible installed (so you can skip this step).

## anddev.yml

Set up the Android build enviroment on Ubuntu 16.04. Bascially, it translate [this](https://source.android.com/setup/initializing) to Ansible.

- Download the playbook

``` bash
wget https://raw.githubusercontent.com/pierrchen/ansible/master/anddev.yml
```

Notes: 
1. Remember that we installed `wget` previously.
2. We could have used `git` to clone whole repo, I just assume `wget` is *simpler* prerequisite than `git`.
3. If you want to run this playbook on Docker image, you can download the playbook on the host and copy it to the container, using  `docker cp anddev.yml $containerID:/anddev.yml`

- Play it

```
ansible-playbook -i "localhost," -c local -v anddev.yml
```

Have a cup of coffee while Ansible is working hard for you.