# Monitoring-EC2-Server-Monitoring-Using-Open-source-tools-and-Nginx

Monitoring of EC2 instances is mostly done with **CloudWatch**, but in this short demo, I implemented monitoring of an EC2 instance that’s running a website with **Nginx Server**, using **Prometheus** and **Grafana** to track key metrics like **CPU, Memory, and Network flow**.
<img width="1438" height="832" alt="Screenshot 2025-09-30 at 11 11 11" src="https://github.com/user-attachments/assets/1f93d774-78b1-4dbe-8da1-255c3658420e" />
<img width="1435" height="832" alt="Screenshot 2025-09-30 at 10 37 51" src="https://github.com/user-attachments/assets/446934a0-2602-49d5-be8e-72f002262847" />
<img width="1145" height="263" alt="Screenshot 2025-09-30 at 10 19 56" src="https://github.com/user-attachments/assets/a38fd453-806c-466c-af53-17dab02df56b" />
<img width="1436" height="832" alt="Screenshot 2025-09-30 at 10 10 44" src="https://github.com/user-attachments/assets/01462d2c-b568-4227-a157-0d5136dd1f71" />
<img width="1440" height="831" alt="Screenshot 2025-09-30 at 09 49 36" src="https://github.com/user-attachments/assets/463d0d39-6257-4c2a-8e31-069dec7ee053" />


## Setup Guide: Prometheus, Grafana & Nginx on AWS EC2 (Ubuntu)

1. Launch an EC2 Instance  
   - Head to the AWS EC2 Dashboard and set up an Ubuntu instance of your choice.

2. Update packages  
   ```bash
   sudo apt update -y && sudo apt upgrade -y
````

3. Install Prometheus

   ```bash
   sudo apt install prometheus prometheus-node-exporter -y
   sudo systemctl enable --now prometheus
   sudo systemctl enable --now prometheus-node-exporter
   systemctl status prometheus
   systemctl status prometheus-node-exporter
   ```
   Restart Prometheus:

   ```bash
   sudo systemctl restart prometheus
   ```


4. Install Grafana
   Follow Grafana installation:
   👉 [https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/](https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/)

   ```bash
   sudo systemctl enable --now grafana-server
   systemctl status grafana-server
   ```

5. Install Nginx Server

   ```bash
   sudo apt install nginx -y
   sudo systemctl enable --now nginx
   ```

   > This makes the server start automatically when you restart the instance.

6. Download and Setup HTML site in Nginx

   * Go to [Tooplate](https://www.tooplate.com), choose a template, and download it:

     ```bash
     wget https://www.tooplate.com/zip-templates/2106_soft_landing.zip
     ```
   * Install unzip if not present and extract:

     ```bash
     sudo apt install unzip -y
     unzip 2106_soft_landing.zip
     ```
   * Move website files into the Nginx web root:

     ```bash
     cd 2106_soft_landing
     sudo mv * /var/www/html/
     ```
  
7. Configure Security Groups

   * Open inbound **port 9090** for Prometheus (from your IP).
   * Open inbound **port 3000** for Grafana (from your IP).
   * Open inbound **port 80** (from anywhere) to view the hosted Nginx site.

8. Access Grafana & Add Prometheus Data Source

   * Go to 👉 `http://<EC2-Public-IP>:3000`
   * Default login: **admin / admin**
   * Add Prometheus as a data source: `http://<EC2-Public-IP>:9090`
---

✅ You now have **Prometheus**, **Grafana**, and **Nginx** running on your EC2 instance, providing monitoring + a live hosted website.

```

