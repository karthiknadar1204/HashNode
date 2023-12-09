---
title: "Empowering Your Development Workflow: A Step-by-Step Guide to Building Your First CI/CD Pipeline in Jenkins with SonarQube and Docker Integration"
datePublished: Sat Dec 09 2023 09:25:21 GMT+0000 (Coordinated Universal Time)
cuid: clpxuojb5000108l8dl4tef4t
slug: empowering-your-development-workflow-a-step-by-step-guide-to-building-your-first-cicd-pipeline-in-jenkins-with-sonarqube-and-docker-integration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702113873051/14616d11-f828-4e70-a592-56c1191ae23a.png
tags: docker, aws, devops, jenkins, cicd, ci-cd

---

This blog aims to guide you through the creation of your inaugural CI/CD pipeline using Jenkins, seamlessly integrated with three AWS instances and fortified with indispensable tools such as SonarQube and Docker. This comprehensive guide will equip you with the knowledge and hands-on experience to set up a robust pipeline.

# Beginners advice

It took me a total of 20 builds to finally see my pipeline running smoothly. While it may seem daunting at first, I want to share my experience to encourage others to embark on a similar path. Don't be disheartened by initial setbacks; instead, view them as valuable learning opportunities. Each failed attempt was a step closer to success, troubleshooting issues, and gaining a deeper understanding of the intricacies involved.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702112745915/f5bbde6b-ff0e-4386-ad1e-399774e1b585.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702112753861/778699d1-1e5a-4965-b05f-22c3dc738118.png align="center")

# Pre-requisites

* motivation to learn something new.
    
* Download an HTML template from Google.
    

Navigate to [Free-css](https://www.free-css.com/) and download a free CSS template, extract it and create a new repository on Git Hub for the downloaded template.

1. ### Creating AWS instances
    

We will be integrating 2 tools into the Jenkins pipeline

* sonarqube
    
* Docker
    

In AWS we will log in as an IAM user and create 3 separate EC2 instances:

* One for Jenkins
    
* One for Sonarqube
    
* One for Docker
    

Follow these steps to launch the EC2 instances in AWS

1. ### In the AWS dashboard that appears after you have logged in as an IAM user, go to the search tab type EC2 and select the first outlined link.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701333577248/9ae7b48f-dd09-4419-a550-ae693935d7de.png align="center")

* Now click on the Launch instance button on the page
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701333709249/33f61e4e-89d0-4dec-8bfd-bcea0b8b6ae6.png align="center")

* Now apply the following configuration to the AWS EC2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701333848686/8161e4de-8890-4223-9080-09c5627091cc.png align="center")

select the instance type to be **<mark>t2.medium</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701333936452/6ee5a60b-863d-4d82-a7b9-0383fed347c2.png align="center")

now create a new key-pair

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334131229/c0f7d724-f71e-4940-9c1b-558c0327a553.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334140462/9229e92a-4491-4121-bf53-df58da173cdd.png align="center")

A key pair is essential for secure authentication and access control to your EC2 instances on AWS. We will be using this key pair to connect the EC2 instance to your own terminal on the local system and monitor it instead of opening the AWS console again and again.

A .pem file by the name **<mark>Jenkins-ssh-key.pem</mark>** is now added to the ***/downloads*** directory in your system

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334290977/bc61340c-5f44-4322-a75f-14bc20c39571.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334295336/77c6a9b5-e4af-4104-beff-3ddf74b96bca.png align="center")

1. ### Now click on Launch instance in the bottom-left corner.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334474620/2b3728aa-2f35-48e8-b55f-438f21a3e698.png align="center")

Access the newly launched instance by clicking on the view all instances on the bottom right corner.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334659590/708b554b-47b1-4d00-b94a-185dfe904726.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701334736238/a1a71676-487f-43df-8721-1faf0724a64d.png align="center")

1. ### Now create 2 more EC2 instances for Sonarqube and Docker each following the above steps, you can use the same key-value pair that you are using for Jenkins.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701335176584/643697df-f242-4b8f-8857-2f35e74a46d1.png align="center")

### The Status check may take some time to get updated, you can keep refreshing the page to confirm the Status check.

1. ### Connecting Jenkins instance to the terminal.
    

* click on the Instance ID
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701335468217/0b9b9556-f339-45f2-bb83-3dd75aa26592.png align="center")

* Copy the public IP address
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701335574216/2e3806cd-8d89-478c-8ad3-de199f870c08.png align="center")

* open your terminal, and write the following command to navigate to the downloads directory because the key-value pair is in this directory.
    

```bash
cd downloads
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701335737684/fac5ee34-344b-4a4d-8661-775f28349d30.png align="center")

* Type the following command to connect the terminal to the EC2 instance
    

```bash
ssh -i <name_of_key_value_pair>.pem ubuntu@<public_ipv4_address>
```

<mark>name_of_key_value_pair </mark> is the key-value pair that is present in the downloads directory downloaded when creating the instance.

<mark>public_ipv4_address </mark> is the address you copied by navigating to the Instance Id of the Jenkins EC2 instance.

You will get the following error on writing the command

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701336171580/d23ddfa4-d33c-4e4d-b12e-3e560ffb163e.png align="center")

This issue basically wants us to update the rules such that the instance can only be accessed by us and not by anyone else, we configured the permissions using the following command

```bash
chmod 400 <name_of_key_value_pair>.pem
```

Now again run the following command to connect the terminal to the EC2 instance, it should connect perfectly.

```bash
ssh -i <name_of_key_value_pair>.pem ubuntu@<public_ipv4_address>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701337218255/cbd2068b-3245-4fe2-8800-cea799497321.png align="center")

1. ### Type the following command in the terminal.
    

```bash
sudo apt update
```

1. ### Now in the browser navigate to [jenkins.io](http://jenkins.io)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701338105483/205ba48d-1a6c-4724-9cdb-d0b9e27acd84.png align="center")

* Navigate to Installing Jenkins and select Linux
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701338219689/78756d2e-cd6e-4929-8c4c-1abf3604185f.png align="center")

* Click on Debian/Ubuntu
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701338308434/98e3e6de-b59d-4df8-b32a-00b32bcfb8c3.png align="center")

* Paste the following command in the terminal
    

```bash
sudo apt install openjdk-17-jdk
```

```bash
java -version
```

* Select the LTS Bash command and paste it into the terminal
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701338403215/2abff4a7-3c8b-4bee-a2f4-5dad38f19dec.png align="center")

* Now the Jenkins server should be up and running, to confirm the same, run the following command.
    

```bash
sudo systemctl status jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339174651/093be852-b931-43e1-a3b5-c5a1fcd18eba.png align="center")

In case of any error, try running the following command

```bash
sudo systemctl start jenkins
```

1. Now we will update the security group of the Jenkins EC2 instance to be able to access Jenkins at port 8080 in our browser.
    

* Click on the Instance Id of Jenkins instance
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339540281/c52aa952-22d2-4c24-9908-14bb153f2c25.png align="center")

* Scroll down and click on Security.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339572090/3bf9530e-69fe-4d26-891a-e1a0e567e88b.png align="center")

* Now navigate to the link highlighted under security groups
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339626273/9661d3a2-0b2a-4e63-81f2-760e8a095ce4.png align="center")

* click on edit Inbound rules.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339658540/37fe0f9d-5585-4a46-9c4b-6236f9e3124a.png align="center")

* Add the following configuration to access the Jenkins server at port 8080.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701339747287/56deee52-0895-4531-9623-82fb6062de18.png align="center")

1. Now in the browser, type the following to navigate to the Jenkins server.
    

```bash
<public_ipv4_address>:8080
```

1. To get the administration password, type the following command in the terminal.
    

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340038624/6016993d-f140-4194-b568-c8b6170c479f.png align="center")

1. copy the password and paste it into the server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340174150/82a4a9d1-3264-4909-ab0f-0dfc500e13b5.png align="center")

1. Select Install suggested plugins.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340227487/a7a2431a-1125-463a-8cd8-170ec99a05cf.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340243768/e25e1081-32df-4903-b10e-19a2cfde5974.png align="center")

1. Fill in the credentials of the admin user
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340354015/17b5041f-8fad-4a7c-951a-59a139bddbbd.png align="center")

1. Now click on New Item in the top left corner
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340522746/a5c78f34-3048-4360-a5ed-b328c6d2fc76.png align="center")

* Give any name to the project, select it to be a Freestyle project and click ok
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340595973/27f2a4e5-f65b-495e-bf84-9c2ab201b323.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701340624427/fd8322d1-65b4-44a7-a0fd-6a196c9513e0.png align="center")

1. Scroll down to source-code-management and select git, now add the URL of the repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701341228486/ee0094c1-3e76-4bbf-925f-210e16106737.png align="center")

* update the branch to build to "main" because our repository code is on the main branch
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701341299155/4adff0b8-f247-4b2d-a6f5-a40251c8bf1c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701341304811/7c106b7f-2f10-4429-bc33-607ea334c130.png align="center")

1. Scroll down to Build Triggers and select the following
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701341764209/92be0b42-5867-41bc-bd43-3b74eb45a636.png align="center")

This is done to automatically trigger the pipeline every time there is a change in the repository. Now we have configured Jenkins to pull our code from GitHub.

1. Now configure the repository to push the code to Jenkins and activate the pipeline every time someone pushes code to the repository or submits a pull request.
    

* Go to Settings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701343438166/e66d4ca7-27eb-44dc-915f-62c48ea12297.png align="center")

* Select Webhooks on the left sidebar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701343523671/68e737b4-b051-495c-833b-6d289978c821.png align="center")

* Now in the payload URL add the following
    

```bash
<public_ipv4_address>:8080/github-webhook/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701345645271/0891437f-5ae5-4f84-8ccf-cd75e2883f03.png align="center")

* Select "Let me select individual events"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701345690599/d128fdbb-4054-4734-bd02-50748f3f8437.png align="center")

* select the following two options
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701345728963/48dfe4b4-f4b9-4c57-8b85-5bda9db988c4.png align="center")

This basically means that each time code is pushed to the repository or if someone submits a pull request, the pipe will automatically be pushed to Jenkins and the pipeline will be triggered.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701345841938/56cd0bcf-a082-494e-8574-d5c91dd12e2a.png align="center")

1. Now in the Jenkins server, click Build Now on the left sidebar
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346036789/6c042ec8-5996-4eea-8f8a-edb384fdbe4e.png align="center")
    

* Now if you get a similar console output, it means that the build was a success and the code is being successfully pulled from githuba nd the pipeline works perfect fine
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346140043/51b493a5-e513-48d3-9d58-6eb4dab644d9.png align="center")
    
    1. further test the pipeline, well will manually try creating files and adding them to the repository and if the build is triggered, then we can confirm that the pipeline works perfectly.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346602045/0f841149-6a03-4432-9805-dcc53b3c75ce.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346606732/2a4b7494-a1c4-4ce8-8835-7009510c2aa1.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346619226/60e6aaea-0327-4482-9461-aee19099f44a.png align="center")
    
* We here see that a second build was automated and was successful as well
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701346691382/84569851-19ac-41e8-b0fd-1906e94b86eb.png align="center")
    

Till here we have set up the Jenkins server and connected it with GitHub while automating the pipeline to get triggered every time someone pushes code to Git Hub or submits a pull request, now we will cointegrate Jenkins with Sonarqube.

1. Open a new terminal, in the AWS console, and click on the Instance Id of Sonarqube.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347107085/38210c62-f0a2-49f9-9eb9-834ea3419d1d.png align="center")

* Copy the public IPv4 address and type the following command in the new terminal.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347262198/08e8828d-faf3-47a7-b277-d2fbf3ce01f2.png align="center")

```bash
ssh -i <name_of_key_value_pair>.pem ubuntu@<public_ipv4_address>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347336710/82cf1f4c-ed3f-41b7-9347-a21166435b18.png align="center")

1. Update the name of the hostname in the two terminals so that we can easily differentiate between the two
    

* ```bash
        sudo hostnamectl set-hostname sonarqube
    ```
    
* ```bash
        /bin/bash
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347519352/aaac11cc-03bb-4e27-abb8-80d95ab906c9.png align="center")

* Do the same with Jenkins server
    

1. Now run the following command in the terminal connected to the sonarqube instance
    

```bash
sudo apt update
```

1. Install Java using the following command
    

```bash
sudo apt install openjdk-17-jdk
```

1. Now to install SonarQube, navigate to the following [Sonarqube](https://www.sonarsource.com/products/sonarqube/downloads/) link.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353081007/d40c8199-cf44-4071-827e-68caaa438e00.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353093760/a88f2e6d-f629-4bb7-8359-6a0a62542e02.png align="center")

1. Paste the following command in the SonarQube terminal
    

```bash
wget wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.3.0.82913.zip
```

1. Follow the series of steps
    

```bash
ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353115983/47c392a0-050f-4c15-8359-71be75df936c.png align="center")

```bash
sudo apt install unzip
```

```bash
unzip sonarqube-10.3.0.82913.zip
```

```bash
ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353329855/f668807d-8319-4b43-b34e-35be5659078c.png align="center")

```bash
cd sonarqube-10.3.0.82913
```

```bash
ls
cd bin
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353434550/96806280-649d-41cb-b381-6aa1129645c8.png align="center")

```bash
ls
cd linux-x86-64
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353538457/14241622-ba32-4a54-bf1b-556eb69b1e87.png align="center")

```bash
ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701353559403/c0acf0fd-0135-4b4a-8804-404c4790ef7d.png align="center")

1. To Run the Sonarqube server on the browser, run the following command.
    

```bash
./sonar.sh console
```

1. Allocate a port for SonarQube on the EC2 instance to access in the browser.
    

* Click on the Instance Id of the SonarQube service
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354053812/620c4a8c-24b8-48dd-bb35-0de99ef8d6ec.png align="center")

* Click on Security
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354090470/4dea0f54-6d08-42df-ae74-c19117b491bf.png align="center")

* Click on the highlighted under security groups
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354525525/29b74b6b-dcde-45bc-b447-e7d009c3a50a.png align="center")

* Click on Edit inbound rules
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354553144/389976cb-4069-4406-b733-90c66bb167c6.png align="center")

* Add the following configuration.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354597716/683e3415-fc34-4cc1-97b7-840b0145652c.png align="center")

1. Now paste the following command on the terminal
    

```bash
<public_IPv4_address>:9000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354779180/cc798291-5799-4078-9ab6-66b65aac4bc3.png align="center")

1. The default login and password of the Sonarube server is ***<mark>admin.</mark>***
    
2. Click on Create a local project
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701354970218/be0f4929-a3f3-4164-85ff-73a8460d9a7e.png align="center")

1. Fill in the details.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355054636/60e00946-c876-45e9-8ff7-7ac91e6c5aae.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355490077/744fd1b0-74cf-4985-b784-7bf9dbda550d.png align="center")

1. Select Analysis method as With Jenkins
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355547989/e6464b4b-c3ef-4611-988b-981693e30026.png align="center")

1. Select DevOps platform as GitHub
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355609507/f5b613df-3f47-47fc-975f-752aa3b1045f.png align="center")

1. Scroll to the end of the page and select the other.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355701480/36c7954a-bc65-429c-89a8-2ca5138d84cf.png align="center")

Save the two snippets that appear on selecting the other in a text file.

1. Click on Account in the top-right corner and go to MY ACCOUNT
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355862486/69762456-c0a4-449e-b3e1-b3dfe0634bb9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355870642/9f1ab5cc-2c67-4850-ba70-6059fe0c6a40.png align="center")

1. Go to security.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701355908669/4fb4a970-ace1-429f-88a3-2c741025bdb4.png align="center")

1. Fill in the details to generate a token and save it in a text file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701356273798/3568f12b-8009-42be-b2e8-0f94529829f3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701356066635/d958e6d6-991c-4e88-80c0-cb8d56cb8137.png align="center")

1. Now we need to install a couple of plugins, to do this, go to manage Jenkins and then to plugins
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701358427190/250e29f3-4952-40b5-b984-fd8114fcc143.png align="center")

* Install the following two plugins.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701358517058/e547451a-33cd-48e1-8ddd-c3eaa0d7af2f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701358525717/a5724e5a-0840-4e55-a341-0eea26dde826.png align="center")

1. Click on the pipeline on the dashboard and click on Configure on the left sidebar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359067670/a838882d-fc86-4b35-91bd-d73208730825.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359075108/869c7395-51fd-4918-b905-83d37473073f.png align="center")

1. Go to Build steps and select the following configuration i.e Execute AonarQube Scanner.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359155861/3baeb25e-8047-4a7d-b5d3-ec39806f0381.png align="center")

1. Go to manage Jenkins and then to the system.
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359245376/0ff3852a-a64d-47c4-bf6a-19f0389eb644.png align="center")
    
3. Scroll to SonarQube Servers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359456569/3d66ea61-bea5-460a-9d01-0d97378eb8ef.png align="center")

The server URL is basically the following

```bash
<public_ipv4_address>:9000
```

1. Click on Add. Follow the steps
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359854284/b10149d0-b78b-4b3a-b6e9-4770fd5218c4.png align="center")

The secret text is the token that we generated in SonarQube.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359865532/f263f154-5578-4fb7-9427-b0ff4e1584f9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701359936495/e44ddae4-c692-4c32-bcf8-9aa6600ffdac.png align="center")

1. Now Try to build the the pipeline again.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701360046808/78e2b100-2b68-4cba-a46f-fee26ca34fc6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701360052485/d4a0b158-3afa-4917-9110-2ce81b9c1a9a.png align="center")

Till this point, we have set up our Jenkins server and perfectly integrated it with SonarQube.  
Now we will push the image to the docker hub after the scanning of the code is successful.

1. Connect the Docker instance to our terminal by following steps 20,21
    
2. Run the following commands to install docker in the instance.
    

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

To test is Docker is installed correctly, run the following command.

```bash
sudo docker run hello-world
```

If the output is similar, the docker has been successfully installed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701417695862/2de53bb6-d191-401e-8fbe-1e89ba8f6625.png align="center")

1. Now in the terminal connected to te Jenkins server, run the following command.
    

```bash
sudo su jenkins
```

This command is used to switch to user to jenkins.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701417954442/7e360763-4f65-44d4-8066-7ea241df03cd.png align="center")

1. Now we will create an SSH connection between jenkins and docker.
    

* Write the following command in the jenkins terminal
    

```bash
ssh ubuntu@<public_IPv4_address_of_docker>
```

you'll get this error on running this command

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701418137660/ee4a1fc3-a6ae-4f8d-9e67-0bfbe382dc37.png align="center")

* To fix the above error, move to the terminal connected to docker and switch to the root user using the following command
    

```bash
sudo su
```

* Type the following bash snippet
    

```bash
nano /etc/ssh/sshd_config
```

* Now in the nano file,update the following
    

uncomment the <mark>pubkeyAuthentication yes</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701419174025/948024f8-9ba1-4d0a-92bf-875f977fd359.png align="center")

Scroll down and change <mark>PasswordAuthentication no</mark> TO <mark>PasswordAuthentication yes</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701419292853/ac34913d-c5f0-4ed5-bc69-68674ed739ad.png align="center")

1. Now run the following command in the docker terminal
    

```bash
passwd ubuntu
```

set anything as you wish, make sure to save it, this password will be used when creating the SSH connection between jenkins server and docker server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701419422752/c61a57e3-8ed3-4f41-826e-2349ac8a313c.png align="center")

1. Now again try running the following command. to connect jenkins server to docker server
    

```bash
ssh ubuntu@<public_IPv4_address_of_docker>
```

Enter the password you you created in the docker server in step 48

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701419698111/55b31eaa-6b81-411f-be2e-213e3bfad7a4.png align="center")

Now jenkins server can access the docker server and push code as well.

1. Now enter the following command in the jenkins terminal connected to docker i.e the terminal we worked with in step 49.
    

```bash
ssh-keygen
```

Click enter for all the inputs, no special need to fill in anything.

The `ssh-keygen` command is used to generate a pair of authentication keys for secure SSH communication. The key pair consists of a private key and a public key.

The purpose of generating an SSH key pair is to establish a secure and passwordless connection between your local machine and a remote server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701419912545/acd58be4-e18f-44a8-822b-96a1a515e45e.png align="center")

1. Now exit the docker server we connected to in the jenkins terminal by running the ***<mark>exit</mark>*** command.
    
2. Now generate an SSH key for jenkins
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701420027026/dd818608-7243-48c8-aa10-5a478078d68f.png align="center")

1. Now we have established a passwordless connection between the jenkins server and docker server,run the following command to confirm the connection.
    

```bash
ssh ubuntu@<public_IPv4_address_of_docker>
```

You should be able to access the docker server from the jenkins server without any pssword authentication successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701420544889/ddd7c249-4e76-4f65-851e-93f634ba01fb.png align="center")

1. Now move to the Jenkins server we have opened in our browser and follow the steps.
    

* Go to manage Jenkins
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701421297952/4476770b-ef7a-4788-80a7-2f8a975ed0bd.png align="center")

* Under System Configuration, go to System
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701421332848/a71e5299-5135-4f79-b736-84e9c86334f8.png align="center")

* Scroll down to Server Groups Center and click Add
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701421394544/81dec77f-7375-45c1-8f7f-00b10e207a76.png align="center")

* Fill up the details as follows
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701421423960/ab101da9-dcc6-4b4b-9503-ee06da0fe8ef.png align="center")

The password here is the one you generated in step 48

Save these changes

* Now again to go manage Jenkins and System, scroll down to Server List
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701425759670/991fb444-6684-4d77-969f-15509953c129.png align="center")

The Server IP is the public IPv4 address of the docker instance

* Now go to the pipeline and click on configure on the left sidebar
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701425832301/29cd4208-1d12-47f5-a28b-62a0914ee890.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701425837491/89ae6fc6-24ae-4f7b-bff6-c8b0cd9ca691.png align="center")
    

Under the build steps dropdown, select Remote shell

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701425971990/4a2b6bc8-78e7-4454-9f61-e33357ae4efe.png align="center")

Now save the changes and run the pipeline.

If the build is successful, a new file is created in docker.

1. Create a Dockerfile
    

```bash
FROM nginx
COPY . ./usr/share/nginx/html
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701426206438/8eaa0d6d-f57d-49e1-8e6e-8cc61c35e9b5.png align="center")

Pushing the changes to the repository will again trigger the pipeline.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701426375220/8731707e-9f8a-46da-9b11-1bb4d2b7a4e6.png align="center")

1. Now in the terminal that is connected to the docker instance, create a new directory.
    

```bash
mkdir website
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701426518793/cdf3120b-4376-49e0-b8b8-c9017509320f.png align="center")

1. Now in Jenkins, go to the pipeline, configure and in the build steps section, delete the remote shell
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701427948270/9f4c4938-d8a9-4b05-a669-f5e350ad3b28.png align="center")

1. Now switch to execute shell
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701427967980/78b09105-8887-4f36-ae9c-b9c8e9beebd9.png align="center")

```bash
scp -r ./* ubuntu@<public_IPv4_address_of_docker>:~/website
```

In the above step, we are moving all the code from Jenkins to the directory we created in step 56 inside of docker.

1. Now we will build the image and Run the container for it.
    

* Go to the pipeline, configure and scroll down to build steps and add a new remote shell
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701429962296/0fbda9c8-a821-49ad-8a34-84b230fdc9d3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701429967805/885a2937-ac11-490a-b6ab-51f0af4b69d6.png align="center")

```bash
cd /home/ubuntu/website
docker build -t mywebsite .
docker run -d -p 8085:80 --name=websiteScan mywebsite
```

apply and save these changes.

* In the terminal connected to the docker instance, run the following commands
    

```bash
sudo usermod -aG docker ubuntu
newgrp docker
```

1. Now the pipeline is ready, now to access the site at port 8085 on our web browser, we have to configure the instance on the AWS console
    

* In the EC2 console, click on the Instance ID of the docker.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701430448589/23590587-4cb8-4702-92cc-113a299028d2.png align="center")

* Navigate to security
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701430465613/f284bfa4-48c2-4b5e-a7ed-9ec6a9ea6b14.png align="center")

* Edit inbound rules according to the following configuration.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701430541658/892fc837-5cb3-44bd-95f1-de8928568e6b.png align="center")

1. Now run the pipeline, the pipeline should run perfectly and you should be able to access the site on port 8085.
    

# Conclusion

Congratulations on reaching the end of this blog! Setting up a Jenkins pipeline can be a challenging but rewarding endeavour. Through my own experience of encountering and overcoming obstacles in 20 builds; Here's to your success in mastering Jenkins pipelines and building a resilient and efficient CI/CD workflow!

You can further follow my work on [Twitter](https://twitter.com/Karthikreincar1), I regularly share posts related to DevOps.