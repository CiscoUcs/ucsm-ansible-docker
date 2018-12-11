# UCSM Docker Image

This docker image contains all required packages to run UCS Manager Ansible playbooks against remote nodes.
The container was originally created to overcome managing dependencies within environments without internet access by SDBrett (SDBrett/ucsm-ansible-docker).

#### Using the container

The container entrypoint is the ansible-playbook command, allowing additional Ansible arguments to be passed at run time.

There is typically not a need to persist the container after running a playbook, so example run with the --rm flag.

If you're using paths within ansible.cfg for settings such as library, remember that the path is local within the context of the running container.

Run the below command on a docker host

`docker pull ciscodevnet/ucsm-ansible`

Example commands

Running from within an Ansible playbook directory

```dockerfile
docker run --rm \
 -v $(pwd):/ansible/playbooks \
 -it ciscodevnet/ucsm-ansible
 -i inventory site.yml
```

Running when external to Ansible playbook directory

```dockerfile
docker run --rm \
  -v /usr/share/my-ucsm-playbook:/ansible/playbooks \
  -it ciscodevnet/ucsm-ansible \
  -i inventory site.yml \
  --check
```

Run with custom hosts file

```dockerfile
docker run --rm \
  -v $(pwd):/ansible/playbooks \
  -v $(pwd)/hosts:/etc/ansible/hosts \
  -it ciscodevnet/ucsm-ansible \
  -i inventory site.yml
```

Using external library path

```dockerfile
docker run --rm \
  -v $(pwd):/ansible/playbooks \
  -v $(pwd)/library:/usr/share/ansible/library \
  -it sdbrett\ucsm-ansible \
  -i inventory site.yml
```

# UCS Projects

[ucsm-ansible](https://github.com/CiscoUcs/ucsm-ansible)

[ucsmsdk](https://github.com/CiscoUcs/ucsmsdk)

[ucsm_apis](https://github.com/CiscoUcs/ucsm_apis)
