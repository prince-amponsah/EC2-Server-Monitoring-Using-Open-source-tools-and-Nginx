# Monitoring-EC2-Server-Monitoring-Using-Open-source-tools-and-Nginx


Monitoring or EC2 INstances are mostly done with cloud watch, but in this short demo, In implemented monitoring of an EC2 Instance thats running a website with Nginx Server to help Monitor key logs like CPU, Memory and Network flow.




# Setup Guide: Prometheus, Grafana & Nginx on AWS EC2 (Ubuntu)

## 1. Launch an EC2 Instance
   i. head to AWS Ec2 Dashboard and setup an instance of your choice
2. Update oackages -
    sudo apt update -y
4. Install Prometheus
    i.   sudo apt install prometheus prometheus-node-exporter -y
    ii.  sudo systemctl enable --now prometheus
    iii. sudo systemctl enable --now prometheus-node-exporter
    iv.  systemctl status prometheus
    v.   systemctl status prometheus-node-exporter
   <img width="1440" height="831" alt="Screenshot 2025-09-30 at 09 49 36" src="https://github.com/user-attachments/assets/8c6fd6b4-08b8-44fb-8a7b-bebf96efd8dc" />

6. Install Grafana
   i. Follow Grafana Installation:
      https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/
8. Install Nginx Server
   i. sudo apt update -y
   ii. systemctl enable nginx - This makes the server kicks in when you restart the entire instance
10. Download and setup html site in nginx
    ii. head to https://www.tooplate.com, select a template of your choice, download unto your instance with wget
    ii. install unzip if you don't have and unzip the zipped folder.
    iii. cd into the unzipped folder and move all the files into nginx index loading folder
    sudo mv * /var/www/html/
   ![Uploading Screenshot 2025-09-30 at 11.11.11.png…]()


12. Configure Security Groups
    i. Open inbound port 9090 for Prometheus from your IP
    ii. Open inbound port 3000 for Grafana from your IP
    iii. Open port 80 from anywhere to be able to see the site being hosted by nginx
14. Login to grafana and setup data sources from Prometheus Server
    Access Grafana:
👉 http://<EC2-Public-IP>:3000
(Default login: admin / admin)
    
    <img width="1145" height="263" alt="Screenshot 2025-09-30 at 10 19 56" src="https://github.com/user-attachments/assets/cbce71fc-661f-4e62-bf60-3f9d4f676f56" />
<img width="1436" height="832" alt="Screenshot 2025-09-30 at 10 10 44" src="https://github.com/user-attachments/assets/954d6d64-7889-4330-b585-61efc14983af" />
<img width="1435" height="832" alt="Screenshot 2025-09-30 at 10 37 51" src="https://github.com/user-attachments/assets/e9fc49a7-1b0d-4f62-8048-91c54d5bf4f1" />


