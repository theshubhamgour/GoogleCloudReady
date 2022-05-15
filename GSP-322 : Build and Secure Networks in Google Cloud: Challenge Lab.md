# Task 1 : Remove the overly permissive rules
```
gcloud compute firewall-rules delete open-access
```

# Task 2 : Start the bastion host instance
```
gcloud compute instances start bastion

```
# Task 3 : Create a firewall rule that allows SSH (tcp/22) from the IAP service and add network tag on bastion
Replace the "[NETWORK TAG]" with the network tag provided in the lab.
```
gcloud compute firewall-rules create <NETWORK_TAG_NAME> --allow=tcp:22 --source-ranges 35.235.240.0/20 --target-tags <NETWORK_TAG_NAME> --network acme-vpc
gcloud compute instances add-tags bastion --tags=<NETWORK_TAG_NAME> --zone=us-central1-b
```
```
```
# Task 4 : Create a firewall rule that allows traffic on HTTP (tcp/80) to any address and add network tag on juice-shop
```
gcloud compute firewall-rules create <NETWORK_TAG_NAME> --allow=tcp:80 --source-ranges 0.0.0.0/0 --target-tags <NETWORK_TAG_NAME> --network acme-vpc
gcloud compute instances add-tags juice-shop --tags=<NETWORK_TAG_NAME> --zone=us-central1-b
```
# Task 5 : Create a firewall rule that allows traffic on SSH (tcp/22) from acme-mgmt-subnet network address and add network tag on juice-shop
```
gcloud compute firewall-rules create <NETWORK_TAG_NAME> --allow=tcp:22 --source-ranges 192.168.10.0/24 --target-tags <NETWORK_TAG_NAME> --network acme-vpc
gcloud compute instances add-tags juice-shop --tags=<NETWORK_TAG_NAME> --zone=us-central1-b
```

# Task 6 : SSH to bastion host via IAP and juice-shop via bastion
In Compute Engine -> VM Instances page, click the SSH button for the bastion host. Then SSH to juice-shop by
```
ssh [Internal IP address of juice-shop]
```
Congratulations, you're all done with the lab 😄
