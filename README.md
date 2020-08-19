# 				**Pipeline**
## **abc project**

**Environments:**
   > Development

   > Staging

   > Production

**Note:1** 
	
- Currently this pipelines are created for staging environment
	
- Pipelines are pushed to gitlab repo for respective environment branch



**Note:2**

Abc\_Staging_Pipelines_Playbooks Folder contains ansible playbooks and jenkinsfile for
abc staging Enviroment.


Pipelines are triggered from Jenkins console (staging - 0.0.0.0:9090) 

- All Jenkins jobs are cretaed with scripted pipeline and script will be the replica of Jenkinsfile for respective service.

- Ansible playbooks, scripts, and configurations will triggered from Jenkins server from respective directory. 


***Directory structure***

Path to directory: */var/lib/jenkins/Abc_Staging_Pipelines_Playbooks*

![ansible scripts](https://github.com/arundevops16/document/blob/master/staging-dir-structure.png)
