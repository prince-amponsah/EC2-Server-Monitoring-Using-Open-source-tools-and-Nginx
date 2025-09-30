# Monitoring-EC2-Server-Monitoring-Using-Open-source-tools-and-Nginx

Monitoring of EC2 instances is mostly done with **CloudWatch**, but in this short demo, I implemented monitoring of an EC2 instance that’s running a website with **Nginx Server**, using **Prometheus** and **Grafana** to track key metrics like **CPU, Memory, and Network flow**.

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

   ![Prometheus Status](https://github.com/user-attachments/assets/8c6fd6b4-08b8-44fb-8a7b-bebf96efd8dc)

   Configure Prometheus scrape jobs (edit config file):

   ```bash
   sudo nano /etc/prometheus/prometheus.yml
   ```

   Add:

   ```yaml
   scrape_configs:
     - job_name: "prometheus"
       static_configs:
         - targets: ["localhost:9090"]

     - job_name: "node_exporter"
       static_configs:
         - targets: ["localhost:9100"]
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

   ![Nginx Deployment](https://github.com/user-attachments/assets/your-image-id.png)

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

---

Do you also want me to **convert this into a single `docker-compose.yml` stack** (Prometheus + Grafana + Node Exporter + Nginx), so you won’t have to install packages manually on EC2?
```
