#
# Task 3:
## Description : A developer of the same 'XYZ' company has been accessing an AWS instance for quite long and deploy one of his client's production application server . One day the client calls in and reports that the production seems to be down. The perplexed developer goes into the server to take a look into the application server. To his surprise, his application server had crashed and the command to restart application server is not even working. The developer, being aware of some commands, tries to tweak around and discovers after running ` df -h ` that the server's disk is 100% full and most of the space is taken by /usr/src directory.
#
## Solution1:

**Assumption1:** If we are not able to execute any commands on the server due to 100% disk space utilization and not able login to the server then

1. Restart the EC2 instance and try to login

2. Find the files which are consuming more space.

> **`$ sudo find /usr/src/ -maxdepth 10 -type f -size +100M -exec ls -lh {} \;`**

- If log files are consuming more space then push to S3 and remove from the server which are earlier than 3 days.

- Also check any packages downloaded on this directory and remove if no longer nedded.

- Moreover remove unwanted file and directories which are consuming more space.

#
## Solution2: 

**Assumption2:**

Even after clearing the storage and existing data needs to recide in the server and then increase the disk space size. 

Steps to increase disk space size. 

Extending a Linux File System after resizing a Volume
- Log into your AWS account and navigate to EC2
- View Instance Details looking for the Root Device and Block Devices to identify the volume you want to resize
- Click the storage Device and select the EBS ID
- While in the Volumes panel click Actions at the top of the page
- Select Modify Volume to modify that particular volume
- Enter the desired volume size in GBs and click modify, yes to confirm
- SSH into your Instance
- Run lsblk to list available blocks (volumes) and note the volume size / names
- Run sudo growpart /dev/volumename 1 on the volume you want to resize, in our case it was sudo growpart /dev/xvda 1
- Run sudo resize2fs /dev/xvda1  to expand file system
- Check new size with df -kh command


**Monitoring disk space utilization of EC2 instance using perl scripts:**

AWS is providing perl scripts to collect disk space and RAM consuming by the EC2 instance and pumps to cloud watch. We can trigger alerts in cloud watch and configure SNS to send notifications if the servers reaches the threshold limit. 
By this we can would be alert and we can clear the disk space with out making the application down. 

