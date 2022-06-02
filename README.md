# Ansible-OCP-Azure-ARM-UPI-Installation


This playbook is to convert the below link steps into automation.

https://github.com/alpha-wolf-jin/ocp-azure-UPI


**Git**
```
echo "# Ansible-OCP-Azure-ARM-UPI-Installation" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/alpha-wolf-jin/Ansible-OCP-Azure-ARM-UPI-Installation.git
git config --global credential.helper 'cache --timeout 7200'
git push -u origin main

git add . ; git commit -a -m "update README" ; git push -u origin main
```

# Prepare Conf file

**The credential file is in the top dir where main.yaml amd roles dor locate** 

```
# ls
credential  credential.sample  main.yaml  README.md  roles
```


**The content of credential.sample**
credential.sample
```
# cat credential.sample 
Your Azure environment details:
Resource Group: openenv-9bkpg
Application: openenv-9bkpg
Application/Client/Service Principal ID: 52192eac
Password: 6NY.Z0475
Tenant ID: 1ce7852
Subscription ID: ede7f891-835

Azure CLI quickstart:
export GUID=9bkpg
export CLIENT_ID=52192ea
export PASSWORD=6NY.Z04
export TENANT=1ce7852f
export SUBSCRIPTION=ede
export RESOURCEGROUP=openenv-9bkpg

curl -L https://aka.ms/InstallAzureCli | bash
az login --service-principal -u $CLIENT_ID -p $PASSWORD --tenant $TENANT

See https://docs.microsoft.com/en-us/cli/azure/install-azure-cli for more info on installing the azure CLI
See https://docs.microsoft.com/en-us/cli/azure/ for full documentation of the azure CLI

When creating ARO clusters, you must specify the following credentials in the az aro create command using this preconfigured service principal:
Resource Group: openenv-9bkpg
Client ID: ab78a0b3
Client Secret: h4R
```
You can directly copy the mail content to "credential" file. 

**You can change the content of the below files as you want**

```
# cat roles/aro-instal/defaults/main.yml 
---
# defaults file for aro-instal

base_home: /root/aro
CLUSTER_NAME: aro
AZURE_REGION: eastus
BASE_DOMAIN: example.opentlc.com
```

**After modifying the above files, we can run playbook to setup OCP.**

```
# ansible-playbook main.yaml 

```

>**Note: the pull-secret info in roles/aro-instal/templates/install-config.j2 is modified. You need put you our own credentail before running this playbook**
