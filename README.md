# Deploying-Docker-Images-via-Docker-Hub

Docker Workflow: Build, Push to Docker Hub, and Run
1. Build Docker Image Locally
------------------------------------
For Frontend:
 docker build -t payroll-fe:25.7.6 --build-arg config=production .
2. Tag the Image
------------------------------------
Get the IMAGE ID from the result of the build command (e.g., 1b41687db3cd), then run:
 docker tag 1b41687db3cd mtesfa/payroll-fe:25.7.6
3. Push the Image to Docker Hub
------------------------------------
 docker push mtesfa/payroll-fe:25.7.6
4. On the Target Machine (e.g., 10.1.12.70)
------------------------------------
Make sure Docker is installed and you're logged into Docker Hub, then run:
 docker run -p 5003:80 -d --name payroll-fe mtesfa/payroll-fe:25.7.6
5. Optional: Explicitly Pull Before Running
------------------------------------
 docker pull mtesfa/payroll-fe:25.7.6
----------------------------------------------
Spring Boot Backend Workflow:
1. Build the Image
 docker build -t payroll_api:25.7.21 .
2. Tag the Image (e.g., c346909fff5d is the image ID)
 docker tag c346909fff5d mtesfa/payroll_api:25.7.21
3. Push the Image
 docker push mtesfa/payroll_api:25.7.21
4. Run on Target Machine
 docker run -p 5005:8080 -e SPRING_PROFILES_ACTIVE=live -d --name payroll_api
mtesfa/payroll_api:25.7.21
