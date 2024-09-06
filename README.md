# League of Legends Data Collection Automation

This repository provides a setup guide for automating data collection from League of Legends using Python scripts, Docker, and cron jobs.

## 0. Preparation

1. Set the Timezone
   ```bash
   sudo timedatectl set-timezone Asia/Seoul
   date
   ```
2. Set Directory Permissions
   ```bash
   chmod -R u+rwx /home/gc/Desktop/ljh/src/lol/data/
   ```
3. Install ssmtp (if necessary, to resolve MTA warnings)
   ```bash
   sudo apt-get install ssmtp
   ```
## 1. Convert Jupyter Notebooks to Python Scripts
Convert the .ipynb files to .py scripts using the following commands:
   ```bash
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Challenger_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Grandmaster_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Master_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Diamond_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Emerald_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Platinum_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Gold_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Silver_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Bronze_API.ipynb
   sudo -E /home/gc/.local/bin/jupyter nbconvert --to script /home/gc/Desktop/ljh/src/lol/0_Iron_API.ipynb
   ```
## 2. Build Docker Images
Build Docker images for each rank using their respective Dockerfiles:
   ```bash
   docker build -f Dockerfile-base -t lol-base-image .
   docker build -f Dockerfile-Challenger -t lol-c .
   docker build -f Dockerfile-Grandmaster -t lol-gm .
   docker build -f Dockerfile-Master -t lol-m .
   docker build -f Dockerfile-Diamond -t lol-d .
   docker build -f Dockerfile-Emerald -t lol-e .
   docker build -f Dockerfile-Platinum -t lol-p .
   docker build -f Dockerfile-Gold -t lol-g .
   docker build -f Dockerfile-Silver -t lol-s .
   docker build -f Dockerfile-Bronze -t lol-b .
   docker build -f Dockerfile-Iron -t lol-i .
   ```
## 3. Set Up Cron Jobs for Automation
1. Start and Verify cron Service
   ```bash
   sudo systemctl start cron
   sudo systemctl status cron
   ```
2. Edit crontab
   ```bash
   crontab -e
   ```
3. Add the following cron jobs to run the Docker containers daily at 4:00 AM:
   ```bash
   00 04 * * * /usr/bin/docker run --rm -d --name lol-c -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-c
   00 04 * * * /usr/bin/docker run --rm -d --name lol-gm -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-gm
   00 04 * * * /usr/bin/docker run --rm -d --name lol-m -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-m
   00 04 * * * /usr/bin/docker run --rm -d --name lol-d -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-d
   00 04 * * * /usr/bin/docker run --rm -d --name lol-e -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-e
   00 04 * * * /usr/bin/docker run --rm -d --name lol-p -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-p
   00 04 * * * /usr/bin/docker run --rm -d --name lol-g -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-g
   00 04 * * * /usr/bin/docker run --rm -d --name lol-s -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-s
   00 04 * * * /usr/bin/docker run --rm -d --name lol-b -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-b
   00 04 * * * /usr/bin/docker run --rm -d --name lol-i -v /home/gc/Desktop/ljh/src/lol:/usr/src/app lol-i
   ```
## 4. View Docker Logs
To check the logs of a specific Docker container, use:
Replace <container_name> with the actual name of the container (e.g., lol-c, lol-gm, etc.).
   ```bash
   docker logs <container_name>
   ```

   ```bash
   # Configure logging
   log_folder = "/usr/src/app/data"
   os.makedirs(log_folder, exist_ok=True)
   logging.basicConfig(filename=os.path.join(log_folder, '1_Challenger_API.log'), 
                       level=logging.INFO, 
                       format='%(asctime)s - %(levelname)s - %(message)s')
   
   logging.info("Starting the script 1_Challenger_API.py")
   ```
