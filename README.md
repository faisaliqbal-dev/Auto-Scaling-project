## 🔥 **Project Title:**  
**Auto-Scaling Static Website Hosting on AWS with Monitoring and Notifications**

---

## 📘 **Project Description:**

In this project, I created a highly available and scalable static website architecture using multiple AWS services. The aim was to deploy a static website on an EC2 instance and automatically handle varying traffic loads using auto scaling, all while monitoring system performance and receiving alerts through email.

---

## ✅ **Steps I Performed:**

### 1. **EC2 Instance and Static Website Deployment**
- I launched a new EC2 instance.
- Connected to it using **WinSCP** and uploaded a static HTML website.
- Installed a web server (like Apache) to host the website.

---

### 2. **Creating an AMI (Amazon Machine Image)**
- I created a custom **AMI** from the EC2 instance to preserve the setup of my static website.
- Selected an existing **key pair** and **security group** during the AMI creation.

---

### 3. **Setting Up a Classic Load Balancer**
- I created a **Classic Load Balancer (CLB)** and selected **4 Availability Zones** to ensure high availability.
- Verified that the website was accessible via the Load Balancer DNS.

---

### 4. **SNS Topic and Email Notification**
- I created an **SNS Topic** named `mytopic`.
- Subscribed my email address `faisaliqbal.dev@gmail.com` to receive notifications.
- Confirmed the email subscription.

---

### 5. **Auto Scaling Group (ASG) Configuration**
- I launched an **Auto Scaling Group** using the custom AMI.
- Selected the same 4 Availability Zones and attached the Classic Load Balancer.
- Set:
  - **Desired capacity:** 2 instances  
  - **Minimum capacity:** 2  
  - **Maximum capacity:** 5  
- Enabled **notifications** using the SNS topic.

---

### 6. **CloudWatch Alarms for Monitoring**
- I used **Amazon CloudWatch** to monitor EC2 metrics by Auto Scaling Group.
- Created 2 alarms:
  1. **If CPU Utilization > 40%**, send an email notification.
  2. **If CPU Utilization < 30%**, send another notification.

---

### 7. **Dynamic Scaling Policies**
- Enabled **Dynamic Scaling** in the Auto Scaling Group.
- Created 2 simple scaling policies:
  - **High-Cpu-Usage:** Add 1 instance if CPU > 40%.
  - **Low-Cpu-Usage:** Remove 1 instance if CPU < 30%.

---

### 8. **Stress Test to Trigger Auto Scaling**
- Installed the `stress` tool on EC2 to simulate CPU load.
- Ran the command: `stress --cpu 4 -t 600` (which increases CPU load for 10 minutes).
- CloudWatch detected high CPU usage and triggered auto scaling.
- Instances scaled up to the maximum (5 instances).
- After the load reduced, CloudWatch triggered scale-in and the group returned to the desired capacity (2 instances).
- All notifications were successfully received via email.

---

## 🚀 **Key Learnings & Skills Gained:**
- Launching and managing EC2 instances
- Creating and using AMIs
- Setting up Classic Load Balancer
- Creating and configuring Auto Scaling Groups
- Implementing monitoring with CloudWatch
- Sending alerts using SNS
- Performing load testing using `stress`
- Automating scale-in and scale-out of instances
