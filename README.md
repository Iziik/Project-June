
# 🚀 Project June: The Future of Task-Scheduling


## 📁 Project Structure


project-june/

├── index.html        

├── style.css          

├── .git/              

└── README.md          

## 🔍 Project Overview

This project demonstrates how to:

  1. Host a static/dynamic site on an Ubuntu EC2 instance
  2. Use **Nginx** as a web server and reverse proxy
  3. Secure your domain with Let's Encrypt SSL
  4. Deploy code updates via Git
  5. Serve production-grade HTML/CSS with styling and personalized content

## 🧑‍💻 Technologies Used

| Tool                      | Purpose                             |
| ------------------------- | ----------------------------------- |
| Ubuntu 22.04 (EC2)        | Cloud compute instance              |
| Nginx                     | Web server & reverse proxy          |
| Certbot                   | SSL certificate with Let’s Encrypt  |
| Git                       | Code versioning & deployment        |
| HTML/CSS                  | Frontend design                     |
| Domain (project-june.xyz) | Public access                       |
| UFW / Security Groups     | Networking & firewall configuration |


## ⚙️ Setup Instructions

### ✅ Step 1: Launch EC2 Instance

  AWS EC2 → Ubuntu 22.04 LTS
  
  Add your SSH key
  
  Configure:

  Allow ports 22, 80, 443

### ✅ Step 2: SSH into EC2

* Copy from AWS

```
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

### ✅ Step 3: Install Nginx & Git

```
sudo apt update
sudo apt install nginx git -y
```

### ✅ Step 4: Set Up Project Directory

```
sudo mkdir -p /var/www/project-june
sudo chown -R $USER:$USER /var/www/project-june
```

Install git(on Ec2) & Clone your project:

```
cd /var/www/project-june
git remote add origin https://github.com/<your-username>/<your-repo>.git
git pull origin main
```

### ✅ Step 5: Configure Nginx

```
sudo vim /etc/nginx/sites-available/project-june
```
* Ensure it points to your Ec2 ip address or your domain name (If configured)
* It should also be able to locate your index.html file or Node.js file 

Enable the site:

```
sudo ln -s /etc/nginx/sites-available/project-june /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl reload nginx
```

### ✅ Step 6: Set up DNS for Your Domain

1. Go to your domain DNS manager (e.g., Namecheap)
2. Add an **A record** for:

   * `@` → your EC2 IP
   * `www` → your EC2 IP
3. Save and wait a few minutes

### ✅ Step 7: Install Certbot and Secure with SSL

Install via Snap:

```
sudo apt install snapd -y
sudo snap install core
sudo snap refresh core
sudo snap install --classic certbot
```
Secure via:

```
sudo certbot --nginx -d project-june.xyz -d www.project-june.xyz
```

## ✅ Troubleshooting

| Issue                      | Solution                                    |
| -------------------------- | ------------------------------------------- |
| Domain shows Nginx welcome | Disable default site, enable your config    |
| `Permission denied` in SSH | Check your key permissions & correct user   |
| Certbot DNS timeout        | Ensure DNS records are correct & propagated |
| Can’t connect on ports     | Open port 443 in EC2 Security Group and make sure that your personal nginx config redirects port 80 to https   |
| ssh timeout                | Create a new instance and attach the 'original instance' volume to it as a secondary volume fix nginx and ssh issues, ensure that ufw.conf 'ENABLED=no'this allows you ssh in back in from the 'original instance' |
| ufw issues                 | chroot into Ec2 server ```ufw allow .... openssh, 80, 443```  , ```sudo ufw allow enable```


# Rendered-Image
![Screenshot (2)](https://github.com/user-attachments/assets/ed3d0e28-cbc4-416f-9f02-8a3a5c1d48c9)

💡 Future Improvements
 * I would like to hear from you!!
