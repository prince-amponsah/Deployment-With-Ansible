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
![01](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/bc166171-419c-4c8a-9849-9136c5568da7)

STEP2
— Now we will install Ansible in host server (Ansible_host). you can follow the followings commands to install Ansible.

sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
STEP3
— copy the private key from local to Host server (Ansible_host) at (/home/ubuntu/.ssh). you can follow the following command to copy the key from local to Ansible_host.

scp -i “<<key pair name>>” <<key pair name>> <<public DNS of EC2>>:/home/ubuntu/.ssh

![02](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/7e916015-7aeb-4d4b-8820-40d96383f3cd)

STEP4
— Now we will access the inventory file using sudo vim /etc/ansible/hosts

Ansible ad hoc commands- using ad hoc commands is a quick way to run a single task on one or more managed nodes.

some examples of valid use cases are rebooting servers, copying files, checking connection status, managing packages, gathering facts etc.

The pattern for ad hoc commands looks like this :

$ansible [host-pattern] -m [module] -a “[module options]”

![03](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/2de5a6bb-988e-4ad9-9aa7-b3dbc9d2443a)

now we will define some servers in our inventory file and ping them using ansible all -m ping (you can refer the Screenshot)


Defining the servers in inventory file
Now we will ping the servers and do some server configurations ( refer the screenshot for better understanding)

![04](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/66df000b-1a8a-4a87-b2f1-803fb07b592f)

Booom we have successfully ping the 2 hosts that we have defined in our host file and checked the disk space of both server at the same time just by a single command , that’s the power of Ansible. you can also perform some other tasks if you want.

STEP5
— in this step we will learn about role of playbooks in ansible.

Playbooks are the simplest way in Ansible to automate repeating tasks in the form of resuable and consistent configuration files. Playbooks are defined in YAML files and any orderd set of steps to be executed in our managed nodes.

As mentioned , task in a playbook are executed from top to bottom. At a minimum, a playbook should define the managed nodes to target and some tasks to run against them.

![06](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/91e08d9a-4eec-47a6-8c1f-ffff1d64bfd2)

here we will see some example of playbooks and execute them and see how can we configure the server.

![07](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/fcffca47-8672-46d3-9e8d-49e2b29161f1)

A sample playbook to install nginx
Now we will run this playbook by using ( ansible-playbook <<name of play book>> ) .
![08](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/2a3cd589-07b5-4278-819f-612a80e4aa03)

so, as we can see in above screenshot that nginx is installed in both the server. so, it’s time to ssh one of the server and check whether nginx is installed or not.

![08](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/23ac85f2-40c4-4c06-b804-867b659d8361)

boom, as we can see we have successfully executed the playbook. so again, we saw how powerful and effective this tool is.

STEP6
— Now we will deploy a sample webpage using the ansible playbook. this sounds interesting, is it?

so first we will create an index.html file in which source code is present. at the end of the blog i will provide Github repository link where all the codes and playbooks are present.

![09](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/6a58c0c8-c551-4e8c-89c8-7d33b13d4ca2)

now we will create a playbook to perform this particular task.

![010](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/ff343c0e-a376-40d4-b29c-dc8d9437e636)

So, now we will run this playbook and see that webpage has deployed to all the dedicated servers.

![011](https://github.com/princekwes/Deployment-With-Ansible/assets/1629130/4df6b6ca-f61c-4a1e-8a9c-b9580bb3291a)

So, we successfully deployed a sample webpage to all the dedicated servers. and we can access this web application using theirs Public IP address.

So, as you can see I have performed all the tasks successfully. I recommend you to first read this article and understand the entire concepts and then move forward to Hands-ON. I believe this was the easiest way to explain about Ansible.

If you folks find any difficulties to perform the labs. kindly mail me at sandeep010498@gmail.com. I would be Happy to help.

GitHub repository — singhsandeep98/Ansible (github.com)

So folks, I hope you liked this article. if you find this article helpful then kindly give feedback and also follow me for more, and also do let me know about the topic of next Blog.

— — — — — — THANK YOU_________

— — — — SANDEEP SINGH______-
