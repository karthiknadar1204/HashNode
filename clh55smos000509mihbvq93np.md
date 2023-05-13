---
title: "Linux 101: Getting Started with the Open-Source OS"
datePublished: Mon May 01 2023 18:13:30 GMT+0000 (Coordinated Universal Time)
cuid: clh55smos000509mihbvq93np
slug: linux-101-getting-started-with-the-open-source-os
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682964249295/79e9b8dc-e8f2-41a3-b8d6-4c6c3c2ec097.png
tags: linux

---

In this article, we will dive into the world of Linux, exploring its architecture, real-world applications, and why it has become the go-to OS for DevOps professionals. Whether you are a beginner looking to learn the basics or an experienced user seeking to deepen your knowledge, this article will provide you with a concise overview of Linux and its key features. Additionally, we will introduce you to a series of essential Linux CLI commands to help you get started with using the OS like a pro. So, let's begin our journey into the world of Linux!

### What is an operating system?

An operating system (OS) is a software program that acts as an intermediary between computer hardware and software applications. It is responsible for managing and coordinating various system resources, such as memory, processing power, input/output devices, and network connectivity, to ensure that applications can run efficiently and effectively.

The main functions of an operating system include providing a user interface for interacting with the computer, managing and allocating system resources to different applications, providing security and protection to the system, facilitating communication between hardware devices and software programs, and controlling the execution of various processes and tasks.

### what is Linux?

Linux is a free and open-source operating system kernel. It was created by Linus Torvalds in the early 1990s. There are many different distributions, or "distros," of Linux available, each with its own set of features and tools. Some popular examples include Ubuntu, Debian, Fedora, CentOS, and Red Hat Enterprise Linux.

Linux distributions, or "distros" for short, are different versions of the Linux operating system that are built around the same Linux kernel but vary in terms of the software packages, applications, and configuration options that are included.

Linux has over the years become a popular choice for servers, supercomputers, embedded systems, and mobile devices. Linux provides a flexible, customizable environment that is widely used in software development and DevOps.

### Why Linux?

Linux plays a critical role in DevOps by providing a stable and reliable platform for developing, deploying, and managing software applications. Here are some ways in which Linux is used in DevOps:

1. Configuration management: Many DevOps teams use configuration management tools such as Ansible, Chef, or Puppet to automate the deployment and configuration of software applications. These tools are typically run on Linux servers and rely on Linux's stability and reliability to ensure that deployments are consistent and error-free.
    
2. Containerization: Containers are a lightweight and portable way of packaging and deploying software applications. Linux is the most widely used operating system for running containers, and many container orchestration tools such as Kubernetes, Docker Swarm, and OpenShift are built on top of Linux.
    
3. Continuous integration and delivery (CI/CD): CI/CD is a process of automating the building, testing, and deployment of software applications. Many of the tools used in CI/CD, such as Jenkins, GitLab, and Travis CI, are built on top of Linux and rely on its stability and reliability to ensure that deployments are consistent and error-free.
    
4. Cloud computing: Many DevOps teams use cloud computing platforms such as Amazon Web Services (AWS), Microsoft Azure, or Google Cloud Platform to deploy and manage their applications. These platforms typically rely on Linux servers to provide the underlying infrastructure and to run the virtual machines or containers that host the applications.
    
5. Security: Linux is known for its robust security features, which make it a popular choice for DevOps engineers. With Linux, DevOps engineers can configure and secure their systems to protect against security threats and vulnerabilities.
    
6. Command line interface (CLI): Linux's CLI is highly powerful and flexible, which makes it ideal for automation and scripting tasks. The CLI provides DevOps engineers with greater control over the system, enabling them to perform complex tasks with ease.
    

Overall, Linux's flexibility, customization options, powerful CLI, package management tools, containerization technologies, and security features make it an essential operating system for DevOps engineers.

### Linux Architecture

Linux architecture consists of a kernel that interacts with the hardware of a computer and a shell that serves as an interface between the user and the kernel.

A kernel is the core component of an operating system that acts as a bridge between the software applications and the hardware components of a computer. It is responsible for managing system resources, providing a secure environment for applications to run in, and controlling the execution of programs.

In Linux, a shell is a program that provides a command-line interface (CLI) for interacting with the operating system. The shell acts as an intermediary between the user and the operating system kernel, allowing users to issue commands and run programs. The shell is often referred to as a command-line interpreter (CLI) because it interprets the commands entered by the user and executes them. It provides a text-based interface that allows users to interact with the operating system using a series of commands and arguments.

### Linux Commands

1. mkdir: makes a new directory/folder.
    
2. cd: changes the directory/folder.
    
3. ls: List files and directories in the current directory.
    
4. pwd: Print working directory.
    
5. cp: Copy a file or directory.
    
6. mv: Move or rename a file or directory.
    
7. rm: Remove a file or directory.
    
8. cat: Display the contents of a file in a directory.
    
9. grep: Search for a pattern in a file like files with a specific extension.
    
10. ps: Display a list of currently running processes.
    
11. clear: To clear the terminal screen.
    
12. echo any\_content &gt; file\_name : this command adds “any\_content” to the file “file\_name”.
    
13. touch: creates a new file in a given directory.
    
14. sudo: allows a permitted user to execute a command as the superuser or another user, as specified by the security policy. The utility provides an efficient way to temporarily grant users or user groups privileged access to system resources so that they can run commands that they cannot run under their regular accounts.
    
15. date: Display time and date.
    
16. history: List previously used commands.
    
17. whoami: Display the current login user name.
    

## Files and Directory

1. Creating a Directory
    
    ```plaintext
    mkdir directory_name
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682672357144/6c6a44d7-6dc7-4f0b-b7e4-e9801657dae3.png align="left")

1. Creating multiple folders in a directory
    
    ```plaintext
    mkdir folder_one_name folder_two_name
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682957312802/166fc886-f7b2-4d54-9cd7-77fcc6d8361e.png align="left")

1. Creating nested directory
    
    ```plaintext
    mkdir -p parent_directory/child_directory
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682957748834/8e90a024-3806-40db-a2ba-64666ad49351.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682957766684/a466f112-94cc-4417-bcf9-e04322eafe3a.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682957772888/989e4507-a34b-40a6-8b5d-683cf4c0261b.png align="left")

1. Create a file
    
    ```plaintext
    touch file_name
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682958073700/114af986-c993-4d9e-b342-93166b93df40.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682958078341/ee4b41b9-7376-4b35-bd14-c97d20c229ec.png align="center")

1. copy files
    
    ```plaintext
    cp Src_file Dest_file 
    ```
    
    If the command contains two file names, then it copies the contents of **1st file** to the **2nd file**. If the 2nd file doesn’t exist, then first it creates one, and content is copied to it. But if it existed then it is simply overwritten without any warning. So be careful when you choose the destination file name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682959068072/80b03f01-67b8-4f22-bf9c-659ae398f498.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682959092296/56f7647c-de6b-4e99-87a1-7a7d52098f7d.png align="left")

1. copy directories
    
    If the command contains two directory names, **cp** copies all files of the source directory to the destination directory, creating any files or directories needed. This mode of operation requires an additional option, typically **R**, to indicate the recursive copying of directories.
    
    In the command below **cp** behavior depends upon whether *Dest\_directory* exists or not. If the *Dest\_directory* doesn’t exist, cp creates it and copies content of *Src\_directory* recursively as it is. But if Dest\_directory exists then copy of *Src\_directory* becomes sub-directory under *Dest\_directory*.
    

```plaintext
cp -R Src_directory Dest_directory
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682959797171/edcf3742-f993-4b76-9ce0-d38b337db73b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682959803676/00e63d0f-2bd7-4a3d-9b7a-73adeda4e9d3.png align="center")

1. Remove a File
    
    ```plaintext
    rm file_name
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682961304761/68906468-17d3-470c-aedb-7d5a0154d5ff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682961280034/9a6aa24f-5125-41d2-b786-d100e5a231b5.png align="center")

1. Remove a Directory
    
    ```plaintext
    rm file_name
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682961419803/1626d5b0-c793-4202-be48-50cee77ca091.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682961425171/e09e8730-f016-4fec-b59b-5f9d7c1ce2cb.png align="center")

## Grep

What does **grep** command do?

This command is used to search for a specific pattern or string within a file or multiple files. It is case-sensitive.

* grep “ content ” file\_name -&gt; searches for the “content” in file\_name and prints it if it exists.
    
* grep -n “content” file\_name-&gt;shows the line number in which the content exists.
    
* grep -w “content” file\_name -&gt;prints content if it’s a complete word.
    
* grep "content" file1 file2-&gt;Searches for content in file1 and file2 and prints the matching line.
    
* grep -i "content" file1-&gt;Search for pattern ignoring the case-sensitivity in file1 .
    
* grep -v "content" file1-&gt;Searches for lines in file1 that do not contain the "content".
    

## Find

What does **find** command do?

This command is used to search for files in a directory hierarchy based on various criteria, such as name, size, type, modification time, etc. It can be used to locate files based on a variety of search criteria.

* find .-&gt;displays all the files and folders of the current directory.
    
* find ..-&gt;displays all the files, directories and images in the previous directory.
    
* find folder\_name-&gt;displays all the files and images present in folder\_name.
    
* find .-type -d-&gt;display all the folders in the given directory.
    
* find .-type -f-&gt; display all the files in the given directory.
    
* find .-type -f -name “file\_name”-&gt;displays the file\_name existing inside the directory.
    
* find .-type -f -mmin -20-&gt;displays all the files that were modified less than 20mins ago.
    
* find .-type -f -mmin +15-&gt; displays all the files that were modified more than 15mins ago.
    

## Conclusion

In conclusion, Linux commands offer a wide range of powerful tools and utilities that can help users efficiently manage their systems and perform a variety of tasks. From simple operations like file management and text editing to more complex tasks such as network administration and system monitoring, Linux commands provide a flexible and versatile way to interact with the operating system. By mastering these commands, users can gain a deeper understanding of the inner workings of their Linux system and become more productive in their day-to-day tasks. Whether you're a seasoned Linux user or just getting started, taking the time to learn some basic Linux commands can be a worthwhile investment in your technical skills and knowledge.