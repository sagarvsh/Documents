# Terraform Interview quetions

1. Define Terraform.
Answer: The first entry among Terraform interview questions always deals with the definition of Terraform. Terraform is a tool for creating, changing, and versioning infrastructure with higher safety and efficiency. Terraform is now popular all over the world as an important addition to the chain of important DevOps tools. Terraform provides essential functionalities of managing solutions for in-house issues. The facility of ‘infrastructure as a code’ model in Terraform is also one of the popular reasons for its adoption. 

2. What are the reasons to choose Terraform for DevOps?
Answer: Candidates would definitely encounter this mention among top Terraform interview questions. The foremost reason to choose Terraform for DevOps is evident in the improvement of quality and efficiency in software delivery. Terraform supports automation and helps in running infrastructure as code. Another potential reason for choosing Terraform is the facility for implementing almost any type of coding principle. 

Also Read: Top 30 Kubernetes Interview Questions

3. What are the notable features of Terraform?
Answer: The features of Terraform would be one of the common topics of the latest Terraform interview questions. The key features of Terraform are as follows.

In-built graphing features for visualization of infrastructure
Friendly custom syntax helps in improving efficiency
The ability for understanding resource relationships
Contribution of updates and new features by the Open Source Project
Capability for breaking down a configuration into smaller parts for ease of organization and maintenance
4. How does Terraform work?
Answer: The working of Terraform is a formidable topic that churns out many relevant Terraform interview questions. The best answer to this question would be to point towards the plugin-based architecture of Terraform. The plugin-based architecture helps developers in extending functionalities of Terraform. Developers could write new plugins or compile the modified versions of current plugins. 

5. What are the notable applications of Terraform?
Answer: The use cases of Terraform are also important aspects of the best Terraform interview questions. Generally, the applications of Terraform are very broad due to the facility for extending the abilities of Terraform for resource manipulation. Here are some of the notable applications of Terraform.

Heroku App setup
Self-service clusters
Development of multi-tier applications
Creation of disposable environments
Multi-cloud deployment
Resource schedulers
Developing software demos
Ansible and Terraform are the two names that are prominent in the DevOps landscape now. Let’s understand the Ansible vs Terraform battle!

6. What is the process for making the object of one module available for another module at a higher level?
Answer: This entry can be one of the difficult Terraform interview questions. Here is the process to make an object of one module available for another module at a higher level.

Define an output variable in a resource configuration. 

Declare the output variable of module_1 for use in another module’s configuration

Create a new key name and ensure that it is equivalent to the output variable of module_1

Now, create a file ‘variable.tf’ for module_2

Set up an input variable inside the ‘variable.tf’ the file that would enable dynamic configuration of the resource in a module

In order to ensure the availability of the variable to another module, repeat the process again. The reason for this is the restricted scope of the particular variable to module_2.

7. Do you know about the new factors in the latest v1.24.0 and v1.25.0 Terraform Azure Provider?
Answer: Candidates should prepare for such Terraform technical interview questions. You can find multiple new resources in the latest versions of Terraform alongside new data resources. For example, Azurerm_batch_certificate. The new resource can support the management of certificates in the Azure batch. Furthermore, it also helps in the management of public IP and the prefix in networking. Another data resource in the latest versions is the Azurerm_firewall that helps in accessing data for a particular firewall existing already. In addition, the new versions also involve a lot of bug fixes. You can also find improvement in the azurerm_app_service resource in the latest versions.

8. Does Terraform support themes?
Answer: Candidates could land up with this entry among Terraform technical interview questions generally. The answer implies that the v0.3.1 of Terraform supports Gtk themes. We can use the command “cp/usr/wherever/THEMENAME/gtk/gtkrc $HOME/.gtkrc” for enabling gtk theme in a system. If the command shows error in opening the theme files or in the event of failure of the files to open, edits in the .gtkrc are mandatory. After editing, you have to attach the line “pixmap_path/usr/wherever/THEMENAME/gtk” at the start of the file name. Now, the theme could load at startup. 

9. What are the components of Terraform?
Answer: The structure of Terraform is another notable point for the best Terraform interview questions. The logical division of Terraform into distinct structures refers to two distinct components. The two components are the Terraform Core and Terraform Plugins. The Terraform Core utilizes remote procedure calls (RPCs) for communicating with Terraform Plugins. In addition, Terraform Core also offers diverse ways of discovering and loading plugins according to requirements. The Terraform Plugins represent an implementation for a specific service such as bash or AWS or provisioner. 

10. What are the primary responsibilities of Terraform Core?
Answer: This is one of the basic Terraform interview questions that you can face. The Terraform Core is a statically-compiled binary written by using the Go programming language. The compiled binary offers an entry-point for Terraform users. The primary responsibilities of the Terraform Core are as follows.

Resource state management
Execution of plans
Communication with plugins through RPC
Construction of Resource Graph
Infrastructure as code functionalities for reading and interpolation of configuration files and modules
Check: Most Common Jenkins Interview Questions & Answers

11. What is the Terraform Plugins?
Answer: Candidates should prepare for Terraform interview questions based on this topic. Terraform Plugins are executable binaries written in Go programming language. Plugins are basically the providers and provisioners in Terraform configurations. Terraform has various in-built provisioner plugins, and users have to discover provider plugins dynamically according to their requirements. The Terraform plugins help in domain-specific implementation of the service they represent. 

12. What are the primary responsibilities of the provider and provisioner plugins?
Answer: Candidates could find this entry as a follow up to Terraform interview questions on architecture or the Terraform plugins. The primary responsibilities for provider plugins are as follows.

Authentication with infrastructure provider
Definition of resources that map to particular services
Initialization of libraries used for making API calls
The primary responsibility of provisioner plugins is the execution of commands or scripts on a specific resource after creation or upon its destruction.

13. How does Terraform help in discovering plugins?
Answer: This entry is one of the most popular Terraform interview questions. The command “terraform init” helps Terraform read configuration files in the working directory. Then, Terraform finds out the necessary plugins and searches for installed plugins in different locations. In addition, Terraform also downloads additional plugins at times. Then, it decides the plugin versions for using and writes a lock file for ensuring that Terraform will use the same plugin versions. 

 14. What are the different behaviors of Terraform plugins during discovery?
Answer: This question is one of the tricky Terraform interview questions that can confuse many expert candidates. The behavior of the plugins depends on their type. The three kinds of plugins are built-in provisioners, providers by HashiCorp, and third-party providers and provisioners. The in-built provisioner plugins are always available in the Terraform binary. The providers by HashiCorp download automatically if not installed already. Regarding the third-party providers and provisioners, you have to install them manually. 

15. What is the Terraform configuration for creating a single EC2 instance on AWS?
Answer: Candidates could land up with this interesting entry among Terraform DevOps interview questions. The following Terraform configuration helps in creating a single EC2 instance on AWS.

    ```
    provider "aws" {

    region = "ap-south-1"

    }

    resource "aws_instance"

    "example" {

    ami = "ami-4fc58420"

    instance_type = "t2.micro"

    tags {

    Name = "terraform-example"

    }

    }
    ```
It is required to be fully prepared before going for a DevOps interview. Prepare with these Top DevOps Interview Questions to ace the interview!

16. Why does POVRay render fields and does not display sometimes?
Answer: This is one of the critical Terraform DevOps interview questions. The primary reason for the failure of default export to POVRay could be the lower version of POVRay. Version 3.0 of POVRay does not support the display. The same reason could be evident in the case of failure in a display of POVRay without error reports. Terraform works effectively with the 3.1 version of POVRay. So, you should use the –pov30 switch for informing Terraform about the issue. You can check the version of POVRay by typing “POVRay” and observing the first line of the output. 

17. How can I check if the POVRay install is compatible with Terraform?
Answer: Candidates could find tough Terraform interview questions like this one. You can try “povray+l tf_land.pov” to check whether the POVRay installs on your system is ok with Terraform. You can find two outcomes – one good and one bad. The good message is an error “tf_land.pov:26:error: Error opening TGA image”. The “tf_land.pov” denotes the file distributed in the root directory of terraforming. It means that you can find the included file in the POV on your system. The second message is about ‘colors.inc,’ that indicates the absence of files in your POV. As a result, you can clearly find out whether the POVRay installs works with Terraform or not. 

18. What if I encounter a serious error and want to rollback?
Answer: Candidates should find this entry among practical Terraform interview questions. The answer is recommitting the previous version of the code for making it the new and current version in a VCS (Version Control System). As a result, a terraform run triggers and runs the old code. It is essential to ensure that the old code contains all entities provisioned in the code for rollback. If the state file has been subject to corruption from a recent Terraform run, then you can opt for State Rollback Feature in Terraform Enterprise. It can help you to roll back to the previous latest state. The validation for this process is the versioning of every state change. 

19. Can I add policies to the open-source or Pro version of Terraform Enterprise?
Answer: This is one of the most popular Terraform interview questions coming up in recent interviews. First of all, you cannot add policies to the open-source version of Terraform Enterprise. The same also goes for the Enterprise Pro version. The Premium version of Terraform Enterprise only could access the sentinel policies.

20. What are the ways to lock Terraform module versions?
Answer: Candidates could find such technical Terraform interview questions difficult. Preparing for such questions in advance gives candidates a definite advantage. The answer is that there is a proven way of locking Terraform module versions. Using the Terraform module registry as a source, you can use the ‘version’ attribute in the module in the Terraform configuration file. Using a GitHub repository as a source, you have to specify branch, versions, and query string with ‘?ref’.

21. Are callbacks possible with Terraform on Azure?
Answer: This is also one of the new Terraform interview questions for aspiring candidates. Callbacks are possible on Azure with Terraform by using the Azure Event Hubs. AzureRM provider of Terraform provides this functionality easily to users. Most important of all, Azure Cloud Shell of Microsoft provides an already installed instance of Terraform. 

If you’re a cloud professional preparing for an Azure interview, we recommend you to prepare with the top Azure interview questions.

22. Can I use Terraform for on-premises infrastructure?
Answer: Candidates could find this question as one of the tough ones based on real experience. The answer to this question clearly implies the feasibility of using Terraform with on-premises infrastructure. Many providers offer this functionality, and you can choose one according to your requirements. Certain providers also have APIs for accessing Terraform in on-premises infrastructure.

23. What are the version controls supported on Terraform?
Answer: The candidate could find this entry as one of the important Terraform interview questions. Although this question may seem to be the simplest of the lot, it is essential to point out the precise responses. First of all, GitHub is the basic version control supported on Terraform. In addition, you can also find the support of GitLab CE and GitLab EE on Terraform. Furthermore, Terraform also supports the Bucket Cloud. 

24. Is there any similarity between the management of Azure Availability Zones and management by other available cloud providers?
Answer: The response to this question would directly refer to the fact that availability zones have different areas and zones. Every availability zone has a specific power source and network. Any region with an enabled availability zone would have three different availability zones. You need to note that AzureRM Terraform provider does not have any accessible resources for the management of Azure Availability Zones. However, this is the present scenario, and AzureRM Terraform provider could include some improvements in the future for this issue. 

25. How can I upgrade plugins on Terraform?
Answer: The answer would start off with running ‘terraform init’ with the ‘-upgrade’ option. The command helps in rechecking the releases.hashicorp.com to find out new acceptable provider versions. The command also downloads the available provider versions. Such types of actions are evident in the case of providers which have their acceptable versions in the automatic downloads directory. The automatic downloads directory is “.terraform/plugins/<OS>_<ARCH>.”

In case of installation of any acceptable version of a specific provider in another location, the ‘terraform init -upgrade’ command will not download a new version. 

!!! tip 
    
    Chef is one of the top DevOps tools. If you are going for a DevOps interview, don’t forget to check out these top Chef interview questions and answers!

