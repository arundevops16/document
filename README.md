# 				**Pipeline**
## **abc project**

**Environments:**
   > Development

   > Staging

   > Production

**Note:1** 
	
- Currently this pipelines are created for staging environment
	
- Pipelines are pushed to devops pipeline repo in Gitlab to respective branch(environment) 



**Note:2**

Abc\_Staging_Pipelines_Playbooks Folder contains ansible playbooks and jenkinsfile for
abc staging Enviroment.


Pipelines are triggered from Jenkins console (staging - 0.0.0.0:9090) 

- All Jenkins jobs are cretaed with scripted pipeline and script will be the replica of Jenkinsfile for respective service.

- Ansible playbooks, scripts, and configurations will triggered from Jenkins server from respective directory. 


***Directory structure***

Path to directory: */var/lib/jenkins/Abc_Staging_Pipelines_Playbooks*

![ansible scripts](https://github.com/arundevops16/document/blob/master/staging-dir-structure.png)



###Jenkinsfile: 

Jenkinsfile contains

- def : Variables in Jenkinsfile can be define

- Label: On which node the job runs

- Stages: Containing a sequence of one or more stage directives, the stages section is where the bulk of the "work" described by a Pipeline will be located.

- Post: Post section of a Pipeline is guaranteed to run at the end of a Pipeline’s execution, we can add some notification or other steps to perform finalization, notification, or other end-of-Pipeline tasks.


**Plugins used in Jenkins:**

- Git

- Maven

- Ansible

- 






###Ansible playbooks:

Playbooks are the files where Ansible code is written. Playbooks are written in YAML format. Playbooks are one of the core features of Ansible and tell Ansible what to execute. They are like a to-do list for Ansible that contains a list of tasks which user wants to execute on a particular machine.


**Note:3**

> Each application contains playbook for deploying application called **Deployment.yml** 

*hosts:*
This tag specifies the lists of hosts or host group against which we want to run the task. The hosts field/tag is mandatory. It tells Ansible on which hosts to run the listed tasks. The tasks can be run on the same machine or on a remote machine. One can run the tasks on multiple machines and hence hosts tag can have a group of hosts’ entry as well.

vars
Vars tag lets you define the variables which you can use in your playbook. Usage is similar to variables in any programming language.

tasks
All playbooks should contain tasks or a list of tasks to be executed. Tasks are a list of actions one needs to perform. A tasks field contains the name of the task. This works as the help text for the user. It is not mandatory but proves useful in debugging the playbook. Each task internally links to a piece of code called a module. A module that should be executed, and arguments that are required for the module you want to execute.

become:

Loops: 


Host file or Invetory file:


Modules used in Ansible playbook:

File:

Copy:

Shell:

Synchronize:

Template:

Service:
















