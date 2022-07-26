### Instaling Chef automate and infra server
```shell
sudo hostnamectl set-hostname <fqdn-hostname>
sudo sysctl -w vm.max_map_count=262144
sudo sysctl -w vm.dirty_expire_centisecs=20000
```
```sh
curl https://packages.chef.io/files/current/latest/chef-automate-cli/chef-automate_linux_amd64.zip | gunzip - > chef-automate && chmod +x chef-automate
```

### Command Line Install of Chef Automate and Infra Server
```sh
sudo ./chef-automate deploy --product automate --product infra-server
```

### Configuration File Install of Chef Automate and Infra Server
```sh
sudo ./chef-automate init-config
```
Add a stanza to the configuration file to deploy Chef Automate and Chef Infra Server
```
[deployment.v1.svc]
products=["automate", "infra-server"]
```
```sh
sudo ./chef-automate deploy config.toml
```

### Check status and get dashboard credentials
```sh
sudo chef-automate status
sudo cat automate-credentials.toml
```
```sh
sudo chef-server-ctl user-create <user-name> <name> <surname> <email> '<password>' --filename <username>.pem

sudo chef-server-ctl org-create lab '<org-name>' --association_user <>user-name --filename <org-name>-validator.pem
```

### Reset admin password
```sh
chef-automate iam admin-access restore NEW_PASSWORD
```

### Installing Chef Workstation

### Configure git config
```sh
git config --global user.email "<email>"
git config --global user.name "<name>"
```

### Download and Install Chef Workstation
```sh
wget https://packages.chef.io/files/stable/chef-workstation/22.7.1006/ubuntu/18.04/chef-workstation_22.7.1006-1_amd64.deb
```

```sh
dpkg -i chef-workstation_22.7.1006-1_amd64.deb
```

```sh
chef --version
knife configure init-config
```

Add cookbook path to config file
```sh
nano .chef/credentials
cookbook_path	= ['/root/chef-repo/cookbooks']
```

Add *.pem file to .chef folder
```sh
scp <username>@<hostname>:/<pem-file> .
```

```sh
knife ssl fetch
knife ssl check
knife client list
```

Generate the chef-repo
```sh
chef generate repo chef-repo
```
Generate the new cookbook and upload
```sh
chef generate cookbook create-user
chef generate recipe user
cookstyle -a recipes/user.rb
knife cookbook upload create-user
knife cookbook list
```

```sh
knife bootstrap <fqdn-or-ip> --ssh-user <user> --ssh-password <pass> --node-name <node-name>
knife bootstrap <fqdn-or-ip> -N <node-name> -x <username> 
knife node list
```

```sh
knife node run_list add <node-name> RUN_LIST_ITEM
knife node run_list add <node-name> 'role[ROLE_NAME]'
knife node run_list add <node-name> 'COOKBOOK'
knife node run_list add <node-name> 'recipe[COOKBOOK::RECIPE_NAME]'
knife node run_list add <node-name> 'recipe[RECIPE_NAME]'
```

```sh
knife supermarket list
```

### Chef Automate Node
Getting recipe from infa server
```sh
sudo chef-client
```


```sh
docker run -it --name chef-workstation -v ~/chef/workspace:/root chef-workstation /bin/bash
```


