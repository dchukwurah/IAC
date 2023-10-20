# Orchestration and Terraform

## What is Terraform and what is orchestration?
![Terraform diagram.png](Terraform%20diagram.png)
Terraform is an open-source IaC tool that allows users to define, provision, and manage infrastructure using configuration files.
It supports various cloud providers like AWS, Azure, Google Cloud, and others, as well as other services like DNS providers, database technologies, and more.
Terraform uses HashiCorp Configuration Language (HCL) to define the infrastructure in a human-readable format.
It maintains a state of the infrastructure, allowing for efficient change planning and application, as well as error detection and resolution.

## **Who Created It?**
   - Terraform was created by HashiCorp and used by many companies such as netflix to deploy and provision software

## **Why Is It Needed?**
   - Terraform addresses the need for a consistent and unified workflow to provision and manage infrastructure across various cloud providers and on-premises environments.
   - It allows organizations to adopt Infrastructure as Code (IaC), making the infrastructure provisioning process more automated, consistent, and repeatable.
   - Terraform helps in managing the lifecycle of infrastructure using configuration files, enhancing the collaboration and versioning in infrastructure management.

## **When Was It Made?**
   - Terraform was first released in July 2014. Since then, it goes through regular updates and versions,  enhancing its capabilities and features.

## **Where Is It Used?**
   - Terraform can be used in various environments, including cloud platforms like AWS, Azure, Google Cloud, and more.
   - It is widely used by DevOps professionals and organizations looking to automate and optimize their infrastructure provisioning and management processes.


### How do we use Terraform
Terraform main file (main.tf) is our central point for running our code and we can use commands to run it in our terminal. 
Our 'variables.tf' file will define any variables to avoid repetition and maintain abstraction of sensitive data.
We can further ensure security by adding this and our statefile and back up to our .gitignore folder hence not including it in the version control.

Once the 'main.tf' has been created, we can initialise our directory:

    ```bash
    $ terraform init
    ```

Then, we can check for any errors when launching it:

    ```bash
    $ terraform plan
    ```

If successful, we can launch our infrastructure using the following command:

    ```bash
    $ terraform apply
    ```

Finally we can destroy the infrastructure or specific resources:

    ```bash
    $ terraform destroy 
    
    $ terraform destroy -target=<resource-type>.<resource-name>
    ```
