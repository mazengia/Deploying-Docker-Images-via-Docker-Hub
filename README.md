 
#  Docker Workflow: Build, Push, and Run

This guide explains how to build Docker images for the **Frontend (Angular)** and **Backend (Spring Boot)**, push them to Docker Hub, and run them on a target server.

---

# 📦 Frontend (Angular) – Docker Workflow

## 1. Build Docker Image Locally

```bash
docker build -t payroll-fe:25.7.6 --build-arg config=production .
```

---

## 2. Tag the Image

Get the IMAGE ID from the build output (e.g., `1b41687db3cd`), then:

```bash
docker tag 1b41687db3cd mtesfa/payroll-fe:25.7.6
```

---

## 3. Push Image to Docker Hub

```bash
docker push mtesfa/payroll-fe:25.7.6
```

---

## 4. Run on Target Machine

Make sure Docker is installed and you are logged in:

```bash
docker run -d -p 5003:80 --name payroll-fe mtesfa/payroll-fe:25.7.6
```

 Access frontend at:

```
http://<server-ip>:5003
```

---

## 5. (Optional) Pull Image Explicitly

```bash
docker pull mtesfa/payroll-fe:25.7.6
```

---

# ⚙️ Backend (Spring Boot) – Docker Workflow

## 1. Build Docker Image

```bash
docker build -t payroll_api:25.7.21 .
```

---

## 2. Tag the Image

Example IMAGE ID: `c346909fff5d`

```bash
docker tag c346909fff5d mtesfa/payroll_api:25.7.21
```

---

## 3. Push Image to Docker Hub

```bash
docker push mtesfa/payroll_api:25.7.21
```

---

## 4. Run on Target Machine

```bash
docker run -d \
  -p 5005:8080 \
  -e SPRING_PROFILES_ACTIVE=live \
  --name payroll_api \
  mtesfa/payroll_api:25.7.21
```

 Backend runs at:

```
http://<server-ip>:5005
```

---

# 🔐 Notes & Best Practices

* ✅ Always use version tags (avoid `latest` in production)
* ✅ Use environment variables for configs (e.g., DB, JWT, URLs)
* ✅ Ensure required ports are open on the server
* ✅ Use `docker logs -f <container>` for debugging
* ✅ Use `docker ps` to verify running containers

---

# 🛠️ Useful Commands

### Check running containers

```bash
docker ps
```

### View logs

```bash
docker logs -f payroll_api
```

### Stop container

```bash
docker stop payroll_api
```

### Remove container

```bash
docker rm payroll_api
```

---

# 📌 Example Deployment Server

Target Machine:

```
10.1.12.70 
