This is a simple Flask application packaged in a Docker container. To run it on your computer, follow these steps:

1. Open your terminal and navigate to the project directory.
2. Run the following command to build the Docker container:
   ```
   docker-compose up --build
   ```

Once the container is running, you can view the application locally by visiting http://localhost:80 in your web browser. Flask runs inside the container on port 5000, but Docker Compose maps this to port 80 on your machine for easy access.

If your local machine and the EC2 instance have the same CPU architecture (x86 or ARM), you can proceed with these additional steps:

1. Build the Docker image locally by running this command from your project directory:
   ```
   docker build -t ec2-flask-demo:v1.0 .
   ```

2. To compress the Docker image before uploading it to the EC2 instance, save it as a tarball with this command:
   ```
   docker save -o ec2-flask-demo.tar ec2-flask-demo:v1.0
   ```

You'll find a `ec2-flask-demo.tar` file in your project directory after running this command.

3. Upload the tarball to your EC2 instance using `scp`. Use this command (replace `vs-kp-1.pem` with your PEM file and `3.142.211.164` with your EC2 instance's public IP):
   ```
   scp -i vs-kp-1.pem ec2-flask-demo.tar ec2-user@3.142.211.164:/home/ec2-user/docker_images
   ```

If you encounter permission errors with the PEM file, ensure it has the correct permissions by running:
   ```
   chmod 600 vs-kp-1.pem
   ```

The demo Docker image tar file is approximately 180 MB in size. You can verify its presence on the EC2 instance by running `ls` once you're logged in.

These steps will help you set up and deploy your Flask application using Docker, ensuring it runs smoothly both locally and on your EC2 instance.


