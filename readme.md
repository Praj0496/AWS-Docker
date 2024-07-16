### This is a simple Flask application packaged in a Docker container. 

### Steps to copy your files to directory in your EC2 instance

1. Open your terminal: Ensure you are in the directory where your files are located that you want to copy to the EC2 instance.

2. Use scp command: The basic syntax for scp is:
```
scp -i /path/to/your/key.pem /path/to/local/file username@ec2-instance-ip:/path/to/destination/directory
```
Replace the placeholders with the following:

+ /path/to/your/key.pem: Path to your PEM file (key.pem).
+ /path/to/local/file: Path to the file or directory you want to copy from your local machine.
+ username: SSH username of your EC2 instance (ec2-user, ubuntu, etc.).
+ ec2-instance-ip: Public IP address or DNS name of your EC2 instance.
+ /path/to/destination/directory: Path on your EC2 instance where you want to copy the files.

Example:
```
scp -i ~/Downloads/key.pem ~/Documents/example.txt ec2-user@3.142.211.164:/home/ec2-user/files/
```

This command copies example.txt from your local machine (~/Documents/) to the files directory on your EC2 instance (/home/ec2-user/files/).

3. Confirm transfer: After executing the scp command, you might be prompted to confirm connecting to the EC2 instance (type yes if prompted).

4. Enter PEM file passphrase: If your PEM file is encrypted with a passphrase, you may need to enter it.

5. Check file transfer: Once the transfer completes without errors, you should see your file in the specified directory on your EC2 instance.

Additional Tips:

+ Ensure your PEM file (key.pem) has restrictive permissions (chmod 400 key.pem) to avoid permission issues.
+ If copying directories recursively, use the -r flag with scp: scp -i key.pem -r local_directory ec2-user@ec2-instance-ip:/remote_directory

## Steps to build and run the Docker container

1. Access your EC2 instance and Navigate to the project directory.
2. Run the following command to build the Docker container:
   ```
   sudo docker build -t <image_name>:<tag> .
   ```
3. To run a container in detached mode (in the background), you can use:
   ```
   docker run -id --name <container_name> -p 80:5000 <image_name>:<tag>
   ```
   + -p 80:5000: Publishes port 5000 from the container which is default port for Flask to port 80 on the host machine.

4. Once the container is running, you can view the application locally by visiting http://Instance-publicIP:80 in your web browser.
   + Flask runs inside the container on port 5000, but Docker Compose maps this to port 80 on your machine for easy access.

These steps will help you set up and deploy your Flask application using Docker, ensuring it runs smoothly on your EC2 instance.


