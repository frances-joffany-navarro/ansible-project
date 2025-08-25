# My Ansible Playbook
These are ansible playbook compilation

- Print the instance information associated to an EIP
- Disassocite an instance
- Associate an instance

## Getting Started
- [https://docs.ansible.com/ansible/latest/index.html](https://docs.ansible.com/ansible/latest/index.html)
  
#### [Getting started with Ansible 01 - Introduction - Learn Linux TV](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

#### [Getting started with Ansible 02 - SSH Overview & Setup](https://www.youtube.com/watch?v=-Q4T9wLsvOQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=2)
  <details>

  <summary>Notes</summary>

  OpenSSH is required in workstation, where you install Ansible, install openSSH-client. In servers, install openssh-server.
  
  Create SSH key pair indicating the type and some description `ssh-keygen -t ed25519 -C "description here"`.
  
  Copy the SSH public key to a server `ssh-copy-id -i ~/.ssh/ed25519.pub username@ipAdress`
  Create an alias called ssha by adding it inside `.bashrc` file `alias ssha=eval $(ssh-agent) && ssh-add` - this activates the ssh-agent and register the password one time. Type `ssha` to run the code and type `alias ssha` to show the code.
  </details>

  <details>
  
  <summary>Issues</summary>
  
  [Ubuntu terminal will not launch](https://askubuntu.com/a/1470425/2314689)
   
  [username is not in the sudoers file](https://stackoverflow.com/questions/47806576/username-is-not-in-the-sudoers-file-this-incident-will-be-reported)</details>
      
#### [Getting started with Ansible 03 - Setting up the Git Repository](https://youtu.be/FFaMqxpphjo?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

  <details>

  <summary>Notes</summary>

  Update and install git `sudo apt update` `sudo apt install git` 
  
  Create SSH key in github account: Settings > SSH and GPG keys > Add title and copy and paste the public SSH key from the workstation
  
  Clone git repository `git clone ssh@github`
  
  Configure name and email `git config --global user.name "name" && git config --global user.email "email@b.com"`
  
  Pushing for the first time `git push origin main`

  </details>

  <details>
  <summary>Issues</summary>

  [Enable shared clipboard between host and VM](https://medium.com/@undoworks4649/to-enable-copy-and-paste-as-well-as-folder-sharing-on-ubuntu-running-on-virtualbox-8a77cfb348f8)

  </details>

#### [Getting Started with Ansible 04 - Running ad-hoc Commands](https://youtu.be/4REljLsOnXk?si=VlK5jN1ROdlWZaPW)

  <details>
  <summary>Notes</summary>
  
  run inventory with ssh key `ansible all --key-file ~/.ssh/ansible -i inventory -m ping`.
  
  use ansible.cfg file to put the default values like the path for the private key and the inventory name. Then run `ansible all -m ping`.
  
  List the hosts in inventory `ansible all --list-hosts`.
  
  Pull more info about the hosts `ansible all -m gather_facts` or to pull a single host `ansible all -m gather_facts --limit <ip address>`.</
  
  </details>
    
#### [Getting started with Ansible 05 - Running elevated ad-hoc Commands](https://youtu.be/FPU9_KDTa8A)
  
  <details>
  <summary>Notes</summary>
  
  `ansible all -m apt -a update_cache=true --become --ask-become-pass` is the same as `sudo apt update`
	
  `ansible all -m apt -a name=vim --become --ask-become-pass` is the same as `sudo apt install vim`. If there are multiple argument then add "" like "name=vim state=latest"

  </details>
	
#### [Getting started with Ansible 06 - Writing our first Playbook](https://youtu.be/VANub3AhZpI?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)
  
  <details>
  <summary>Notes</summary>
  
  created two playbook, which [install](install_apache.yml) and [uninstall](remove_apache.yml) apache package 
  
  to run playbook `ansible-playbook --ask-become-pass install_apache.yml`
  </details>
    
  
#### [Getting started with Ansible 07 - The 'when' Conditional](https://youtu.be/BF7vIk9no14?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

In this tutorial, we take a look at differentiating our playbook based on the distribution of the target. That what we use the where condition 

  <details>
  <summary>Notes </summary>  

  Some servers use other package distribution like Ubuntu uses apt package and CentOS use dnf
    
  if you want to run some tasks in different distribution then `when: ansible_distribution in ["Ubuntu","Debian"]`
  
  Get information to use as use cases for when statement `ansible all -m gather_facts --limit ip_address | grep a ansible_distribution` this line says that gather facts on the indicated ip address and search the ansible_distribution variable
  
  </details>

  <details>
    <summary>Issues</summary>

For CentOS server, you need to run the following command to allow communication and for the httpd to run smoothly. These command should be automated for CentOS server:  
  - `sudo systemctl start httpd`
  - `sudo firewall-cmd --add-port=80/tcp`
  </details>

#### [Getting Started with Ansible 08 - Improving your Playbook](https://youtu.be/JJ-aoyydfVU?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70) 

In video #8, we look into a few ways we can clean up and consolidate the playbook we've been working with so far. 

  <details>
    <summary>Notes</summary>
  
  To consolidate plays, you can install multiple packages and update packages.
  
  You can create/use variables and initialize it in inventory per ip
  </details>

#### [Getting started with Ansible 09 - Targeting Specific Nodes](https://youtu.be/EraC1AuWEF8?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

In video #9, we split our inventory file into groups, and look at how to run tasks on nodes based on their group. 

  <details>

  <summary>Notes</summary>
    
  We split our inventory file by group like webservers, fileserver and etc.
  
  ~~~
  [webservers]
  192.168.129.44
  ~~~

  Then indicate in plays which host you want to implement the plays with.

  </details>  

#### [Getting started with Ansible 10 - Tags](https://youtu.be/gH_A-0zYLyw?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

In video 10, we learn how to add tags to our plays that can make it easier to target specific things when we don't want to run the entire playbook each time.

  <details>

  <summary>Notes</summary>
 

  </details> 

### Credit
- [Is it better to disassociate first the EIP or reassociate?](https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_eip_module.html)
