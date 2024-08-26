# lol-data-collector
Automated data collection pipeline for League of Legends using Python, Docker, and cron jobs.

# League of Legends Data Collection Automation

This repository provides a setup guide for automating data collection from League of Legends using Python scripts, Docker, and cron jobs.

## 0. Preparation

1. **Set the Timezone**
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

