## Tenderduty is a comprehensive monitoring tool for Tendermint networks.
#### This monitoring allows TenderDuty to monitor the behind the nodes and, in particular, to see the network height, validator status, uptime, signed and skipped blocks. It is also possible to connect notifications to telegrams and discord

![1 (1)](https://user-images.githubusercontent.com/44331529/189982005-b4e0fe45-36a5-4a24-b824-eef923be2f11.png)
![1 (2)](https://user-images.githubusercontent.com/44331529/189982018-5cf5d687-d221-4e23-accb-a277696d6b38.png)

## Server preparation
```bash
sudo apt update && sudo apt upgrade -y &&
sudo apt install curl build-essential git wget jq make gcc tmux htop nvme-cli pkg-config libssl-dev lib
```

## Install docker 
```bash
apt update && \
apt install apt-transport-https ca-certificates curl software-properties-common -y && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && \
apt update && \
apt-cache policy docker-ce && \
sudo apt install docker-ce -y && \
docker --version
```

## Install tenderduty
```bash
tmux new-session -S tenderduty
mkdir tenderduty && cd tenderduty
docker run --rm ghcr.io/blockpane/tenderduty:latest -example-config >config.yml
```

## Editing the configuration
```bash
nano $HOME/tenderduty/config.yml
```
### For simple monitoring without notifications, just change in the config:

+ network name:
+ chain-id:
+ valoper_address:
+ RPC url:

<details>
  <summary> screenshots </summary>
  
  ![con (1)](https://user-images.githubusercontent.com/44331529/189982668-1af71d13-aa62-407d-b0c1-8a6fa6074f65.png)
  ![con (2)](https://user-images.githubusercontent.com/44331529/189982691-bfc8acc0-3e28-4a4c-a3a7-f08b9bce469d.png)
</details>

<details>
  <summary>🟢If you need multiple nodes - just copy the same data below and edit it like in the screenshot below. </summary>

  ![multi](https://user-images.githubusercontent.com/44331529/189982855-8b2f3ba8-8b39-4227-8a59-4d226c9f2c5c.png)
</details>

## Start
```bash
docker run -d --name tenderduty -p "8888:8888" -p "28686:28686" --restart unless-stopped -v $(pwd)/config.yml:/var/lib/tenderduty/config.yml ghcr.io/blockpane/tenderduty:latest
```
`logs`
+ docker logs -f --tail 20 tenderduty

## Let's check our monitoring in the browser
```bash
echo -e "\033[0;32mhttp://$(wget -qO- eth0.me):8888/\033[0m"
# Exmp - http://1.2.3.4:8888/
```

## Useful Commands

`stop the container`
+ docker stop tenderduty

`restart the container`
+ docker restart tenderduty

`logs`
+ docker logs -f --tail 20 tenderduty


