Working with AWS Code Commit.

What is Code Commit?

AWS CodeCommit is a highly scalable, managed source control service that hosts private Git repositories. CodeCommit stores your data in Amazon S3 and Amazon DynamoDB giving your repositories high scalability, availability, and durability. You simply create a repository to store your code. There is no hardware to provision and scale or software to install, configure, and operate.

What you will learn thorugh this lab?
How to create a code repository using AWS CodeCommit via the Amazon Management Console
How to create a local code repository on the Linux instance using git
How to synchronize a local repository with an AWS CodeCommit repository

Task 1: Create an AWS CodeCommit repository

In this task, you use the AWS Management Console to create an AWS CodeCommit repository.
At the top of the AWS Management Console, in the search bar, search for and choose CodeCommit

On the AWS CodeCommit page, choose Create repository.

On the Create repository page:

For Repository name, enter: My-Repo

For Description enter: My first repository

Choose Create: An empty repository named My-Repo is created.

You should now be on the My-Repo page, which contains the details to connect to the repository.

Task 2: Connect to the Amazon EC2 instance
An Amazon EC2 instance has been created for you as part of the lab environment build process. In this task, you connect to the instance using AWS Systems Manager Session Manager.

Copy the Ec2InstanceSessionUrl value from the list to the left of these instructions, and then paste it into a new web browser tab.

Task 3: Create a local repository using Git
This task provides an example of how you would use AWS CodeCommit to synchronize to any local code repository that you might create in your normal production development environment.

sudo yum install -y git

Run the following commands to configure the Git credential helper with the AWS credential profile, and allow the Git credential helper to send the path to repositories:
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true

Next, obtain the HTTPS URL of your AWS CodeCommit repository.
Return to your web browser tab with the AWS CodeCommit console, which should be on the My-Repo page.
At the upper-right of the page, choose Clone URL , and then choose Clone HTTPS.

The repository URL is copied to your clipboard and should look similar to this: https://git-codecommit.us-east-1.amazonaws.com/v1/repos/My-Repo.
Return to your web browser tab with the terminal session.

 Run the following command to clone the My-Repo repository to the instance:
 Replace the CLONE_HTTPS_URL placeholder value with the Clone HTTPS URL that you copied previously.
 git clone CLONE_HTTPS_URL

The output should indicate that you are cloning the My-Repo repository, and that the repository is empty, similar to this:
Cloning into 'My-Repo'...
warning: You appear to have cloned an empty repository.


Task 4: Making a code change and first commit to the repo
Run the following command to change to the My-Repo directory:
cd ~/My-Repo

Run the following command to create two files in your local repo:
echo "Hello Earth how are you?" > earth.txt
echo "Heya!! Jupiter how are you doing?" > jupiter.txt

Run the following command to list the files in the current directory:
ls
The output should show the two files you created, similar to this:
earth.txt jupiter.txt

Run the following command to stage the changes in your local repo:
git add earth.txt jupiter.txt

Run the following command to view the status of your repo:
git status
The output should show the branch you are current working in (master) and that the two files are ready to be committed to the repository

Run the following command to commit the changes in your local repo:
git commit -m "Added  earth.txt and jupiter.txt"

The output displays a message stating that the name and email address of the committer were configured automatically. In a production environment, you would use the commands listed to set your name and email address, which are then applied to each commit you do. The output also shows that two files were changed and inserted.

Run the following command to view details about the commit you just made: 
git log


Task 5: Push your first commit
Run the following command to push your commit through the default remote name Git uses for your AWS CodeCommit repository (origin), from the default branch in your local repo (master):
git push -u origin master

After you have pushed code to your AWS CodeCommit repository, you can view the contents using the AWS CodeCommit console.

Return to your web browser tab with the AWS CodeCommit console, which should be on the My-Repo page.

Choose your web browser’s refresh button to refresh the page. The two files that you added to your repository should be displayed. Choose the link for each file to view its contents.

Congratulations! You have successfully pushed the changes from your local repository to the remote CodeCommit repository.






