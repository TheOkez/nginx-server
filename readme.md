# Setting Up Docker Container on AWS EC2 Instance

## Step 1: Launch EC2 Instance

- From AWS, select the EC2 instance:
  - Give it a name and launch the instance.
  - Select a new or existing keypair file (.pem).
  - **Note:** Allow HTTP traffic from the internet.

## Step 2: SSH into the Instance

- On your terminal, navigate to the directory where the keypair was downloaded.
- Modify the permission of the keypair file:
  ```bash
  chmod 400 keypair-name.pem
ssh -i keypair-name.pem ec2-user@[ip-address]
```
- ssh -i keypair-name.pem ec2-user@[ip-address]

## Step 3: Update and Install Docker & Git
- sudo yum update -y
- sudo yum install -y docker git

## Step 4: Clone the Repository
- git clone [link to the git repo]

## Step 5: Start Docker Service
- sudo service docker start
- sudo chkconfig docker on
- sudo usermod -a -G docker ec2-user
- exit

## Step 6: Pull and Verify Docker Images
- ssh -i keypair-name.pem ec2-user@[ip-address]
- docker pull nginx
- docker pull httpd (optional)
- docker images

## Step 7: Run Docker Container
- For Nginx: ```docker run -d -p 80:80 --name [app-name] -v $(pwd)/[app-name]:/usr/share/nginx/html:ro nginx
```
- For Httpd(Optional): ```docker run -d -p 80:80 --name httpd-[app-name] -v $(pwd)/[app-name]:/usr/local/apache2/htdocs:ro httpd
```

## Note: Delete Existing Containers if on the same port
- Stop all containers: ```sudo docker stop $(sudo docker ps -aq)
```
- Remove all containers ``` sudo docker rm $(sudo docker ps -aq)
```
## Step 8: Access the Application
- Check the public IP address from the EC2 instance to see the app hosted.
