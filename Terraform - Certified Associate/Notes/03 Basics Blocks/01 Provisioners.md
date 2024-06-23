Terraform provisioners install software, edit files and provision machines that are created with Terraform.

Terraform allows us to work with two different provisioners: 

#### Cloud Init :
An industry standard for cross-platform **cloud instance initializations**. When you **launch a VM** on a Cloud Service provider, we provide a YAML or a Bash Script a.k.a "user data / metadata" - these scripts run the first time the instance is created - so usually package installation, users and group creations can happen in this script
   
   Example:
   In the example shown here, the following script is executed within the VM instance on startup. Here a new file is created at the location provided in `var.config_file_loc`. In this location, an environment file is created using the `cat` command.
   
	```
	metadata_startup_script = <<-EOF
		#!/bin/bash
		touch ${var.config_file_loc}
		: > ${var.config_file_loc}
		cat > ${var.config_file_loc} <<-INNER_EOF
			PORT="${var.app_port}"
			# DATABASE
			DB_TYPE="${var.db_type}"
			DB_HOST="${google_sql_database_instance.instance.private_ip_address}"
			DB_PORT=${var.db_port}
			DB_USERNAME="${google_sql_user.user.name}"
			DB_PASSWORD="${google_sql_user.user.password}"
			DB_NAME="${google_sql_database.database.name}"
			# Pub/Sub
			USER_CREATED_TOPC="${var.pub_sub_topic_name}"
			EMAIL_VALIDITY_MINUTES="${var.env_variables_validity_minutes}"
	EOF
	```


#### Packer :
Packer is an automated image-builder service. You provide a configuration file to create an provision the image and the image is then delivered to a repository for use. 

Here is an example packer file snippet: 
```packer
packer {
	required_plugins {
		googlecompute = {
			version = ">= 0.0.1"
			source = "github.com/hashicorp/googlecompute"
		}
	}
}

source "googlecompute" "centos" {
	project_id = var.project_id
	zone = var.zone
	source_image_family = var.source_image_family
	ssh_username = "centos"
	image_name = var.image_name
}

...
```

Check out this link to see a sample packer file that defines and creates a virtual machine image in google cloud : <insert link to github file here >

![[Screenshot 2024-06-19 at 1.24.34 AM.png]]

Probably that's what is happening in the example shared above where we used the `metadata_startup_script`  within the terraform file to create the init script rather than explicitly use a separate module like cloud init.


Example usage of the `cloud-init` provisioner: 

![[Screenshot 2024-06-19 at 1.28.40 AM.png]]