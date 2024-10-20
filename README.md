# gcp_terraform
Build, change, and destroy infrastructure with Terraform

Create Resource Dependencies with Terraform

terraform plan -out static_ip>>>>>>>>>>>Saving the plan this way ensures that you can apply exactly the same plan in the future.
terraform apply "static_ip">>>>>>>>>>>>>Terraform created the static IP before modifying the VM instance. Due to the interpolation expression that passes the IP address to the instance's network interface configuration, Terraform is able to infer a dependency, and knows it must create the static IP before updating the instance.

Provision infrastructure with Terraform
  provisioner "local-exec" {
    command = "echo ${google_compute_instance.vm_instance.name}:  ${google_compute_instance.vm_instance.network_interface[0].access_config[0].nat_ip} >> ip_address.txt"
  }
  This adds a provisioner block within the resource block. Multiple provisioner blocks can be added to define multiple provisioning steps. Terraform supports many provisioners, but for this example you are using the local-exec provisioner.he local-exec provisioner executes a command locally on the machine running Terraform, not the VM instance itself.
  terraform taint google_compute_instance.vm_instance>>>>>>>to tell Terraform to recreate the instance and the terraform apply.

