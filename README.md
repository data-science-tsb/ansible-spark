# Spark Cluster Setup with Ansible
Run this ansible script to spawn a spark cluster

# Documentations
- http://spark.apache.org/docs/latest/spark-standalone.html
- http://spark.apache.org/docs/latest/submitting-applications.html

# Setup
sudo yum install git
git clone git@github.com:hack-of-all-codes/ansible-spark.git

/etc/ansible/hosts
```
[master]
35.160.75.242

[slave]
35.161.66.165
35.161.234.3
```

#Ansible Machine Master Setup
```
sudo yum install git
git clone git@github.com:hack-of-all-codes/ansible-spark.git
sudo pip install ansible
vi /etc/ansible/hosts
```