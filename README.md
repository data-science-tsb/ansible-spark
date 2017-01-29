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

sudo vi /etc/ansible/ansible.cfg
[defaults]
host_key_checking = False

ansible-playbook playbook.yaml
ansible-playbook playbook-terminator.yaml
ansible-playbook playbook.yaml --private-key ~/Documents/KWL/keys/dev-lyndon.pem  --user ec2-user
```

Add The Secret Stuffs
```
mkdir private_vars

vi private_vars/config.yaml
aws_key_id: xxx
aws_key_secret: xxx
aws_image_master: ami-xxxxx
aws_image_slave: ami-xxxx
aws_slave_count: 2
aws_instance_type: t2.xlarge
aws_security_group: sg-xxxxxx
aws_region: us-west-2
spark_cluster_name: namespace_conflict
environment_type: TEST/PROD/STAGING

slave_port: 7078
slave_memory: 512mb
slave_core: 1
master_port: 7077
master_memory: 512mb
```

Spark Shell
```
spark-shell --executor-memory 1g --total-executor-cores 1 --executor-cores 1 --driver-memory 1g --driver-cores 1 --master spark://54.202.71.167:7077

54.202.102.150:8080

sc.textFile("sample-file.html").flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_ + _).saveAsTextFile("testxx")
```