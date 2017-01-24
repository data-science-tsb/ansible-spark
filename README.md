# Spark Cluster Setup with Ansible
Run this ansible script to spawn a spark cluster

# Documentations
- http://spark.apache.org/docs/latest/spark-standalone.html
- http://spark.apache.org/docs/latest/submitting-applications.html


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

ansible-playbook -e 'host_key_checking=False' playbook.yaml
```

##Spark Machine Basic Setup
We only need to do this once, just to give ansible SSH access to the machine
After this, just clone the damn machines without key mods
```
ssh-keygen -t rsa -b 4096 -C "lyndon.spark@spark.com"
cat /home/ec2-user/.ssh/id_rsa.pub >> /home/ec2-user/.ssh/authorized_keys
cat /home/ec2-user/.ssh/id_rsa_ansible.pub >> /home/ec2-user/.ssh/authorized_keys

pscp -i C:\Users\KWL\Desktop\DriveSync\aws-priv.ppk C:\Users\KWL\Desktop\id_rsa.pub ec2-user@54.149.247.58:/home/ec2-user/.ssh/id_rsa_ansible.pub
```