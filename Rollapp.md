* roller kurdunuz kanal buldu mu ? evetse devam edelim
* faucete gönderme için artık kısa bir kodumuz var deneyelim .
```
roller tx fund-faucet
```
![image](https://github.com/molla202/Dymension/assets/91562185/0a0bed26-56b9-4874-8f98-2159ff631596)

* faucet hernekadar kapalı olsada sonucta açılacak bakiye gönderimini göirmek için
```
$balance dym1g8sf7w4cz5gtupa6y62h3q6a4gjv37pgefnpt5 <RollApp-ID>
```
* evet zurnanın zırt dediği yere geldik repoyu forklayalım
https://github.com/dymensionxyz/rollapp-registry
* sunucumuza geçelim. ve forkladığımız repoyu sunucuya çekicez alttaki buraya yazan yere kendi github adınızı yazıcaksınız
```
git clone https://github.com/BURAYA/rollapp-registry
```
```
cd rollapp-registry
```
Not: altaki rollap idniz roller çalıştırdığınızda yazıor zaten... BURAYA yazan kısma yazın
![image](https://github.com/molla202/Dymension/assets/91562185/0d58e837-73f4-4707-8f49-f93c519afc3a)
```
export ROLLAPP_ID=BURAYA
```
```
mkdir -p $ROLLAPP_ID/logos
cd $ROLLAPP_ID && touch $ROLLAPP_ID.json
```

* şimdi sunucumuzdaki dosyanın içine logo muzu atıcaz desteklediği uzantılar SVG, PNG, or JPG
* winscple yada mobo uzerinden buraya yazan yer sizin rollapp idniz adında klasör  `/root/rollapp-registry/BURAYA/logos/`
* şimdide yaptığımız ayarlamaları çıktı alalım.
```
roller config export
```
![image](https://github.com/molla202/Dymension/assets/91562185/e32fb431-e7ec-44ff-a30b-022400861e17)

* bu çıktıyı kaydedelim dursun.
* şimdide bu olusturduğumuz jsonu düzenleyeceğiz...

cd rollapp-registry

not: aşağıya buraya yazan yere sizin rollapp idnizi yazacaksınız mesel cd molla_456453-1 gibi idniz neyse o dosyaya giricez.

cd BURAYA

* json adınız rollap id adınız. BURAYA kısmına diyelim rollapp idniz molla_456453-1     nano molla_456453-1.json gibi yazıcaz anliyomusun mubarek... :D

nano BURAYA.json

* Aşağıdaki yerleri bulup ip adresini yazıcaksınız vps'in. sonra ctrl+x y enter dicez kaydedicez...

``"rpc": "http://IP-ADRES:26657"``

``"rest": "http://IP-ADRES:1317"``

``"rpc": "http://IP-ADRES.8545"``

* logoyu attık jsonu düzenledik.. geriye kaldı bu yaptıklarımızı kendi hesabımıza puşş etmeye puşş nasıl edilir çok puşş bi işlem :D

* githubunuza girin... sağ menuden resmine tıkla setting'e girin
![image](https://github.com/molla202/Dymension/assets/91562185/72e008f8-fd46-4e8e-8176-7e06e63f2043)
* sol altta developer settinge girelim
![image](https://github.com/molla202/Dymension/assets/91562185/42b63d38-f3b7-4732-b8d2-3f3015cd7fe3)
* sol menuden ``personel acces token diyelim açılan alt menıden classic diyelim
![image](https://github.com/molla202/Dymension/assets/91562185/87e561b8-5082-4900-8c8e-9507cd881abd)
* sağ üst menuden generate deyip yine classic seçelim
* açılan ekranda bi ad verelim alttaki tum kutuları tıklayıp en altaki generateye tıklayalım..
![image](https://github.com/molla202/Dymension/assets/91562185/6585fe18-8834-43d8-8802-93190208039a)

*çıkan kodu bir yere kaydedin bu bizim şifremiz unutmayın
![image](https://github.com/molla202/Dymension/assets/91562185/1a09b406-4501-44e3-82c3-4a3b49e6c38a)

* şimdi sunucumuzda hazırladığımız herseyi gthub repomuza puşşş edelim bize kullanıcı adı sorucak neyse onu yazın sonra şifre sorucak oda yukarıda yaptığımız classic token şeysi  vardıya kod onu yazıyoruz enter dıyoruz ve puş edıyor
```
git add .
git commit -m "added RollApp"
git push -u origin main
```
![image](https://github.com/molla202/Dymension/assets/91562185/27c38010-cf51-433c-8235-9e1c50b8f0d4)

* eğer hata alırsanız token olusturmada hata yapmısınızdır şöle der

![image](https://github.com/molla202/Dymension/assets/91562185/2d66acd5-26a0-4437-a4de-716890ee8218)

* artık githundan bakalım dosya gelmiş mi repoya sayfayı yenile
![image](https://github.com/molla202/Dymension/assets/91562185/45e20818-d8b7-4691-a2d4-2b6cda0042e2)









  
