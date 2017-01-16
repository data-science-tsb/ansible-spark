# Spark Cluster Setup with Ansible
Run this ansible script to spawn a spark cluster

# Documentations
- http://spark.apache.org/docs/latest/spark-standalone.html
- http://spark.apache.org/docs/latest/submitting-applications.html

# Setup
sudo yum install git
git clone git@github.com:hack-of-all-codes/ansible-spark.git

create the file: private_vars/nodes.yaml
```
nodes:
  - hostname: spark-master
    ip: 35.160.75.242
  - hostname: spark-slave001
    ip: 35.161.66.165
  - hostname: spark-slave002
    ip: 35.161.234.3
```

cd ansible-spark
sudo chmod u+x setup.sh
./bin/setup.sh
