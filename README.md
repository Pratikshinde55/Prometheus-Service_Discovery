# Prometheus-Service_Discovery
Prometheus Service Discover setup for File_sd and EC2_sd

## Service Discovery:
Prometheus Service Discover helps us to monitoring dynamic environment that keep on changing.

Prometheus Service Discover auto detect Targets.

There are different Sevice Discovery:

### 1. File Service Discovery:

In this type of SD we create a custom YAMl file and put Targets information in that file, and that file we put in "prometheus.yml" config file for referance.

- Note:

  For Linux target Node Prometheus Node_exporter is installed and allow inbound rules.

- Step:1 [Create custom file]
  
   The file extension should be .yml

![image](https://github.com/user-attachments/assets/75748754-280b-41d0-9e92-08df3da69311)

Here,

" - targets: " is endpoint of target node where node metrics exposes.
" labels: " we can any label to target nodes this helps during run query on prometheus WebUI using "PromOL".

  
  
