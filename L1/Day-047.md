# Day 47: Docker Python App

## Scenario

A python app needed to be Dockerized, and then it needs to be deployed on App Server 1. We have already copied a requirements.txt file (having the app dependencies) under /python_app/src/ directory on App Server 1. Further complete this task as per details mentioned below:


- Create a `Dockerfile` under **/python_app** directory.
    - Use any `python` image as the base image.
    - Install the dependencies using **requirements.txt** file.
    - Expose the port **3002**.
    - Run the **server.py** script using CMD.
- Build an image named **nautilus/python-app** using this Dockerfile.
- Once image is built, create a container named `pythonapp_nautilus`.
    - Map port `3002` of the container to the host port `8094`.
- Once deployed, you can test the app using `curl` command on App Server 1.

  curl http://localhost:8094/   

---

## Task

- Create a Docker image called `nautilus/python-app` using the Dcokerfile, with the specified requirements and command.
- Create and run the container `pythonapp_nautilus` with port mapping.

---

## Solution

### 1. SSH into App Server 1

```bash
ssh tony@stapp01
```

---

### 2. Create the Dockerfile under /python_app with below content

```bash
# Use a Python base image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Copy requirements and source code
COPY src/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY src/ .

# Expose the application port
EXPOSE 3002

# Run the server
CMD ["python", "server.py"]

```

---

### 3. Build the Docker Image

```bash
cd /python_app/
docker build -t nautilus/python-app .

```

---

### 4. Run the Container

```bash
docker run -d --name pythonapp_nautilus -p 8094:3002 nautilus/python-app
```

---

### 5. Test the Deployment

```bash
curl http://localhost:8094/

```

---


## Result

- The `nautilus/python-app` Docker image is successfully created along with the pythonapp_nautilus container, port `3002` mapped with host port `8094` on App Server 1.
