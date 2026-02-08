# AWS CloudWatch CPU Monitoring & SNS Alerting

## 📌 Project Overview
This project demonstrates how to monitor EC2 instance CPU utilization using **AWS CloudWatch** and send **automated email alerts via Amazon SNS** when CPU usage exceeds a defined threshold (80%). It simulates a real-world monitoring and alerting use case commonly used in DevOps and Cloud environments.

---

## 🛠️ Services Used
- **Amazon EC2** – Compute resource to monitor
- **Amazon CloudWatch** – Metrics and alarm configuration
- **Amazon SNS (Simple Notification Service)** – Email alert notifications
- **IAM** – Access and permission management

---

## 🧠 Architecture
**Flow:**
1. EC2 instance publishes CPU utilization metrics to CloudWatch
2. CloudWatch Alarm monitors CPU usage
3. Alarm triggers when CPU usage exceeds 80%
4. SNS topic sends an email notification to subscribed users

*()*

---

## ⚙️ Implementation Steps
### 💥 Step 1: Create an SNS Topic

1. **Open SNS Console**
    
    https://console.aws.amazon.com/sns
    
2. **Click “Topics” > “Create topic”**
3. **Choose topic type:**
    - Use **Standard** (the FIFO one is for people who like pain).
4. **Name it something creative**, like:
    
    `cpu-spike-warning`
    
5. **Click “Create topic”**

### 📬 Step 2: Subscribe to the Topic (Your Email)

1. After topic creation, click **“Create subscription”**
2. **Protocol:** `Email`
    
    **Endpoint:** Your email address
    
    (Example: "abc123@hotmail.com")
    
3. **Click “Create subscription”**
4. Go to your **email inbox** and **confirm** the subscription.

### 📊 Step 3: Create a CloudWatch Alarm

1. Go to **CloudWatch Console**
    
    https://console.aws.amazon.com/cloudwatch
    
2. On the left menu, choose **“Alarms” > “Create Alarm”**
3. **Select Metric**
    - Choose:
        
        `EC2 > Per-Instance Metrics > CPUUtilization`
        
    - Select your poor, overworked EC2 instance.
4. **Click “Select metric”**
5. **Set Conditions**
    - Threshold type: **Static**
    - Whenever **CPUUtilization > 80%**
    - For 1 out of 1 datapoints (adjust if you want to be fancy or less panicky)
6. **Next: Notification**
    - Choose **“Select an existing SNS topic”**
    - Pick your `cpu-spike-warning` topic
    
    OR
    
    - Create new one here if you missed Step 1 somehow (which would be impressive)
7. **Alarm name**:
    
    `ec2-high-cpu-alert`
    
    Feel free to name it something else
    
8. Click **“Next”**, review and click **“Create alarm”**

### 🧪 Step 4: Test It

1. SSH into your EC2 instance
2. Run something CPU-intensive like:
    
    ```bash
    sudo yum install stress -y  # (or apt-get on Ubuntu)
    stress --cpu 2 --timeout 300
    ```
    
3. Sit back and watch your inbox light up like Times Square.

### ✅ That’s It

When CPU spikes >80%, CloudWatch will go "OH NO," SNS will go "EMAIL TIME," and your inbox will whisper, "You're bad at scaling workloads."

---

## 🧪 Testing & Validation
- Generated artificial CPU load on the EC2 instance
- Verified alarm state change from **OK → ALARM**
- Confirmed successful email alert delivery via SNS
- Ensured notifications were received in near real-time

---

## 📸 Screenshots
*(Optional but highly recommended)*
- CloudWatch Alarm configuration
- SNS topic & email subscription
- Alert email received

---

## ✅ Outcome
- Successfully implemented automated monitoring and alerting
- Gained hands-on experience with AWS monitoring best practices
- Understood alarm states: **OK, ALARM, INSUFFICIENT_DATA**

---

## 🚀 Key Learnings
- Importance of proactive monitoring in cloud infrastructure
- How CloudWatch alarms integrate with SNS
- Real-world usage of AWS services for operational reliability

---

## 📚 Future Improvements
- Add SMS notifications
- Use Auto Scaling to handle high CPU usage
- Implement infrastructure using Terraform
- Monitor additional metrics (Memory, Disk, Network)

---

## 👤 Author
**Nur Hoosain Sakil**  
Aspiring DevOps / Cloud Engineer  
GitHub: https://github.com/yourusername  
LinkedIn: https://www.linkedin.com/in/nur-hossain-sakil-a21407130/$0

