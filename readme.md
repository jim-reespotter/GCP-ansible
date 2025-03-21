## ansible playbooks to do GCP stuff

my efforts at working out how to do ansible + GCP compute.

To begin with you need to:
- create a new project (add details to doit.yml vars)
- don't know how to connect a billing account via API, so do this by hand...
- you'll need to be logged in via gcloud (```gcloud auth login```)

then: ```ansible-playbook -i ./hosts.yml doit.sh```

What this does:
- pre tasks:
  - get public IP of this device (not quite right, not used yet)
  - gets an access token
  - enables compute APIs

- GCP tasks:
  - create an OS disk (Ubuntu)
  - create a VPC
  - create a public IP address
  - create a firewall (22+80TCP world accessible - work needed here?)
  - create a VM with all the above gubbins
  - set up SSH keys
  - set up SSH config
  - add to inventory

- on newly created VM:
  - install apache

(works for me, I get apache homepage at ```http://<ip address>/```)

### Issues:
- requires internet accessible SSH access
  - how to use ```gcloud compute ssh --proxy-through-iap``` here instead?
  - constraining SSH to just ansible host doesn't work
