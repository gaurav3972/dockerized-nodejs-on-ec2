# 🚀 Dockerized Node.js App on AWS EC2 (Ubuntu)

A simple Node.js application containerized using Docker and deployed on an AWS EC2 Ubuntu instance. This project demonstrates how to set up a basic Express server, build a Docker image, and run the application on the cloud.

---

## 📌 Project Features

- 🧱 Simple Node.js + Express web server
- 🐳 Dockerized with custom `Dockerfile`
- ☁️ Deployed on AWS EC2 (Ubuntu)
- 🌍 Accessible from any browser using EC2 public IP

---

## 🧰 Tech Stack

- Node.js
- Express
- Docker
- AWS EC2 (Ubuntu)

---

## 📁 Project Structure


````
docker-aws-project/
├── app/
│   ├── server.js         # Node.js application
│   └── package.json      # Dependencies
├── Dockerfile            # Docker build config
├── .dockerignore         # Ignore unnecessary files
└── README.md             # Project documentation

````

---

## ✅ Step-by-Step Setup Guide

### 1️⃣ Clone the Project (on your local system)


git clone https://github.com/your-username/docker-aws-project.git
cd docker-aws-project

OR manually create the folder and files as per the structure above.

---

### 2️⃣ Create the App Files

📄 `app/server.js`

```js
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send('Hello from Docker on AWS EC2 (Ubuntu)!');
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

📄 `app/package.json`

```json
{
  "name": "docker-node-app",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

---

### 3️⃣ Create Dockerfile

📄 `Dockerfile`

```Dockerfile
FROM node:18

WORKDIR /app

COPY app/package*.json ./
RUN npm install

COPY app/ .

EXPOSE 3000

CMD ["npm", "start"]
```

📄 `.dockerignore`

```
node_modules
npm-debug.log
```

---

### 4️⃣ Launch an Ubuntu EC2 Instance

* Use Ubuntu 22.04 or Amazon Linux 2
* Allow inbound ports: `22` (SSH) and `3000` (App)

---

### 5️⃣ Install Docker on EC2

SSH into your EC2 instance:

```bash
ssh -i your-key.pem ubuntu@<your-ec2-public-ip>
```

Install Docker:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
exit
```

Log in again to apply group permissions:

```bash
ssh -i your-key.pem ubuntu@<your-ec2-public-ip>
```

---

### 6️⃣ Upload Project to EC2

From your local machine:

```bash
scp -i your-key.pem -r docker-aws-project ubuntu@<your-ec2-public-ip>:~
```

Then on EC2:

```bash
cd docker-aws-project
docker build -t node-docker-app .
docker run -d -p 3000:3000 node-docker-app
```

---

### 7️⃣ Access the App

Open your browser and go to:

```
http://<your-ec2-public-ip>:3000
```

You should see:

> Hello from Docker on AWS EC2 (Ubuntu)!

---

## 🛡️ Security Group Configuration

Make sure EC2's security group allows:

| Type       | Port Range | Source    |
| ---------- | ---------- | --------- |
| SSH        | 22         | 0.0.0.0/0 |
| Custom TCP | 3000       | 0.0.0.0/0 |

## 🤝 Author

**Gaurav Patil**
Cloud & DevOps Enthusiast
📧 [3972gauravpatil@gmail.com](mailto:3972gauravpatil@gmail.com)

---

## 📷 Sample Screenshot

---

## 🏁 Final Notes

This project is perfect to showcase:

* Docker basics
* AWS EC2 deployment
* Node.js backend knowledge

