### Task 6 Bringing it all together
### IaaC with CI/CD workflow

#### The goal of the task was:

1. Create a website, is sufficient demonstrate a website that displays text [Lorem Ipsum](https://loremipsum.io/) and an image on a single home page.

2. On the complexity of the solution is enough to create static website in Google Cloud Platform [GCP](https://cloud.google.com).

In order to set up an application that displays a web page, you could provide the following components:

1. **A web server**: The web server is responsible for serving web pages to clients over the internet. In this case the webserver is virtual machine (VM) in GCP.

2. **A programming language or framework**: To create dynamic web pages, you will need a programming language or framework that can generate **HTML and CSS** code dynamically. Popular web development languages include JavaScript, PHP, Python, Ruby, and Java. In this case the programming language is HTML.

3. **A text editor** or integrated development environment (IDE): A text editor or IDE is used to create and edit the code for the web pages and server-side scripts. There are many popular text editors and IDEs available, such as Visual Studio Code, Sublime Text, Atom, and Eclipse. In this case the used text editor is **Visual Studio Code** [VSC](https://code.visualstudio.com/).

4. **Deployment tools**: You will need tools to deploy your web application to a web server. Deployment was performed using **[Terraform]**(https://developer.hashicorp.com/terraform/intro) that is an infrastructure as code tool that lets you build, change, and version cloud and on-prem resources safely and efficiently. Deployment process was automated with **CI/CD** [GitHub](https://github.com/) Actions. The website was deployed on GCP, sample code you can find in [terraform docs](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/storage_bucket) and also [google cloud](https://cloud.google.com/storage/docs/creating-buckets).

5. **Version control system**: A version control system like **[Git]**(https://git-scm.com/) is useful for tracking changes to your code and collaborating with other developers.

To complete the task you should meet the following steps:

* Create an **account on GCP** and first project.
* Create a **Service Account** in the GCP console for Terraform: go to IAM -> create Service Account -> named it and Create. For the Role, choose "Project -> Editor", then click "Continue". You can skip granting additional users access, and click "Done".
* Generate the Key for that Service Account. Click **ADD KEY** and choose JSON for the Key type.
* Download the file that contains the private key. Store the file securely because yhis key cannot be recovered if lost.
* Create a bucket in which we will store the terraform state file. Do not grant public access to this bucket.

By default, Terraform stores state locally in a file named terraform.tfstate. This default configuration can make Terraform usage difficult for teams when multiple users run Terraform at the same time and each machine has its own understanding of the current infrastructure.

* Create a new **repository in Github**, go to the Settings tab in the repository. Choose Actions under the Security section. Click the button New repository secret.
Paste the contents of the your-file-name.json ->named and save it. You will later refer to the name of that variable in your Workflow.

* In VSC Create file **backend.tf** (remember to provide the name of the bucket you create before).The Terraform state file will be stored in this bucket. Sample code you can find in attached backend file.
* Create **provider.tf** file, remember to input the right project id. In this file you defines the provider of the resources.
* Create the **main.tf** that shows what kind of resources you are going to create.
* The last file is **terraform.yml, create .github/workflow/terraform.yml**. In attached sample code we wanted the workflow to run every time we push a new commit to the main branch in our repository.

In the end you can commit all files to the repository and push the change to the remote repository. Go to github.com and check the Actions tab in your repository. You should see the workflows in there (in other tools e.g gitlab we would call them pipeline runs).
In the Actions you can see one failed workflow and one workflow that is currently running. Now that that job is completed, you can check the GCP Console to see if new resources got successfully created.
