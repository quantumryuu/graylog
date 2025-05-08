# 🚀 Graylog Docker Setup Guide

This guide will help you install and run **Graylog** using **Docker**.

---

## 📦 Prerequisites

Make sure the following are installed on your system:

- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/engine/install/)

---

## 🔧 Step-by-Step Setup

### 1. Create a Docker Network

```bash
docker network create graylog -d bridge
```

---
### 2. Create a directory called `graylog` and navigate to it


```bash
mkdir graylog && cd graylog/
```

---

### 3. Get the `docker-compose.yml` file

Download it using:

```bash
wget https://raw.githubusercontent.com/quantumryuu/graylog/refs/heads/main/docker-compose.yml
```

---

### 4. Edit the Docker Compose file

Open `docker-compose.yml` in a text editor (e.g., VS Code, nano, vim) and **change the environment variables** as needed (e.g., passwords, ports, volumes).
- Run `tr -dc A-Z-a-z-0-9_@#%^-_=+ < /dev/urandom | head -c${1:-32}`, copy the output and change `$RANDOMPASSWORD` on `line 22` to the copied generated password.
- Run `tr -dc A-Z-a-z-0-9_@#%^-_=+ < /dev/urandom | head -c${1:-32}` again, copy the output and change `$RANDOMPASSWORD` on `line 34` to the copied generated password.
- Generate a sha256 password by changing the `PASSWORD` on the following command and run it `echo -n PASSWORD | sha256sum`, copy the output and change `$RANDOMSHA256PASSWORD` on `line 35` to the copied generated password.
- Save the file.
---

### 5. Start the Docker Stack

```bash
docker compose up -d
```

This will start all services in the background.

---

### 6. Stop the Docker stack

```bash
docker compose down
```

---

### 7. Download Graylog Configuration fFile

Navigate to the config directory:

```bash
cd ~/graylog/graylog/config/
```

Then download the config file:

```bash
wget https://raw.githubusercontent.com/Graylog2/graylog-docker/refs/heads/main/config/graylog.conf
```

---

### 8. Set correct permissions

Navigate back to the main graylog directory:

```bash
cd ~/graylog
```

Set ownership for the `opensearch` directory:

```bash
sudo chown -R 1000:1000 opensearch/
```

Set ownership for the `graylog` directory:

```bash
sudo chown -R 1100:1100 graylog/
```

---

### 9. Run the Stack again

Finally, start the stack:

```bash
docker compose up -d
```

---

## ✅ Done!

You should now have Graylog running in Docker. Visit it at:

```
http://HOSTIP:9000
```
