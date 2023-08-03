# Deployment-With-Ansible
Deployment of a simple webpage using Ansible.



<strong>Things to be covered in Hands-On.</strong>

1. Creating Host server.

2. Install Ansible to Host server.

3. Creating 2 more EC2 instances (servers)

4. Add these EC2s to inventory file.

5. Configure the servers using command method.

6. Uses of playbooks.

7. Deployment of a simple webpage using Ansible.




The server which has ansible installed is known as the Control node while the remote hosts/servers which are configured are known as Managed nodes.

In ansible, you have two approaches to configure things: -

Ad-hoc commands (Command-line)
Playbooks

Usually, we write playbooks in Ansible to configure things. In playbooks, we write everything that needs to be configured on remote servers known as tasks. The playbook contains three things: -

1) Name of the play.

2) Hosts

3)Tasks. The format used for writing playbooks is YAML.

The remote servers or hosts which need to be configured are mentioned in the Inventory. There are two types of inventories: -

1) Static Inventory

2)Dynamic Inventory. We use dynamic inventory if our hosts are running on top of the cloud or in a container engine where the hosts are up and down frequently.

Now I won’t let you deep down in theoretical part. here we will do some Hands-On practice.

Deployment of a simple webpage using Ansible.

So, fasten your seat belt and just login to your AWS account. and follow me for next 10–15 minutes.

Step_1
First of all we will create 3 EC2 instances . make sure all three are created with same key pair. our one server would be host server where we perform all the tasks and rest are other servers.


SERVERS
STEP2
— Now we will install Ansible in host server (Ansible_host). you can follow the followings commands to install Ansible.

sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
STEP3
— copy the private key from local to Host server (Ansible_host) at (/home/ubuntu/.ssh). you can follow the following command to copy the key from local to Ansible_host.

scp -i “<<key pair name>>” <<key pair name>> <<public DNS of EC2>>:/home/ubuntu/.ssh


adding key pair to ec2
STEP4
— Now we will access the inventory file using sudo vim /etc/ansible/hosts

Ansible ad hoc commands- using ad hoc commands is a quick way to run a single task on one or more managed nodes.

some examples of valid use cases are rebooting servers, copying files, checking connection status, managing packages, gathering facts etc.

The pattern for ad hoc commands looks like this :

$ansible [host-pattern] -m [module] -a “[module options]”

now we will define some servers in our inventory file and ping them using ansible all -m ping (you can refer the Screenshot)


Defining the servers in inventory file
Now we will ping the servers and do some server configurations ( refer the screenshot for better understanding)


SERVER CONFIGURATION
Booom we have successfully ping the 2 hosts that we have defined in our host file and checked the disk space of both server at the same time just by a single command , that’s the power of Ansible. you can also perform some other tasks if you want.

STEP5
— in this step we will learn about role of playbooks in ansible.

Playbooks are the simplest way in Ansible to automate repeating tasks in the form of resuable and consistent configuration files. Playbooks are defined in YAML files and any orderd set of steps to be executed in our managed nodes.

As mentioned , task in a playbook are executed from top to bottom. At a minimum, a playbook should define the managed nodes to target and some tasks to run against them.

here we will see some example of playbooks and execute them and see how can we configure the server.


A sample playbook to install nginx
Now we will run this playbook by using ( ansible-playbook <<name of play book>> ) .


so, as we can see in above screenshot that nginx is installed in both the server. so, it’s time to ssh one of the server and check whether nginx is installed or not.


nginx is installed in the servers
boom, as we can see we have successfully executed the playbook. so again, we saw how powerful and effective this tool is.

STEP6
— Now we will deploy a sample webpage using the ansible playbook. this sounds interesting, is it?

so first we will create an index.html file in which source code is present. at the end of the blog i will provide Github repository link where all the codes and playbooks are present.


index.html
now we will create a playbook to perform this particular task.


Playbook to deploy a webpage
So, now we will run this playbook and see that webpage has deployed to all the dedicated servers.


Deployment of a sample webpage using Ansible playbook
So, we successfully deployed a sample webpage to all the dedicated servers. and we can access this web application using theirs Public IP address.

So, as you can see I have performed all the tasks successfully. I recommend you to first read this article and understand the entire concepts and then move forward to Hands-ON. I believe this was the easiest way to explain about Ansible.

If you folks find any difficulties to perform the labs. kindly mail me at sandeep010498@gmail.com. I would be Happy to help.

GitHub repository — singhsandeep98/Ansible (github.com)

So folks, I hope you liked this article. if you find this article helpful then kindly give feedback and also follow me for more, and also do let me know about the topic of next Blog.

— — — — — — THANK YOU_________

— — — — SANDEEP SINGH______-
