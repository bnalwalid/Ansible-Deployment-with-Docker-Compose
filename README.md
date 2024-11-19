# **Ansible Deployment with Docker Compose**

Follow the instructions below to set up Ansible locally, run the playbook, verify the deployment, and manage services in the `docker-compose.yml` stack.

---

## **Setup Requirements**

1. **Install Ansible**  
   Ensure you have Python installed on your machine.

   ```bash
   sudo apt update
   sudo apt install ansible -y
   ```

2. **Install Docker and Docker Compose**  
   Install Docker and Docker Compose to manage the services.

   ```bash
   sudo apt install docker.io docker-compose -y
   ```

3. **Clone the Repository**  
   Clone this repository to your local machine.

   ```bash
   git clone https://github.com/your-repo/ansible-docker-stack.git
   cd ansible-docker-stack
   ```

---

## **Setting Up Ansible Locally**

1. **Configure the Inventory File**  
   Add your local or remote server details to the `inventory.ini` file:

   ```ini
   [local]
   localhost ansible_connection=local
   ```

2. **Check Ansible Version**  
   Verify that Ansible is installed:

   ```bash
   ansible --version
   ```

3. **Test Connection**  
   Ensure Ansible can communicate with the server:

   ```bash
   ansible -i inventory.ini all -m ping
   ```

---

## **Instructions to Run the Playbook**

**Path to project files** 
 ```bash
   /root/laravel-app
   ```
1. **Review the Playbook**  
   Open `deploy.yml` to review tasks such as Docker installation, stack deployment, and service management.

2. **Run the Playbook**  
   Execute the playbook to set up Docker Compose and deploy the stack:

   ```bash
   ansible-playbook -i inventory.ini deploy.yml
   ```

   This playbook will:
   - Install Docker and Docker Compose (if not already installed).
   - Deploy services defined in the `docker-compose.yml` file.

3. **Monitor the Output**  
   Ensure all tasks complete successfully. If there are errors, resolve them as indicated.

---

## **How to Verify the Deployment**

1. **Check Running Containers**  
   After deployment, log into the server and verify the running containers:

   ```bash
   docker ps
   ```

2. **Access the Application**  
   Open your web browser and navigate to `http://localhost` (or your server's IP address). Check that the application is running.

3. **Inspect Logs**  
   Review the logs for running services to ensure proper functionality:

   ```bash
   docker-compose logs -f
   ```

---

## **How to Add or Modify Services in the Stack**

1. **Edit `docker-compose.yml`**  
   Open the `docker-compose.yml` file and add or modify services as needed. For example, to add a Redis service:

   ```yaml
   redis:
     image: redis:latest
     ports:
       - "6379:6379"
   ```

2. **Apply Changes**  
   Apply the updated `docker-compose.yml` file by redeploying the stack:

   ```bash
   docker-compose up -d
   ```

3. **Update the Ansible Playbook (Optional)**  
   If the new service requires additional configuration, update the `deploy.yml` playbook accordingly.

4. **Verify New Services**  
   Check that the new or modified services are running:

   ```bash
   docker ps
   ```

---

## **Cleanup**

To stop and remove the stack, run:

```bash
docker-compose down
```
---
