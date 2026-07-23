# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![Screenshot](<screenshots/Screenshot 1_Task 1_Assignment 3.png>)

#### Screenshot 2 — Output of `ip a`
![Screenshoot 2](<screenshots/Screenshot 2 _Task 1_Assignment 3.png>)

#### Screenshot 3 — Output of `sudo ss -tulpen`

![Screenshot 3](<screenshots/Screenshot 3_Task 1_Assignment 3.png>)



#### Screenshot 4 — Output of `sudo ufw status`

![Screenshot 4](<screenshots/Screenshot 4_Task 1_Assignment 3.png>)


### Notes

Answer the following in your own words:

1. What proves Nginx is listening on 0.0.0.0:80?

Write your answer here.

The output showed 0.0.0.0:80 with the nginx process, confirming that Nginx is listening on port 80 and accepting HTTP connections from all network interfaces.

2. What proves SSH is active on port 22?

Write your answer here.

The output showed 0.0.0.0:22 with the sshd process, confirming that the SSH service is running and listening on port 22 for remote connections.

3. Did you find any unexpected open ports? Explain briefly.

Write your answer here.

No. I only found the expected open ports: 22 for SSH and 80 for Nginx (HTTP). There were no unexpected ports open that could pose a security risk.

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

![Screenshot 1](<screenshots/Screenshot 1_Assignment 3_ Task 2.png>)



#### Screenshot 2 — Output of `sudo nginx -t`


![Screenshot](<screenshots/Screenshot 2_Assignment 3_ Task 2.png>)


#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

![Screenshot](<screenshots/Screenshot 3_Assignment 3_ Task 2.png>)


### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

Write your answer here.

If Nginx fails to restart, the website or application becomes unavailable to users. This can cause downtime, prevent users from accessing the service, and may affect business operations until the issue is fixed.

**2. What's your basic rollback plan?**

Write your answer here.

If Nginx fails after a configuration change, I would restore the last working configuration, test it using nginx -t, and then restart the Nginx service. This helps bring the website back online quickly while I investigate the issue.

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

![Screenshot 1](<screenshots/Screenshot 1 _Assignment_3 Task 3.png>)



#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

![Screenshot](<screenshots/Screenshot 2_Assignment_3 Task 3.png>)



#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

![Screenshot 3](<screenshots/Screenshot 3_Assignment_3 Task 3.png>)


### Notes

Answer the following in your own words:

1. Were there any errors in the logs?

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

Write your answer here.

No. I did not find any recent errors in the error log. This means the web server was running normally and there were no problems while handling requests during my check.

2. If there were no errors, what does that indicate about the system?

Write your answer here.

It indicates that the system is healthy and functioning correctly. The web server is running properly and processing requests without any issues or failures.

3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?

Write your answer here.

Yes. My curl requests appeared in the access log. This proves that the requests successfully reached the web server, the server processed them, and it returned a response. It also confirms that network connectivity and HTTP traffic flow were working correctly.

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

![Screenshot](<screenshots/Screenshot 1_Assignment_3_Task_4.png>)



#### Screenshot 2 — Output of `free -h`

![Screenshot](<screenshots/Screenshot 2_Assignment_3_Task_4.png>)



#### Screenshot 3 — Output of `df -h`

![Screenshot](<screenshots/Screenshot 3_Assignment_3_Task_4.png>)



#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

![Screenshot 4](<screenshots/Screenshot 4_Assignment_3_Task_4.png>)



### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Write your answer here.

The disk is the most critical resource because if it runs out of space, the server may not be able to save logs, store data, or run applications properly. Monitoring disk usage helps prevent unexpected system failures.

**2. What happens if disk becomes 100% full in a production server?**

Write your answer here.
If the disk becomes 100% full, the server may stop working properly. Applications may fail to save data, logs cannot be written, updates may not install, and some services may crash or become unavailable. This can lead to downtime and affect users accessing the application.

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

![Screenshot 1](<screenshots/ Screenshot 1_Assignment 3_Task_5.png>)



#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

![Screenshot 2](<screenshots/Screenshot 2 _Assignment 3_Task_5.png>)



#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

![Screenshot 3](<screenshots/Screenshot 3_Assignment 3_Task_5.png>)



### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

Write your answer here.

I confirm the correct version of the application is deployed by checking the application's version or build information after deployment. I can also access the application in a web browser or use curl to verify that it displays the expected version and is working correctly. If the version matches the latest deployment, it confirms that the correct application has been deployed successfully.

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

![Screenshot 1](<screenshots/Screenshot 1_Assignment_3_Task 6.png>)



#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

![Screenshot 2](<screenshots/Screenshot 2_Assignment_3_Task 6.png>)



#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![Screenshot 3](<screenshots/Screenshot 3_Assignment_3_Task 6.png>)



### Notes

Answer the following in your own words:

1. What caused the configuration failure?

Write your answer here.

The configuration failure was caused by an incorrect setting in the configuration file. This could be a wrong value, a missing parameter, or a syntax error that prevented the service from starting correctly.

2. How did you fix the issue?

Write your answer here.

I checked the error message, reviewed the configuration file, corrected the incorrect setting, and restarted the service. After restarting, I verified that the application was running normally.

3. How can you avoid this kind of issue in real production systems?

Cause: A mistake in the configuration file.

Fix: Corrected the setting and restarted the service.

Prevention: Test changes first, use reviews, backups, and monitoring.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

![Screenshot 1](<screenshots/Screenshot 1_Assignment_3_Task_7.png>)



#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![Screenshot 2](<screenshots/Screenshot 2_Assignment_3_Task_7.png>)



### Notes

Answer the following in your own words:

1. What caused the application to break in this scenario?

Write your answer here

The application failed because the deployed web application directory (/var/www/html) was moved and replaced with an empty directory. Since the required HTML, CSS, JavaScript, and application files were missing, Nginx could not serve the expected website content, resulting in an error response.

2. How did you fix the issue and restore the application?

Write your answer here.

The issue was fixed by removing the empty web directory and restoring the original application files from the backup:

sudo rm -rf /var/www/html
sudo mv /var/www/html_backup /var/www/html
sudo systemctl restart nginx

3. What steps would you take to prevent this kind of issue in real production systems?

Write your answer here.

Maintain regular backups of application files and configurations.
Use version control systems such as Git to track deployment changes.
Use automated deployment tools with rollback capabilities.
Test deployments in a staging environment before pushing to production.
Implement monitoring and alerting using tools like Amazon CloudWatch.
Use Infrastructure as Code (IaC) tools such as Terraform or AWS CloudFormation to recreate environments quickly.
Apply proper access controls to prevent accidental deletion or modification of production files.
Use deployment strategies like Blue/Green Deployment or Rolling Deployment to reduce downtime during updates.

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

1. Why is SSH key-based authentication more secure than sharing passwords?

Write your answer here.

SSH key-based authentication is more secure because it uses a pair of cryptographic keys (a private key and a public key) instead of a password. The private key remains with the user and is never shared with the server. This makes it much harder for attackers to gain access through password guessing, brute-force attacks, or stolen passwords.

2. Why should only required ports be open on a production server?

Write your answer here.

Only required ports should be open because every open port creates a possible entry point for attackers. Limiting access to only necessary ports reduces the attack surface, improves security, and helps prevent unauthorized access to services running on the server.

3. Why is it important for Nginx to be enabled on boot?

Write your answer here.

Enabling Nginx on boot ensures that the web server automatically starts whenever the server restarts. This helps maintain application availability and reduces downtime because the website can become accessible again without requiring manual intervention.
Command: sudo systemctl enable nginx

4. What are the risks of sharing secrets, keys, or credentials publicly?

Write your answer here.

Sharing secrets, SSH keys, API keys, or cloud credentials publicly can allow unauthorized users to access systems, steal data, modify resources, or create unexpected costs. Attackers can use exposed credentials to compromise servers, databases, and cloud accounts.

5. Why should cloud resources be stopped or terminated when they are no longer needed?

Write your answer here.

Cloud resources should be stopped or terminated when they are no longer needed to avoid unnecessary costs and reduce security risks. Unused resources can continue consuming money and may become targets for attackers if they are not properly maintained or secured. Proper resource management helps optimize cloud spending and improves overall security.

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/senyocouragekwaku_devops-cloudcomputing-aws-share-7483230108296642560-fs3y/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADn3DX0BJj1PVBzmKTFriaizjpjw6GKyID4

`https://www.linkedin.com/posts/senyocouragekwaku_devops-cloudcomputing-aws-share-7483230108296642560-fs3y/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADn3DX0BJj1PVBzmKTFriaizjpjw6GKyID4`

---

#### Screenshot — Published LinkedIn post

![Linkedin Post](<screenshots/Screenshot 1_assignment_3_Linkedin post.png>)


# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*