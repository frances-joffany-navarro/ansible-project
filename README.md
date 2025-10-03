My Ansible Playbook
These are ansible playbook compilation

Do this project
Project
- Print the instance information associated to an EIP
- Disassocite an instance
- Associate an instance
- create a new repositories
- explore other area; researching


## Getting Started
- [https://docs.ansible.com/ansible/latest/index.html](https://docs.ansible.com/ansible/latest/index.html)
  
#### [Getting started with Ansible 01 - Introduction - Learn Linux TV](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

#### [Getting started with Ansible 02 - SSH Overview & Setup](https://www.youtube.com/watch?v=-Q4T9wLsvOQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=2)
  
  In the second episode, we take a look at some foundational knowledge, specifically OpenSSH which is required for Ansible to work. 

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

In part 3, we take a look at another foundational concept - Git. Everyone who effectively implements automation uses Git, and in this video, we look into creating a repository and how to push changes. 
  
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

In the fourth episode, we install Ansible and use it to run some ad-hoc commands. 

  <details>
  <summary>Notes</summary>
  
  run inventory with ssh key `ansible all --key-file ~/.ssh/ansible -i inventory -m ping`.
  
  use ansible.cfg file to put the default values like the path for the private key and the inventory name. Then run `ansible all -m ping`.
  
  List the hosts in inventory `ansible all --list-hosts`.
  
  Pull more info about the hosts `ansible all -m gather_facts` or to pull a single host `ansible all -m gather_facts --limit <ip address>`.</
  
  </details>
    
#### [Getting started with Ansible 05 - Running elevated ad-hoc Commands](https://youtu.be/FPU9_KDTa8A)

In the fifth video, we take a look at more ad-hoc commands - but this time, commands that perform changes. 
  
  <details>
  <summary>Notes</summary>
  
  `ansible all -m apt -a update_cache=true --become --ask-become-pass` is the same as `sudo apt update`
	
  `ansible all -m apt -a name=vim --become --ask-become-pass` is the same as `sudo apt install vim`. If there are multiple argument then add "" like "name=vim state=latest"

  </details>
	
#### [Getting started with Ansible 06 - Writing our first Playbook](https://youtu.be/VANub3AhZpI?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

In video #6, we get started on writing playbooks, which is how we'll use Ansible from here on out. 
  
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

  Add tags to your plays by adding `tags:` variable before the module.
  
  ```
  tags: ubuntu,db,mariadb
  apt:
  ```

  List the created tags in a playbook by typing `ansible-playbook --list-tags site.yml`

  Run a certain tag by typing `ansible-playbook --tags ubuntu --ask-become-pass site.yml`
  </details> 

#### [Getting started with Ansible 11 - Managing Files](https://youtu.be/teEhLgHpGgo?list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)

In video #11, we look at a few methods of copying files to target nodes.

  <details>

  <summary>Notes</summary>
    - Create a play to copy files to servers and a play to download a package and unzip it

  </details> 

  <details>

  <summary>Issues</summary>

    - Problem connecting to the host
      - Install openssh-server and copy public key to the host. Refer to Tutorial #2
      - Restart the servers or run this manually to the workstation when there is an 
    - Unable to acquire the dpkg frontend lock (Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 4379 (unattended-upgr))
      - error in dpkg `sudo dpkg -- configure -a`
      - [dpkg frontend lock fix](https://www.geeksforgeeks.org/linux-unix/how-to-fix-unable-to-acquire-the-dpkg-frontend-lock-error-in-ubuntu/)

  </details> 

#### [Getting started with Ansible 12 - Managing Services](https://youtu.be/soeBHGAMkoQ?si=5ao8jDgzCEW4PhC6)

In video 12, we learn how to manage systemd services that run in the background.

  <details>

  <summary>Notes</summary>

    Create a play where it automatically run httpd on boot and when it install it will ask

    Create a play to change a line in a httpd configuration file and restart the service

    Note: when registering a variable, check if you need to reuse or change it's name to avoid confusion

  </details>


#### [Getting started with Ansible 13 - Adding Users and Bootstrapping](https://youtu.be/P5iKWANifrU?si=Q6mpfhpCvCrNgxvA)

 In video 13, we'll look at adding a user, and then we'll set up Ansible to use a specific user for running tasks. Also, we'll walk through creating a bootstrap playbook specifically for adding new nodes. 

  <details>

  <summary>Notes</summary>
  Created a user called grumpy and added a ssh public key and created a sudoers file for this user.

  With this user using a sudoer permission without using password, we configure the ansible configuration file and put grumpy user as a remote_user. This resulted to not use the --ask-become-pass argument when running the ansible playbook.

  Before:  
  ``` ansible-playbook --ask-become-pass site.yml ```

  After:
  ``` ansible-playbook site.yml ```

  We created a bootstrap.yml and this playbook will be useful when for example a new server is provisioned, we would like to to run this playbook to create the user, add ssh public key and add the user to sudoers.


  Command used:
    - ``cat /etc/passwd``
  
  Ansible module used:
    - user - create a new user
    - authorized_keys - add or remove ssh to a user
    - copy - copy files
 
 System service user
  </details>
  
#### [Getting started with Ansible 14 - Roles](https://youtu.be/tq9sCeQNVYc?si=hVZTVX8qY3hr8UG3)

In video 14, we get started on roles. Roles in Ansible is one of its most amazing features, that allows you to categorize your hosts based on their intended purpose.

 <details>

  <summary>Notes</summary>
  
  Steps on categorizing hosts by roles:

  1. Update main yml file, which is the site.yml
      
      ```
      
      ---
      
      - hosts: all
        become: true
        pre_tasks:
        
        - name: update repo cache (CentOS)
          tags: always
          dnf:
            update_cache: yes
          changed_when: false 
          when: ansible_distribution == "CentOS"

        - name: update repo cache (Ubuntu)
          tags: always
          apt:
            update_cache: yes
          changed_when: false
          when: ansible_distribution == "Ubuntu"


      - hosts: all
        become: true
        roles:
          - base

      - hosts: workstations
        become: true
        roles:
          - workstations

      - hosts: web_servers
        become: true
        roles:
          - web_servers

      - hosts: db_servers
        become: true
        roles:
          - db_servers

      - hosts: file_servers
        become: true
        roles:
          - file_servers
      
      ```
  2. Create a role directory
  3. Create a directory for each role
  4. Create a tasks sub-directory for each role
  5. Create a file called main.yml in every tasks directory, then add the task dedicated to that role
  6. Optional: Incase a task needs to copy a file in files directory you need to create this directory and copy/create the need file.
 
Directory
 - roles
    - base
      - tasks
        - main.yml
    - db_servers
      - tasks
        - main.yml
    - file_servers
      - tasks
        - main.yml
    - web_servers
      - tasks
        - main.yml
      - files
        - index.html
    - workstations
      - tasks
        - main.yml
 - site.yml
 - inventory
 - ansible.cfg

Using roles helps to understand your code and make it cleaner.

  </details>
  
#### [Getting started with Ansible 15 - Host variables and Handlers](https://youtu.be/shBlQQZLU9M?si=lb8S5iimO0txln36)

 In video 15, we'll learn how we can benefit from host variables, and we'll also take a look at handlers as well which is a more efficient method of restarting services after a configuration change is made.

<details>

  <summary>Notes</summary>
  host variable is useful as a placeholder for packages for different host. For example there is host running in ubuntu and centOS. There are dedicated tasks for these os because the commands/package name are different from each other.

  We use host varaibles to store information needed per host such as the package names and with this we can use only one task to run a similar task by just using host variables.

  Steps on using host_variables
  
  1. Create a folder names host_vars
  2. Add a file using the ip_address of the host, 192.168.129.44.yml. Do not forget the file format .yml
  3. Add the variables that will be used in the playbook
  4. Update the task in the site.yml

  </details>

#### [Getting started with Ansible 16- Templates](https://youtu.be/s8F_YWGHeDM)

In video 16 (the final episode) we'll learn how to create templates, that can be used to automate the creation of configuration files for services/daemons.

<details>

  <summary>Notes</summary>
 Allows us to use a template to implement to multiple host and independently change the variable in each host as we see fit.

 For this example we use a template of ssh configuration file

 1. mkdir roles/base/templates 
 2. copy /etc/ssh/sshd_config to templates for ubuntu and centos
 3. Add `AllowUsers {{ ssh_users }}`
 4. Edit all host_vars files by adding ``ssh_user: "grumpy"`` && ``ssh_template_file: sshd_config_ubuntu.j2``
 5. Need to create a host_vars for the workstation by using the ip_address
 6. Edit the main.yml in roles/base/tasks
 7. Create a handlers inside base called restart_sshd

  </details>

### Credit
- [Is it better to disassociate first the EIP or reassociate?](https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_eip_module.html)
- [How to Use Ansible For DevOps? Hands-On Tutorial](https://spacelift.io/blog/ansible-devops)