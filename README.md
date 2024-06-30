<p align="center">
</p>
<h1>
<p align="center"> Analog </p>
</h1>


* Minimum Sistem Gereksinimleri

```console
Hardware: 8 vCPUs, 16 GB Ram, 300 GB Disk
Network: Port 9944
Network: 500 MBps
Ubuntu version 20.04 ya da 22.04. Sorunsuz olsun diyorsan 22.04

"Benim Contabo Vps3'te çalışıyor. Yanında 5 tane daha node kurulu. Sync olduktan sonra sıkıntısız ilerliyor Analog."
```


* Güncellemeleri yapalım

```console
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

* Docker kuralım

```console
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

* Docker bileşenlerini yükleyelim

```console
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

* Analog Timechain Docker görüntüsünü çekelim

```console
docker pull analoglabs/timechain
```

* Analog dizinini oluşturalım
```console
mkdir -p $(pwd)/.analog
```

* Analog docker container'ı çalıştıralım. 🐅
* Önemli: Moniker'i değiştirmeyi unutmayın. (Moniker, senin Telemetry üzerinde görünecek ismin olacak. Daha sonra form doldururken bilgilere ekleyeceğiz bunu.) (Parantezleri uçur 😁) 

```console
docker run -d -p 9944:9944 -p 30303:30303 -v $(pwd)/.analog:/.analog --name analog analoglabs/timechain --base-path /.analog --rpc-external --rpc-methods=Unsafe --unsafe-rpc-external --name (senin-moniker-ismin)
```


* Websocat'i yükleyelim

```console
curl -LO https://github.com/vi/websocat/releases/download/v1.7.0/websocat_amd64-linux
chmod +x websocat_amd64-linux
sudo mv websocat_amd64-linux /usr/local/bin/websocat
```

* Websocat kurulumunu Verify edelim

```console
websocat --version
```

* |websocat version 1.7.0 olmalı|

* Author_rotateKeys method ile "SESSION KEY'imizi" alalım. (Bunu saklayalım mı hocam dediğinizi duyar gibiyim 😁 ✅)


```console
echo '{"id":1,"jsonrpc":"2.0","method":"author_rotateKeys","params":[]}' | websocat -n1 -B 99999999 ws://127.0.0.1:9944
```


* Genellikle Node Sync olduktan sonra Moniker'iniz Telemetry üzerinde görünür. (Ben 4 gün bekledim ama ismim hiçbir türlü görünmedi. Neden? Sayfa içinde arama ile değil sıralama yapıp, isminizin baş harfinin olduğu bölgeye gelip, kontrol edin, Moniker'iniz ile bakışın 🐅) 

* [Telemetry](https://telemetry.analog.one/)




* Son işlemler için Polkadot.js'ye bağlanmamız gerekiyor
* Öncelikle Subwallet ile bir cüzdan açalım 🐅
* Daha sonra aşağıdaki link üzerinden siteye cüzdanımızı bağlayalım
* [PolkadotDashboard](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.testnet.analog.one###/accounts/)
* [Discord](https://discord.com/invite/analog/) adreslerine gidip Analog adresimize, Faucet'ten token alalım. (Analog adresimiz nerede hocam? Subwallet içerisinde, sağ üst kısımda "Customize asset display" bölümünden Analog Testnet ağını ekleyip, adresinizi alabilirsiniz)


### Token geldi mi? 😁 Eğer geldiyse birkaç işlemimiz daha olacak. 

* İlk olarak PolkadotDashboard sitesine gidelim.
* 




> Help me

* Logları kontrol etme
  
```console
docker logs -f analog
```
* Analog başlatma
```console
docker start analog
```
* Analog durdurma
```console
docker stop analog
```
docker pull analoglabs/timechain
```

