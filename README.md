# **Pipeline**
## **abc project**

**Environments:**
   > Development

   > Staging

   > Production

**Applications:** {{ app_name }}
   > adm-service

   > abc_backend_api

   > con_syn_service

   > push

   > mim

   > not_service

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



### Jenkinsfile: 

Jenkinsfile contains:-

- _def_		: Variables in Jenkinsfile can be define with this tag

- _Label_	: On which node the job runs

- _Stages_	: Containing a sequence of one or more stage directives, the stages section is where the bulk of the "work" described by a Pipeline will be located.

- _Post_		: Post section of a Pipeline is guaranteed to run at the end of a Pipeline’s execution, we can add some notification or other steps to perform finalization, notification, or other end-of-Pipeline tasks.


**Plugins used in Jenkins:**

- Git

- Maven

- Ansible


### Ansible playbooks:

Playbooks are one of the core features of Ansible and tell Ansible what to execute and playbooks are written in YAML format. They are like a to-do list for Ansible that contains a list of tasks which user wants to execute on a particular machine.


**Note:3**

> Each application contains playbook for deploying application called `**Deployment.yml**` 

Path to Ansible playbook:

> /var/lib/jenkins/aaaa/{{ app name }}/Deployment.yml

Inventory file:  Ansible works against multiple systems in your infrastructure at the same time. It does this by selecting portions of systems listed in Ansible’s inventory file.

> path to inventory file /var/lib/jenkins/aaaaa/hosts


**Key terms used in Ansible playbook:**

- *hosts:* This tag specifies the lists of hosts or host group against which we want to run the task on defined hosts.

- *vars:* Vars tag let us to define the variables which can use in the playbook. 

- *tasks:*  Playbook contains a tasks are a list of actions one needs to perform. Each task internally links to a piece of code called a module.

- *become:* Ansible allows you to ‘become’ another user, different from the user that logged into the machine (remote user). Set the value to ‘true’/’yes’ to activate privilege escalation.

- *Loops:* Often we want to do many things in one task, such as create a lot of users, install a lot of packages, or repeat a polling step until a certain result is reached.

- *Module:* A module that should be executed, and arguments that are required for the module you want to execute.

**Modules used in Ansible playbook:** **Deployment.yml**

File 

Copy

Shell

Synchronize

Template

Service

