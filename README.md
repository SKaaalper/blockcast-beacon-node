# Blockcast BEACON Node Setup Guide

![image](https://github.com/user-attachments/assets/94e9bef9-8fe4-436a-a129-05f541ff5682)

Guide: **How to [Buy a VPS Server](https://medium.com/@Airdrop_Jheff/guide-on-how-to-buy-a-vps-server-from-contabo-and-set-it-up-on-termius-0928e0e5cb5d) from Contabo and Set It Up Using Termius**

### Register Account:
Go to: [https://app.blockcast.network](https://app.blockcast.network?referral-code=SfD1Be)
- Use my Code: `SfD1Be`
- Connect your SOL wallet (Burner Wallet recommended)


| Component   | Requirement                                     |
| ----------- | ----------------------------------------------- |
| **CPU**     | 2-core Quad-core (e.g., Intel i5 or equivalent) |
| **Memory**  | 4 GB RAM or more                                |
| **Storage** | SSD with 20 GB+ available space                 |
| **Network** | 100 Mbps+ upload/download                       |
| **OS**      | Ubuntu 20.04 or later                           |

## Installation Steps:

1. Install Dependencies:
```
sudo apt-get update && sudo apt-get upgrade -y && \
sudo apt install -y curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev
```

2. Install Docker (If not installed):
```
sudo apt update -y && sudo apt upgrade -y

for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do
  sudo apt-get remove -y "$pkg"
done

sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

3. Clone the Repository:
```
git clone https://github.com/SKaaalper/blockcast-beacon-node.git
cd blockcast-beacon-node
```

4. Start the Node:
```
docker compose up -d
```
![image](https://github.com/user-attachments/assets/7f5797d3-9b58-403d-9553-468e2fb570a2)

5. Verify Running Services:
```
docker compose ps
```
You should see the following services running:
- blockcastd
- beacond
- control_proxy
- watchtower
![image](https://github.com/user-attachments/assets/60146836-808c-448d-8fc4-d2b14a2d6c92)

6. View Logs:
```
docker compose logs -fn 1000
```
![image](https://github.com/user-attachments/assets/3d7a6624-29c6-4ee2-ba4d-06bd0ffff4c2)

7. Generate Hardware ID & Challenge Key
```
docker compose exec blockcastd blockcastd init
```
Example output:
```
Hardware ID:
------------
c6ff0e6f-bc4d-4151-47c3-07df0e3cf53f

Challenge Key:
--------------
MCowBQYDK2VwAyEAXP49l4pBK1V5qy7vbRJYv3etRdEr7ycsQAvrgS+hQY0=

Register URL:
-------------
https://app.blockcast.network/register?hwid=c6ff0e6f-bc4d-4151-47c3-07df0e3cf53f&challenge-key=MCowBQYDK2VwAyEAXP49l4pBK1V5qy7vbRJYv3etRdEr7ycsQAvrgS%2BhQY0%3D
```
![image](https://github.com/user-attachments/assets/f26c9fe5-5fe3-4ba7-a4ab-875b58f97548)


📌 Backup your private key:
```
cat ~/.blockcast/certs/gw_challenge.key
```
![image](https://github.com/user-attachments/assets/608fba6f-f147-46d3-9dc4-7b682db23048)

8. Register Your Node:
Go to: [https://app.blockcast.network](https://app.blockcast.network?referral-code=SfD1Be)
- Connect your SOL wallet (Burner Wallet recommended)
- Go to `Manage Nodes`
- Click `Register Node`
- Enter your `Hardware ID` and `Challenge Key`
- Allow Location Access when prompted by your browser
- Save it!

![image](https://github.com/user-attachments/assets/a2201cb0-c604-40b3-8d42-9e7359e60404)

9. Verify Node Status
- Your node should show Healthy status within a few minutes
- Click on your node to view uptime, rewards, and connectivity

⚠️ **Important Notes**:
- **First Test: Node must be online for 6 hours**
- **Rewards Start: After 24 hours of continuous uptime**
- **You can run multiple nodes — no limit**

**Reference**:
Official Docs: [https://docs.blockcast.network/](https://docs.blockcast.network/main/getting-started/how-do-i-participate-in-the-network)



