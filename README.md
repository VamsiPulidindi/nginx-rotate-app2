# Nginx Rotating Web Pages with Docker

This project demonstrates how to rotate multiple HTML pages automatically inside an Nginx container using Docker and Bash scripting.

The application switches between 3 HTML pages every 5 seconds.

---

# Project Structure

```bash
nginx-rotate-app/
│
├── docker-compose.yml
├── Dockerfile
├── start.sh
│
└── webpages/
    ├── index1.html
    ├── index2.html
    ├── index3.html
    └── rotate_pages.sh
```

---

# Features

* Dockerized Nginx application
* Automatic webpage rotation
* Page changes every 5 seconds
* Simple Bash scripting
* Easy to start and stop using Docker Compose

---

# HTML Pages

The application contains:

* Page 1 → Light Blue
* Page 2 → Light Green
* Page 3 → Light Coral

The displayed page rotates automatically.

---

# How Rotation Works

The script:

```bash
rotate_pages.sh
```

creates a symbolic link:

```bash
index.html -> index1.html
index.html -> index2.html
index.html -> index3.html
```

every 5 seconds.

Nginx always serves `index.html`, which points to a different page during rotation.

---

# Prerequisites

Install:

* Docker
* Docker Compose

Verify installation:

```bash
docker --version
docker compose version
```

---

# Build and Start the Application

Open terminal inside the project folder:

```bash
cd nginx-rotate-app
```

Build and start:

```bash
docker compose up --build
```

---

# Access the Application

Open browser:

```bash
http://localhost
```

You will see pages rotating automatically every 5 seconds.

---

# Run in Background

To run container in detached mode:

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker ps
```

---

# Stop the Application

Stop containers:

```bash
docker compose down
```

---

# Restart the Application

```bash
docker compose restart
```

---

# View Logs

```bash
docker compose logs
```

Live logs:

```bash
docker compose logs -f
```

---

# Rebuild After Changes

If you modify HTML files or scripts:

```bash
docker compose up --build
```

---

# Remove Containers and Images

Remove containers:

```bash
docker compose down
```

Remove containers + images:

```bash
docker compose down --rmi all
```

---

# Docker Components Explanation

## Dockerfile

Builds custom Nginx image and copies files into container.

## start.sh

Starts:

1. Page rotation script
2. Nginx server

## rotate_pages.sh

Rotates pages by updating symbolic links.

## docker-compose.yml

Defines container configuration and port mapping.

---

# Port Mapping

```yaml
ports:
  - "80:80"
```

Meaning:

* Left side → Host machine port
* Right side → Container port

Access via:

```bash
http://localhost
```

---

# Common Commands

## Start

```bash
docker compose up
```

## Start in Background

```bash
docker compose up -d
```

## Stop

```bash
docker compose down
```

## Restart

```bash
docker compose restart
```

## Check Running Containers

```bash
docker ps
```

---

# Troubleshooting

## Port 80 Already in Use

Error:

```bash
bind: address already in use
```

Solution:

Either stop the existing service using port 80:

```bash
docker ps
```

then:

```bash
docker stop <container_id>
```

OR change port mapping:

```yaml
ports:
  - "8080:80"
```

Then access:

```bash
http://localhost:8080
```

---
