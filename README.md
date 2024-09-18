## Rainbow

> evet ödüllü - beklentisiz kurulum, taktir sizin.

> Donanım 4 GB-ram / 50 GB-disk.

### Kurulum

```console
# komutlarımızı tek tek giriyoruz.
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# docker kurulumu
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
sudo systemctl start docker
sudo systemctl enable docker

# rainbow kurulumu
mkdir -p /root/project/run_btc_testnet4/data
git clone https://github.com/rainbowprotocol-xyz/btc_testnet4
cd btc_testnet4

sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
```console
# bitcoin cli kurulumu

docker-compose up -d
docker exec -it bitcoind /bin/bash

# ruesct yazdığım yerlere kendi bilgilerinizi giriniz. (totalde 3 kısım)
bitcoin-cli -testnet4 -rpcuser=ruesct -rpcpassword=ruesct -rpcport=5000 createwallet ruesct

# burada 2 kısma giriyoruz bilgilerimizi ve kaydediyoruz adresi.
bitcoin-cli -testnet4 -rpcuser=ruesct -rpcpassword=ruesct -rpcport=5000 getnewaddress
```

> Sunucumuza çık gir yapalım.

```console
git clone https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet && cd rbo_indexer_testnet

wget https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker
chmod +x rbo_worker

# bu dosayaya girelim
nano docker-compose.yml
# altta verdiğim komutu düzenleyerek içine yapıştırın.
```

> user ve password değişmeniz simdilik yeterli.

```console
version: '3'
services:
  bitcoind:
    image: mocacinno/btc_testnet4:bci_node
    privileged: true
    container_name: bitcoind
    volumes:
      - /root/project/run_btc_testnet4/data:/root/.bitcoin/
    command: ["bitcoind", "-testnet4", "-server","-txindex", "-rpcuser=demo", "-rpcpassword=demo", "-rpcallowip=0.0.0.0/0", "-rpcbind=0.0.0.0:5000"]
    ports:
      - "8333:8333"
      - "48332:48332"
      - "5000:5000"
```

```console

# buradan container id alıyoruz bitcoin-cli olan.
docker ps

# id kısmını doldurup kaldırıyoruz.
docker stop id
docker rm id

# tekrar başlatalım yeni compose ile.
docker-compose up -d
````

```console
# screen açıyoruz
screen -S Rainbow

# gerekli 2 bilgiyi dolduruyoruz
./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000

# CTRL A D ÇIKIŞ
```

> nano `nano ./identity/principal.json` komutu ile [explorer](https://testnet.rainbowprotocol.xyz/explorer) girip submit ediyoruz


<img width="437" alt="Ekran Resmi 2024-09-08 22 14 56" src="https://github.com/user-attachments/assets/b71c6f71-0a8f-42d7-83d8-6a6024841334">


> `nano ./identity/private_key.pem` bu dosyayı da saklayalım.

> İşlemler bu kadar. Incentivize indexer çalışıyor.




