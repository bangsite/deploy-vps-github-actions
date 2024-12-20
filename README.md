## Deploy to VPS with github actions

Effortlessly deploy your projects to a VPS with GitHub Actions! This repository provides scripts and configurations to
set up Nginx, deploy web applications like Vue, Nuxt 3, React, and Next.js, and secure your sites with SSL using Certbot
on Ubuntu. Perfect for developers and system administrators to automate and simplify the deployment process for modern
web applications.

### Deploy scripts

- [x] Vue [View scripts](https://github.com/bangsite/deploy-vps-github-actions/tree/main/vue3)
- [ ] Nuxtjs [View scripts]()
- [ ] React [View scripts]()
- [ ] Nextjs [View scripts]()

### System and Environment Preparation

#### Server Setup
- Operating System: Ubuntu 20.04+ or CentOS 7+ recommended.
- Web Server: Install and enable Nginx.

```bash
sudo apt update && sudo apt install nginx -y  
sudo systemctl enable nginx && sudo systemctl start nginx

```

- Node.js: Install Node.js version 18 or later.

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install -y nodejs  

```

- PM2: Install PM2 globally for process management.

```bash
npm install -g pm2

```

#### GitHub Configuration

- Use the main branch (or customize it in your deploy.yml file).
- Add a GitHub Actions workflow file (deploy.yml) to automate deployment.
- Ensure your repository is properly connected to GitHub.

#### Source Code Configuration

- Add an ecosystem.config.cjs file to define the app's process management via PM2.
- Include build scripts in your package.json to prepare the application for deploymen

```bash
"scripts": {  
  "build": "npm run build",  
  "start": "pm2 start ecosystem.config.cjs"  
}  

```
### Deployment Workflow Overview

#### Setting Up GitHub Actions: 

The deploy.yml workflow file should include the following steps:
- Clone the repository from the specified branch (default: main).
- Install dependencies and build the project.
- Transfer files to the VPS via SSH.
- Restart the application using PM2.
  
#### Nginx Configuration: 
- Create or update the Nginx configuration file (/etc/nginx/sites-available/project.conf) for your project.
- Enable and restart Nginx:
  
```bash
sudo ln -s /etc/nginx/sites-available/project.conf /etc/nginx/sites-enabled/  
sudo nginx -t  
sudo systemctl restart nginx  

```
#### SSL Setup
Install SSL using Certbot:
```bash
sudo snap install certbot --classic  
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com  

```
### Contributions

Contributions to this project are welcome. Feel free to propose improvements or report issues via GitHub issues.

### License

MIT License by Bang
