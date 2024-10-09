Worker çalıştırdığımız ekran içerisine giriyoruz
```
screen -r Rainbow

```
CTRL + C ile logları durduruyoruz

Yeni güncellemeyi yüklüyoruz 
```
cd

wget https://storage.googleapis.com/rbo/rbo_worker/rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz && tar -xzvf rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz

cp rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8/rbo_worker rbo_indexer_testnet/rbo_worker

#Dosyayı yetkilendiriyoruz

cd rbo_indexer_testnet && chmod +x rbo_worker

# Workerı yeniden çalıştırıyoruz

./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000
```
Gerekli dosyaları bilgisayarınıza yedekleyin

```
nano identity/identity.json

```
```
nano identity/private_key.pem

```
