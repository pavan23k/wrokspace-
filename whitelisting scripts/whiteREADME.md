##AWS whitelisting automation through python scripts

####Prerequisites for python scripts :

* Python3
*	Boto3
*	AWS CLI
*	AWS credentials like access key, secret access key, region name etc.

#####To install python3, run the following commands:
* sudo yum install centos-release-scl
*	sudo yum install rh-python36
*	scl enable rh-python36 bash

####To install pip, run the following commands:
*	curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
*	python get-pip.py

####To install boto3, run the following commands:
*	pip install boto3

####To install awscli, run the following commands:
*	pip install awscli

####Then configure the AWS using following command:
*	aws configure
__Provide AWS access key, secret access key, region and output format__


**Scripts description:**

+	**sg_inbound_rules.py:**
> This script is used to create a text file (sg_inbound_rules.txt) that contains following informations about all security groups present in ‘us-east-1"region

* Security group name
*  Security group id
*	Protocol
*	Source cidr (IPv4)
*	From port
*	To port
+	**sg_inbound_rules_in_csv.py:**  
>This script is used to create a csv file (sg_inbound_rules_csv.csv) from the existing text file (sg_inbound_rules.txt) and will contain the information we have gathered in previous step.
+	**remove_open_inbound_rules.py:**  
>This script is used to remove all open inbound rules (0.0.0.0/0) and this inbound rule should be IPv4 ,i.e., not ::/0. This script will access the csv file (sg_inbound_rules_csv.csv) and check for CIDR value 0.0.0.0/0 in all security groups and then remove it.
+	**add_inbound_rules.py:**  
>This script is used to add the inbound security rules provided in the csv file (input_inbound_rules.csv).

+ **This csv file will contain following informations :**

  *	Security group id
  * Source ip (IP of user)
  *	Description (containing Username)
  *	Application
  *	Protocol
  *	From port
  *	To port

#####Parameters need to be changed when using these scripts in some other environment :-

+ Region name in
  * sg_inbound_rules.py
  * remove_open_inbound_rules.py
  * add_inbound_rules.py


- File location description of csv file in
  * remove_open_inbound_rules.py
  * add_inbound_rules.py
