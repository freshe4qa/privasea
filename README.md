<p align="center">
  <img height="100" height="auto" src="https://github.com/user-attachments/assets/2b478d54-eb60-4cef-ad3c-c558c7abd38d">
</p>

# Privasea Testnet

Official documentation:
>- [Validator setup instructions](https://docs.privasea.ai/)

Explorer:
>- [Explorer](https://deepsea-beta.privasea.ai)

### Minimum Hardware Requirements
 - 6x CPUs; the faster clock speed the better
 - 4GB RAM
 - 100GB of storage (SSD or NVME)

### Recommended Hardware Requirements 
 - 12x CPUs; the faster clock speed the better
 - 8GB RAM
 - 200GB of storage (SSD or NVME)

 - Ubuntu 22.04

Ставим ноду:

``sudo apt update && sudo apt upgrade -y``

``sudo apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev tar clang bsdmainutils ncdu unzip libleveldb-dev lz4 screen bc fail2ban -y``

``sudo apt-get install ca-certificates curl gnupg``

``sudo install -m 0755 -d /etc/apt/keyrings``

``curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg``

``sudo chmod a+r /etc/apt/keyrings/docker.gpg``

``echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null``

``apt install docker.io -y``

``sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin``

``docker pull privasea/acceleration-node-beta:latest``

``mkdir -p ~/privasea/config && cd ~/privasea``

``docker run --rm -it -v "$HOME/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore``

Придумываем пароль и вводим 2 раза:

![NVIDIA_Overlay_3ulapsRlad](https://github.com/user-attachments/assets/51d14946-bfe9-4f20-8bd6-19210864b87d)

Сохраняем node address и node filename:

![NVIDIA_Overlay_akUAwL7lEY](https://github.com/user-attachments/assets/9a39d82c-278a-4840-b1ff-c9aff0eb79dd)

Ваш приватный ключ хранится по пути - /root/privasea/config/UTC... данный файл можно скачать при помощи терминала Mobaxterm. Далее этот ключ можно импортировать в Metamask для дальнейших действий.

Выше мы сохраняли node filename. Нам нужно вписать вместо UTC Ваш UTC файл. Например: mv $HOME/privasea/config/UTC--2025-02-05T16-09-34.024190398Z--536272967a15b657d432db3b5c3dd993d6272bc3 $HOME/privasea/config/wallet_keystore

``mv $HOME/privasea/config/UTC $HOME/privasea/config/wallet_keystore``

Далее нам нужно получить тестовых $ETH в сети Arbitrum Sepolia через [кран](https://faucet.quicknode.com/arbitrum/sepolia) на тот адрес, который мы восстановили через приватный ключ. После этого переходим на [сайт](https://deepsea-beta.privasea.ai/privanetixNode), подключаем кошелек, нажимаем "Set one up now!", придумываем название ноды, выставляем 1% и вписываем адрес ноды, который сохраняли выше.

Теперь нужно включить ноду. Вместо PASS вписываете пароль, который придумывали ранее. Например: KEYSTORE_PASSWORD=qwerty123

![KZPJkdMREt](https://github.com/user-attachments/assets/22cb49ad-e8f0-483a-b532-f00fb0d6efd4)

``KEYSTORE_PASSWORD=ENTER_YOUR_KEYSTORE_PASSWORD && docker run -d --name privanetix-node -v "$HOME/privasea/config:/app/config" -e KEYSTORE_PASSWORD=PASS privasea/acceleration-node-beta:latest``

Далее запрашиваем тестовые $TPRAI через кран - https://deepsea-beta.privasea.ai/deepSeaFaucet и стейкаем на свой узел, нажимая "Stake".

Полезные команды:

Просмотр логов:

``docker logs -f privanetix-node``

Удалить ноду:

``docker stop privanetix-node``

``docker rm privanetix-node``

``rm -rf ~/privasea``
