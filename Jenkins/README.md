**Jenkins pipelines**

- https://www.cprime.com/resources/blog/how-to-integrate-jenkins-github/

## Creating jenkins server

Creating a Jenkins CI/CD pipeline involves several steps, including setting up Jenkins, creating a Jenkinsfile for your pipeline, and configuring the Jenkins job. Below is a step-by-step guide to help you create a Jenkins CI/CD pipeline.

### Step 1: Set Up Jenkins
Install Jenkins:

Download Jenkins from the official Jenkins website.
Follow the installation instructions for your operating system.
Start Jenkins:

Start the Jenkins service on your system. Typically, you can access Jenkins at http://localhost:8080.
Unlock Jenkins:

When you first start Jenkins, it will prompt you to unlock it using an initial admin password found in the jenkins.log file.
Install Suggested Plugins:

Jenkins will recommend plugins to install. Install the suggested plugins for a typical setup.
Create an Admin User:

Follow the prompts to create an admin user.
### Step 2: Create a Jenkinsfile
The Jenkinsfile is a text file that contains the definition of the Jenkins pipeline. Here’s an example of a simple Jenkins pipeline:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add build steps here, e.g., compile your code
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add testing steps here, e.g., run unit tests
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add deployment steps here, e.g., deploy to a server
            }
        }
    }
}
```
### Step 3: Add Your Project to Jenkins
Create a New Job:

In Jenkins, click on New Item.
Enter a name for your job, select Pipeline, and click OK.
Configure the Pipeline:

In the job configuration page, scroll down to the Pipeline section.
Select Pipeline script from SCM if your Jenkinsfile is stored in a version control system like Git. Otherwise, you can enter the pipeline script directly in the Pipeline script text box.
Example configuration for Pipeline script from SCM:

SCM: Git
Repository URL: https://github.com/your-repo.git
Script Path: Jenkinsfile

### Step 4: Run the Pipeline
Save and Build:

Save your job configuration.
Click Build Now to run the pipeline.
Monitor the Pipeline:

Jenkins will execute the stages defined in your Jenkinsfile.
You can monitor the progress and results of each stage in the Jenkins dashboard.
Example Jenkinsfile for a Node.js Project
Here’s a more detailed example for a Node.js project:


```groovy
pipeline {
    agent any

    environment {
        NODE_HOME = tool 'NodeJS' // Assumes you've configured NodeJS in Jenkins tools
        PATH = "$NODE_HOME/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                // Add deployment steps, e.g., upload artifacts or deploy to a server
                echo 'Deploying...'
            }
        }
    }
}
```
### Additional Tips
Credentials: If your Git repository requires authentication, you can configure credentials in Jenkins and use them in the Pipeline script from SCM section.
Plugins: Install necessary plugins based on your project requirements (e.g., Git plugin, NodeJS plugin, Docker plugin, etc.).
Pipeline Libraries: For more complex pipelines, you can use shared libraries to encapsulate reusable pipeline code.
This setup will help you create a basic CI/CD pipeline using Jenkins. You can extend and customize it based on your project's specific needs.   