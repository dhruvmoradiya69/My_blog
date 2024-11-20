---
title: "Day-46: Set Up CloudWatch Alarms and SNS Topic in AWS"
datePublished: Wed Nov 20 2024 11:32:45 GMT+0000 (Coordinated Universal Time)
cuid: cm3pt0yzv000409l94j6w9oji
slug: day-46-set-up-cloudwatch-alarms-and-sns-topic-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732102314217/10fb7cb5-f217-4562-8713-4284442cb6e3.webp
tags: aws, devops, sns, aws-cloudwatch, 90daysofdevops, aws-sns, tws

---

Hey, learners! 🎉  
You’ve been working with AWS services for at least the past 45 days. But have you ever wondered what would happen if a service kept charging your account, and you didn’t realize it until your pocket money was gone? 😱

---

### **What is Amazon CloudWatch?**

Amazon CloudWatch is a monitoring service for AWS resources and the applications running on them. It provides real-time metrics, allowing you to collect and track data like CPU usage, memory usage, and billing information.

➡️ **Learn more from the** [**official documentation**](https://docs.aws.amazon.com/cloudwatch/)**.**

---

### **What is Amazon SNS?**

Amazon Simple Notification Service (SNS) is a messaging service designed for mass delivery of messages—ideal for mobile users. It’s cost-effective and allows you to send notifications to subscribers via email, SMS, or other means.

➡️ **Read more about SNS** [**here**](https://docs.aws.amazon.com/sns/)**.**

---

### **Today's Task**

We’ll set up a CloudWatch alarm to monitor your billing and notify you via email when the cost exceeds $2. Here’s what we’ll cover:

1. **Create a CloudWatch Alarm**
    
2. **Send Notifications via SNS**
    
3. **Delete the Billing Alarm**
    

---

### **Step-by-Step Guide**

#### **1\. Create a CloudWatch Alarm for Billing**

* **Requirement:** Ensure billing alerts are enabled in your AWS account.
    
* Go to the **CloudWatch** console.
    
* Select **Billing** under metrics (use the **Billing metric namespace**).
    
* Choose the metric **EstimatedCharges**.
    
* Set a threshold: `$2` (you can adjust this based on your budget).
    
* Configure the alarm to trigger when the threshold is breached.
    

**Tip:** Make sure your AWS region supports billing alarms (usually, this is only available in the `US East (N. Virginia)` region).

---

#### **2\. Send Notifications via SNS**

* **Requirement:** Create an SNS topic to receive notifications.
    
* Go to the **SNS** console and create a new topic (e.g., `BillingAlertsTopic`).
    
* Add an email subscription to the topic.
    
* Confirm the subscription via the email link sent to your inbox.
    
* Link the SNS topic to your CloudWatch alarm during the alarm setup.
    

**Pro Tip:** Use an easily accessible email address so you never miss important notifications.

---

#### **3\. Delete the Billing Alarm**

* Navigate to the **CloudWatch** console.
    
* Go to the **Alarms** section.
    
* Select the billing alarm you created.
    
* Click **Delete** to remove it.
    

**Why Delete?** This helps you practice managing alarms and ensures you don’t get unnecessary notifications during testing.

---

### **Need More Help?**

If you’re stuck or need further clarification:

* Check out the [CloudWatch documentation](https://docs.aws.amazon.com/cloudwatch/) for detailed guidance.
    
* Review the [SNS documentation](https://docs.aws.amazon.com/sns/) for additional help.
    

---

### **Conclusion**

By setting up a CloudWatch alarm and integrating it with an SNS topic, you ensure you’ll never be caught off guard by unexpected AWS charges. This is an essential skill for any AWS user aiming to manage costs effectively. 💰

Let us know how it went in the comments, or share any tips you discovered during this task. **Happy learning!** 🚀

---