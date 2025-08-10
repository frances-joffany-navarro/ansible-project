# My Ansible Playbook
These are the playbook compilation

- Print the instance information associated to an EIP
- Disassocite an instance
- Associate an instance

## Getting Started
- [https://docs.ansible.com/ansible/latest/index.html](https://docs.ansible.com/ansible/latest/index.html)
- [Getting started with Ansible 01 - Introduction - Learn Linux TV](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)
- [Getting started with Ansible 02 - SSH Overview & Setup](https://www.youtube.com/watch?v=-Q4T9wLsvOQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=2)
  - Notes
      - OpenSSH is **required**: in workstation, where you install Ansible, install openSSH-client. In servers, install openssh-server
      - Create SSH key pair indicating the type and some description `ssh-keygen -t ed25519 -C "description here"`
      - Copy the SSH public key to a server `ssh-copy-id -i ~/.ssh/ed25519.pub username@ipAdress`
      - Create an alias called ssha by adding it inside `.bashrc` file `alias ssha=eval $(ssh-agent) && ssh-add` - this activates the ssh-agent and register the password one time. Type `ssha` to run the code and type `alias ssha` to show the code.
  - Issues
      - [Ubuntu terminal will not launch](https://askubuntu.com/a/1470425/2314689)
      - [username is not in the sudoers file](https://stackoverflow.com/questions/47806576/username-is-not-in-the-sudoers-file-this-incident-will-be-reported)
- [Getting started with Ansible 03 - Setting up the Git Repository](https://youtu.be/FFaMqxpphjo?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)
  - Notes
    - Update and install git `sudo apt update` `sudo apt install git` 
    - Create SSH key in github account: Settings > SSH and GPG keys > Add title and copy and paste the public SSH key from the workstation
    - Clone git repository `git clone ssh@github`
    - Configure name and email `git config --global user.name "name" && git config --global user.email "email@b.com"`
    - Pushing for the first time `git push origin main`
  - Issues
      - [Enable shared clipboard between host and VM](https://medium.com/@undoworks4649/to-enable-copy-and-paste-as-well-as-folder-sharing-on-ubuntu-running-on-virtualbox-8a77cfb348f8)
- [Getting Started with Ansible 04 - Running ad-hoc Commands](https://youtu.be/4REljLsOnXk?si=VlK5jN1ROdlWZaPW)
- [Getting started with Ansible 06 - Writing our first Playbook](https://youtu.be/VANub3AhZpI?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

### Credit
- [Is it better to disassociate first the EIP or reassociate?](https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_eip_module.html)
