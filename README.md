# Prometheus Service Discover setup for File_sd and EC2_sd

## Service Discovery:
**Prometheus** Service Discover helps us to monitoring dynamic environment that keep on changing.

---Prometheus Service Discover auto detect Targets

There are different Sevice Discovery:

## 1. File Service Discovery:

In this type of SD we create a custom YAMl file and put Targets information in that file, and that file we put in "prometheus.yml" config file for referance.

- Note:

  For Linux target Node Prometheus **Node_exporter** is installed and allow inbound rules.

### Step:1 [Create custom file]

Scraping menas retrieve data from targets.

The file extension should be .yml

![image](https://github.com/user-attachments/assets/75748754-280b-41d0-9e92-08df3da69311)

Here,

**- targets:** = is endpoint of target node where node metrics exposes.

**labels:** = we can any label to target nodes this helps during run query on prometheus WebUI using "PromOL".

![image](https://github.com/user-attachments/assets/f45ae27a-0aa9-46e3-bb2e-fd39f71575df)
  
### Step:2 [Add File name in prometheus.yml config file]

     vim prometheus.yml

![image](https://github.com/user-attachments/assets/13360711-fc7c-454e-b5d6-d33363b37522)

Here, 

**- job_name:** = we give job name for our task in prometheus.yml file.

**file_sd_configs:** = This defines File Service Discovery use.

**- files:** = we put custom file name here.

### Step:3 [Restart Prometheus server]

After make any changes in prometheus.yml config file then need to restart prometheus service for apply new changes.

Kill or delete prometheus service command:

     pkill prometheus

start prometheus command:

     ./prometheus

### Step:4 [ On prometheus WebUI]

Go to prometheus WebUI then go to Status here we see "Service Discovery"

![image](https://github.com/user-attachments/assets/fcd1935d-b0f6-4bfe-90b5-1dc8051e774d)

Go to prometheus WebUI then go to Status here we see Target list

![image](https://github.com/user-attachments/assets/d375adb1-7384-4f88-bf21-8bbd8fd77b8a)

PromQL
![image](https://github.com/user-attachments/assets/054766f9-f6dc-4d51-8e4a-f7bb7600fb64)


## EC2 Sevice Discovery:

Prometheus EC2 Service Discovery is useful for automatic detect AWS Instances.

- Note :

  EC2 instance must have installed prometheus node_exporter and allow Inbound rules.


### Step-1: [Authentication]

To access any aws service from outside we need access or credentials. When any instance launch then automatic data collect by prometheus by using prometheus.

For this on AWS Console i create IAM user and attach policy **"AmazonEC2ReadOnlyAccesss"** and create secret key for "Third party use"

![Screenshot 2024-09-23 165015](https://github.com/user-attachments/assets/6674760d-af72-43f0-9ffd-efb392be78f9)


### Step-2: [Prometheus config file]

- Note:

 this only get EC2 outside information like public IP and Private IP. but not get inside data.

**__address__** = This is endpoint of target node 

We know the endpoint of prometheus node_exporter is public Ip:9100 port no.  The endpoint is right then only Scraping is done.
 
" relabel_configs: " = This helps to set endpoint for EC2 Service Discovery and make perfect setup.

"- source_labels: "  = This is source for taking any thing put keyword.

" [__meta_ec2_public_ip] " = This is keyword for taking public Ip of EC2

"- source_labels: [__meta_ec2_public_ip] " = This take public Ip of newly launched EC2 instance from Service Discovery.

 regex: "(.*)" = It means any Ip



