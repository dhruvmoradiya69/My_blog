---
title: "Day 22: Getting Started with Jenkins! 😃"
datePublished: Sun Oct 27 2024 15:05:58 GMT+0000 (Coordinated Universal Time)
cuid: cm2rq2pp000020amfeg1tdqos
slug: day-22-getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730038808054/f3b1af50-8093-48c0-b855-6bb01ea549cd.png
tags: devops, jenkins, aws-ec2, 90daysofdevops, jenkins-installation

---

Hello DevOps enthusiasts! 🌟 Today, we're diving into Jenkins, the powerful CI/CD tool that helps automate all those repetitive tasks in the software development lifecycle. Imagine never having to manually check if a code test passed or if your app deployed successfully. Jenkins does this for you and more! So let's jump in and explore how Jenkins works, why it’s essential, and how you can start using it today. 🚀

---

### 🌐 What is Jenkins?

Jenkins is an open-source tool that automates tasks in the DevOps lifecycle, specifically Continuous Integration (CI) and Continuous Deployment (CD). It’s written in Java, and as an open-source server, it allows developers to build, test, and deploy software automatically. 🛠️ This tool works like a conductor in an orchestra, ensuring that every part of the process flows smoothly from one stage to the next.

In simpler terms, Jenkins helps you:

1. **Build** 🏗️ - Compile code automatically.
    
2. **Test** ✅ - Run automated tests to check code quality.
    
3. **Deploy** 🚀 - Move code to staging or production environments seamlessly.
    

Imagine working with multiple developers on a project. Without automation, you'd have to manually verify each piece of code, test it, and then move it to production. But Jenkins does this all with just a few clicks, or even automatically on a schedule. Isn't that amazing? 🤩

---

### 💡 Why Jenkins?

In today's fast-paced tech world, automation is no longer a luxury but a necessity. Here’s why Jenkins is invaluable:

1. **Time-saving** ⏳: Jenkins automates repetitive tasks, letting developers focus on actual coding.
    
2. **Consistency** 🔄: No more "it works on my machine" issues! Jenkins makes sure the code works as expected every time.
    
3. **Effortless collaboration** 🤝: Multiple team members can see real-time updates, test results, and logs, making it easier to work together.
    
4. **Reliable deployment** 📈: Jenkins ensures smooth deployments, reducing the chances of errors when moving code to production.
    

Think of Jenkins as your software project’s personal assistant, constantly monitoring and executing tasks without needing breaks. 😴 Whether you’re integrating Git, Docker, or other tools, Jenkins has plugins that make automation possible for each stage of DevOps.

---

## 🛠️ Installing Jenkins on Ubuntu: Step-by-Step Guide 🖥️

### Step 1: Update Your System 🆙

It’s always a good idea to start with updating the system package list to make sure all available packages are up-to-date.

```bash
sudo apt-get update
```

### Step 2: Install Java 17 ☕

Jenkins requires Java to run, and we’ll be using OpenJDK 17. Run the following commands:

```bash
sudo apt-get install fontconfig openjdk-17-jre
```

**Verify Java installation** by checking the version:

```java
java -version
```

Expected output:

```java
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```

This confirms Java is installed correctly and is ready to support Jenkins.

### Step 3: Add the Jenkins Repository 🔗

Since Jenkins is not in the default Ubuntu repositories, we’ll need to add the official Jenkins repository.

1. **Download the Jenkins key** and save it to your keyring:
    
    ```bash
    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    ```
    
2. **Add the Jenkins repository** to your system:
    
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```
    

### Step 4: Update the Package List Again 📦

After adding the Jenkins repository, refresh the package list to include Jenkins:

```bash
sudo apt-get update
```

### Step 5: Install Jenkins 🚀

Now, install Jenkins using the following command:

```bash
sudo apt-get install jenkins
```

This command will install Jenkins along with its necessary dependencies.

---

### Step 6: Start and Enable Jenkins 🔄

1. **Start Jenkins** to ensure it’s running:
    
    ```bash
    sudo systemctl start jenkin
    ```
    
2. **Enable Jenkins** to automatically start on system boot:
    
    ```bash
    sudo systemctl enable jenkins
    ```
    

---

### Step 7: Check Jenkins Status ✅

To confirm Jenkins is running properly, check its status with:

```bash
sudo systemctl status jenkins
```

If Jenkins is running correctly, you should see the status `active (running)`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730039339616/d4f47c1a-7fb9-4dc6-a1cf-f543db3b91ab.png align="center")

---

### Step 8: Access Jenkins in Your Browser 🌐

Once Jenkins is running, you can access its web interface:

1. **Open a browser** and go to:
    
    ```yaml
    http://localhost:8080
    ```
    
    (If you’re accessing Jenkins remotely, replace [`localhost`](http://localhost) with your server’s IP address.)
    
2. **Unlock Jenkins**:
    
    * The first time you access Jenkins, it will ask for an **Admin Password**.
        
    * To find this password, run:
        
        ```bash
        sudo cat /var/lib/jenkins/secrets/initialAdminPassword
        ```
        
    * Copy the password and paste it into the Jenkins setup screen.
        
3. **Customize Jenkins**:
    
    * Follow the on-screen instructions to install suggested plugins and set up your first admin user.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730039566059/99019ddd-f9b5-4254-9d29-897b4287d62f.png align="center")

---

### Checking Jenkins Version 🎉

To confirm Jenkins was installed correctly, you can check its version. Although Jenkins doesn’t have a direct version command, you can verify it with:

```bash
dpkg -l | grep jenkins
```

This will display the version number of Jenkins installed on your machine.

---

### 🚀 Task 1: What Makes Jenkins So Essential? (In Your Words)

Jenkins plays a critical role in the DevOps lifecycle. Here’s a closer look at how it integrates and its benefits:

* **Continuous Integration**: With Jenkins, new code is automatically tested as soon as it’s pushed to a shared repository (like GitHub). Jenkins runs the tests, letting you know immediately if there’s an issue.
    
* **Continuous Delivery**: Once the code passes all tests, Jenkins helps deploy it to a staging environment. This allows developers to continuously release features to testers or users, resulting in faster feedback.
    
* **Continuous Deployment**: Taking it one step further, Jenkins can deploy your code directly to production if needed, making your release cycles faster and more reliable.
    

In essence, Jenkins becomes the backbone of the automation pipeline, taking care of builds, tests, and deployments so you can focus on innovation! 💡

---

### 🛠️ Task 2: Create a Freestyle Pipeline to Print "Hello World" 🌍

This task will get you familiar with Jenkins basics and how to create automated workflows (or jobs). Let’s dive into each step!

---

### Step 1: Open Jenkins Dashboard and Start a New Project 🖥️

#### Access the Jenkins Dashboard

1. **Log In**: Go to your Jenkins URL (often [`http://localhost:8080`](http://localhost:8080) if you’re running it locally) and log in with your credentials.
    
2. **Navigate to “New Item”**:
    
    * On the dashboard, look for a menu option that says **New Item**. This is where we start our journey to creating a new Jenkins project.
        

#### Creating a New Project

1. **Project Name**:
    
    * Enter a unique name for your project. For our example, let’s use `HelloWorldPipeline`.
        
2. **Choose Project Type**:
    
    * Select **Freestyle project**. This option is best for beginners, allowing you to customize build steps without needing advanced configurations.
        
3. **Click OK**:
    
    * After entering the name and selecting **Freestyle project**, click the **OK** button to create the project.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730039836123/c4c901f0-0c01-4a29-89e9-4221541275a1.png align="center")

Great! Now we have a blank project ready for configuration. 🎉

---

### Step 2: Configure the Freestyle Project 🔧

Now, we’ll configure what this project will do, including our specific tasks.

#### Adding Build Steps

Build steps are the actions Jenkins performs whenever it runs this job. Let’s add each task as a separate build step.

1. **Task 1: Print “Hello World”** 🌍
    
    * In the project configuration page, scroll down to the **Build** section.
        
    * Click on **Add build step** and choose **Execute shell**. This opens a command box.
        
    * In the command box, type the following command:
        
        ```bash
        echo "Hello World"
        ```
        
    * This command will print “Hello World” to the job output, helping you confirm that Jenkins can execute simple shell commands.
        
2. **Task 2: Print the Current Date and Time** 📅
    
    * Add another build step under **Execute shell**.
        
    * In this new command box, enter the following command:
        
        ```bash
        date
        ```
        
    * The `date` command will display the current date and time. This is useful for logging when each job ran, making it easy to track if Jenkins is executing jobs on schedule.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730040196489/ab66e8df-1b96-4d9b-8bcd-1f081fb1ef74.png align="center")

1. **Task 3: Clone a GitHub Repository and List Its Contents** 📂
    
    * Add another **Execute shell** build step to clone a GitHub repository.
        
    * In the command box, type:
        
        ```bash
        git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
        ```
        
    * Replace `YOUR_USERNAME` and `YOUR_REPOSITORY` with your actual GitHub username and repository name.
        
        * **Note**: Jenkins needs to have Git installed on the server for this to work. You can check if Git is installed by running `git --version` in your terminal.
            
    * After cloning the repository, let’s list its contents to verify everything was downloaded successfully. Add this command right below the `git clone` line:
        
        ```bash
        ls YOUR_REPOSITORY
        ```
        
        * Replace `YOUR_REPOSITORY` with your repository’s actual folder name.
            
        * The `ls` command lists all files and folders within the repository, helping us confirm that the clone was successful.
            

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730040851115/2870c687-a488-41ba-a094-1b0acc2e8852.png align="center")

Your Freestyle job now has three basic tasks: printing text, displaying the current time, and cloning a repository. Let’s move on to scheduling! ⏰

---

### Step 3: Set a Build Schedule ⏱️

Let’s automate this pipeline to run periodically. Here’s how you set up a schedule:

1. Scroll to the **Build Triggers** section in your project’s configuration page.
    
2. **Enable Periodic Builds**:
    
    * Check the **Build periodically** option.
        
3. **Define the Schedule**:
    
    * In the text box, enter `H * * * *`. This setting tells Jenkins to run the job every hour at a random minute (to avoid all jobs starting at the exact same time across servers).
        
    * The format follows the *cron* syntax: `Minute Hour Day Month Day-of-week`.
        
        * Here, `H` represents any random minute, and `*` stands for every hour, day, month, and day of the week.
            

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730041245278/1a7f2a4a-d8ae-4b9b-8e08-aaa2db30133c.png align="center")

💡 **Tip**: You can customize this schedule if you prefer, but for this example, an hourly schedule helps to automate regularly.

---

### Step 4: Save and Run the Pipeline 🎬

Now that everything is set up, let’s save the project and do a test run.

1. **Save the Configuration**:
    
    * At the bottom of the configuration page, click the **Save** button. This saves all your settings.
        
2. **Run the Job**:
    
    * On the project’s main page, click **Build Now**. This will trigger the job to run immediately so we can confirm everything works correctly.
        
3. **Check the Console Output**:
    
    * To see the results, click on the latest build under **Build History** on the left side of the project page.
        
    * Click **Console Output** to view the step-by-step output from the build.
        

You should see:

* “Hello World” printed in the console.
    
* The current date and time.
    
* A list of files from your GitHub repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730041395824/959e8a03-c136-4833-bf6d-0ee2420cf255.png align="center")

If everything is in order, congratulations! 🎉 You’ve just built your first Jenkins job.

---

### 🔄 Bonus: Customizing and Expanding the Pipeline

Now that you’re comfortable with creating simple tasks in Jenkins, you can expand your job to add more complex workflows:

* **Additional Commands**: Try adding commands that perform more actions, like file manipulation or email notifications.
    
* **Integrate with Docker**: Jenkins has a plugin to work directly with Docker, making it easy to deploy containers.
    
* **Slack or Email Notifications**: Add notifications to alert you when the job finishes or fails.
    

With each improvement, Jenkins can become more powerful, managing complex tasks that save you time and help your team release code confidently.

---

### Wrapping Up 🎉

In this guide, you learned how to set up a basic Jenkins Freestyle Pipeline that automates a series of tasks. Jenkins is a great tool for simplifying repetitive tasks in development and deployment, and with this foundation, you’re ready to start exploring more advanced features.

Happy Jenkins-ing! 😄