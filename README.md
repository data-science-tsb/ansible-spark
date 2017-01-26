# Spark Cluster Setup with Ansible
Run this ansible script to spawn a spark cluster

# Documentations
- http://spark.apache.org/docs/latest/spark-standalone.html
- http://spark.apache.org/docs/latest/submitting-applications.html

##ALL Machine Basic Setup
We only need to do this once, just to give each other passwordless SSH access, 
including ansible controller.
After this, just clone the damn machines without key mods.
I basically created an image with passwordless SSH and used it as a base
im
```
ssh-keygen -t rsa -b 4096 -C "lyndon.spark@spark.com"
cat /home/ec2-user/.ssh/id_rsa.pub >> /home/ec2-user/.ssh/authorized_keys
```

#Ansible Machine Master Setup
```
sudo yum install git
git clone git@github.com:hack-of-all-codes/ansible-spark.git
sudo pip install ansible
sudo mkdir /etc/ansible/

sudo vi /etc/ansible/hosts
[master]
35.160.75.242
[slaves]
35.161.66.165
35.161.234.3

ansible-playbook playbook.yaml
```

Add The Secret Stuffs
```
mkdir private_vars

vi private_vars/aws.yaml
aws_key_id: xxx
aws_key_secret: xxx
aws_image_master: ami-xxxxx
aws_image_slave: ami-xxxx
aws_slave_count: 2
aws_instance_type: t2.xlarge
aws_security_group: sg-xxxxxx
aws_region: us-west-2
```