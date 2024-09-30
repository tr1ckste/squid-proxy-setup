## [Source](https://saturncloud.io/blog/how-to-install-dockercompose-on-amazon-ec2-linux-2-and-run-a-9kb-dockercompose-file/)

How to Install Docker-Compose on Amazon EC2 Linux 2 and Run a hello-world Docker-Compose File
=============================================================================================

In this tutorial, we’ll walk through the steps of installing Docker-Compose on an Amazon EC2 Linux 2 instance and running a hello-world Docker-Compose file. Docker-Compose is a tool for defining and managing multi-container Docker applications. It uses YAML files to configure the application’s services and allows you to manage the entire lifecycle of your application.

By **Saturn Cloud** | Tuesday, August 08, 2023 | [Miscellaneous](https://saturncloud.io/blog/categories/miscellaneous/) | Updated: Tuesday, January 02, 2024

![](/images/blog/how-to-blog4.webp)

#### Saturn Cloud provides customizable, ready-to-use cloud environments for collaborative data teams.

[Try Saturn Cloud](https://saturncloud.io/?utm_source=Blog+&utm_medium=Try&utm_campaign=Try) and join thousands of users moving to the cloud without  
having to switch tools.

Table of Contents[](#table-of-contents)
---------------------------------------

1.  [Connecting to your Amazon Linux EC2 instance](#1)
2.  [Installing Docker](#2)
3.  [Installing Docker-Compose](#3)
4.  [Running hello-world Docker-Compose File](#4)
5.  [Common Errors](#5)
6.  [Conclusion](#6)

Prerequisites[](#prerequisites)
-------------------------------

Ensure you have the following:

*   An [AWS](https://saturncloud.io/glossary/aws) account
*   An EC2 instance running

Connecting to your Amazon Linux EC2 instance[](#connecting-to-your-amazon-linux-ec2-instance)
---------------------------------------------------------------------------------------------

After creating your Amazon Linux EC2 instance on your AWS account and have it up and running, follow the steps below to connect to the instance from your local machine

1.  Open the terminal you prefer to use on your system
    
2.  Run the following command:
    
```
    ssh -i ~/.ssh/your-key-name.pem ubuntu@your-ec2-public-ip
```

Replace `your-key-name.pem` with the path to your private key file and `your-ec2-public-ip` with the public IPv4 address or DNS name of your EC2 instance.

3.  Enter your SSH key passphrase if prompted and then you should be connected to your EC2 instance. You should see a window that looks like this.

![1](/images/blog/how-to-install-dockercompose-on-amazon-ec2-linux-2-and-run-a-9kb-dockercompose-file1.png)

Installing Docker[](#installing-docker)
---------------------------------------

Before installing Docker-Compose, we need to install Docker. In your instance, run the following commands:

```
    sudo yum update -y
    sudo yum install -y docker
```

Start the Docker service:

    sudo service docker start
    

Add the `ec2-user` to the Docker group so you can execute Docker commands without using `sudo`:

```
    sudo usermod -a -G docker ec2-user
```  

Log out and log back in again to pick up the new Docker group permissions.

Installing Docker-Compose[](#installing-docker-compose)
-------------------------------------------------------

To install Docker-Compose, use the following commands:

    sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    

Next, set the permissions:

```
    sudo chmod +x /usr/local/bin/docker-compose
```

Verify the installation:
```
    docker-compose --version
```   

You should see the Docker-Compose version if the installation was successful.

Running hello-world Docker-Compose File[](#running-hello-world-docker-compose-file)
-----------------------------------------------------------------------------------

Now that Docker and Docker-Compose are installed, we can run a Docker-Compose file. In this case, we’re using the hello-world docker file.

For that we need to create a docker-compose.yml file that contains the following code:

```
    version: '3'
    services:
      web:
        image: hello-world:latest
        ports:
          - "80:80"
```

You can create this file locally and then transfer it to your EC2 instance using `scp` or any method you prefer. Alternatively, you can create the file directly in your EC2 instance. Once the file is on your EC2 instance, navigate to its location and run:
[← Back to Blog](/blog)
```
    docker-compose up
```

Docker-Compose will start all the services defined in your Docker-Compose file. You should see something like that:

![2](/images/blog/how-to-install-dockercompose-on-amazon-ec2-linux-2-and-run-a-9kb-dockercompose-file2.png)

Common Errors[](#common-errors)
-------------------------------

*   **Incorrect SSH key or path**: Ensure you’re using the correct private key file name and path in the ssh command.
    
*   **Docker service not starting**: Check if the Docker service is already running or if there are errors in the system logs.
    
*   **Syntax errors in docker-compose.yml**: Double-check the YAML syntax for indentation and missing characters.
    
*   **Image not found**: Confirm that the hello-world image is available in your Docker registry or repository.
    
*   **Port conflict**: Check for existing processes using port 80 and stop them before running the application.
    

#### Saturn Cloud provides customizable, ready-to-use cloud environments for collaborative data teams.

[Try Saturn Cloud](https://saturncloud.io/?utm_source=Blog+&utm_medium=Try&utm_campaign=Try) and join thousands of users moving to the cloud without  
having to switch tools.

Conclusion[](#conclusion)
-------------------------

Installing Docker-Compose on Amazon EC2 Linux 2 is straightforward. With Docker and Docker-Compose installed, you can define and manage multi-container Docker applications using a single YAML file. This makes it easier to manage complex applications and ensures that they run the same way, regardless of the environment.

Remember to always verify your installations by checking the version of the installed software. This can help you troubleshoot any issues that might arise during the installation process.
