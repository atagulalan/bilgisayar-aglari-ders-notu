# Bilgisayar Ağları 2. Hafta

1-47 arası slaytlar burada anlatılmıştır.

#### Open System Interchange (OSI) Referans Modeli
- Open Systems Interconnections

Bottom-up approach (Aşağıdan yukarı yaklaşım)
7 katmandan oluşur:
 1. Uygulama
 2. Sunum
 3. Oturum
 4. Taşıma
 5. Ağ
 6. Veri Bağlantı
 7. Fiziksel

![Bölümler](https://i0.wp.com/trnetwork.org/wp-content/uploads/2017/03/01_00_002_01_tr_OSI.katmanlari.jpg?resize=525,281)

#### TCP/IP Protokol Yığını
- Internet Protocol Stack

Top-down approach (Yukarıdan aşağı yaklaşım)
5 Katmandan oluşur:
1. Uygulama
2. Taşıma
3. Ağ
4. Veri Bağlantı
5. Fiziksel

### Konular
- 1.1 İnternet nedir?
- 1.2 Ağ sınırı
- 1.3 Ağ çekirdeği
- 1.4 Ağ erişimi ve fiziksel ortam
- 1.5 İnternet yapısı ve ISSler
- 1.6 Paket anahtarlama ağlarında gecikme, kayıp ve akış
- 1.7 Protokol katmanı ve servis modeli

## Bilgisayar ağı nedir?
Bilgisayar ağı, bilgisayarların bilgi ve kaynaklarını paylaşabilmeleri için oluşturulan yapıdır. 
- __En az iki__ bilgisayarı birbirine bağlayarak bir ağ oluşturulabilir.
- Bu ağ vasıtası ile bilgisayarlar birbirleri ile haberleşebilir.

__Leonard Kleinrock__ internet bağlantısının temeli olan _Paket Anahtarlama_ Teorisini geliştirdi.

### Network çeşitleri

 - Local Area Network (LAN)
 - Metropolitan (MAN)
 - Wide (WAN)
 - Personal (PAN)
 
 LAN: Şirket/üniversite yerel alan ağları uç sistemleri sınır yönlendiricilere bağlar. Kampüs veya şirketin içerisinde olabilir.
 MAN: Yerel alan ağları ile aynı, ancak daha büyük (şehir kadar). Yerel televizyon (kablolu televizyon) ağları, kampüs ağı.
 WAN: Kıta/Ülke kadar büyük alan ağları. İnternet.
 PAN: Evimizde oluşturduğumuz, birkaç bilgisayarı, yazıcıyı bağladığımız alan ağları. Kişisel alan ağı.

## 1.1 İnternet nedir?
Ağların ağı, birçok ağın biraraya geliştirerek oluşturduğu yapı.

Bilgisayarlar arasında bilgi, çeşitli protokollere göre paketler halinde gönderilir.

İnternet kavramına iki farklı şekilde yaklaşılabilir:
- Nuts and bolts (Temellere odaklı): İnterneti meydana getiren temel donanım ve yazılımların tümü.
- Servis yaklaşımı: Uygulamalar için servisler sunan bir altyapı.

### Temellere odaklı
Uç sistemlerin toplandığı tüm cihazlar: 
 - TV'ler
 - PC'ler
 - Ev elektronikleri
 - Sunucular
 - PDA'lar
 - Akıllı telefonlar
 - IP Resim çerçevesi
 - Ekmek kızartıcısı
 - İnternet telefonları

#### Temellere odaklı yaklaşım birimleri
 - __Aygıtlar:__ Milyonlarca birbirine bağlı hesaplama aygıtı var. Bunlara hosts (ana sistemler) veya end systems (uç sistem) denir.
 - __Yönlendiriciler (routers):__ Paketleri iletir (veri yığını)
   -  __Paket anahtarlama__: Ağda aktarılan verilere paket denir. Adanmış bir yol kullanmak yerine yönlendiricinin yardımı ile yol bulunur.
 - __İletişim bağlantıları (communication links):__ Bu aygıtları birbirine bağlamak için kurulan bağlantılar.
   - Fiber optik lif, bakır tel, radyo dalgası
   - Aktarım hızı = bandwith bits/sn - bps
- __Protokoller:__ Mesajların gönderilmesini ve alınmasını tanımlar.
  - TCP
  - IP
  - UDP
  - HTTP
  - FTP
  - PPP
- __Internet Servis Sağlayıcılar (ISS, ISP):__ Uç sistemleri birbirine bağlar. 


#### Intranet
  - Özel, genele açık olmayan ağ. İnternet ile aynı altyapıyı kullanır.
- **İnternet: "ağların ağı (network of networks)"**
  - Hiyeraşik
  - İnternet servis sağlayıcılar (ISP)
  - *Genel İnternet* ve *Özel İntranet*
- Internet standartları
  - __RFC:__ Reqest for Comments
  - __IETF:__ Internet Engineering Task Force
İnternet Mühendisliği Görev Grubu, İnternet protokollerini geliştiren ve standartlaştıran, resmî statüsü olmayan bir gruptur. IETF'nin çalışmaları ve ürettiği dokümanlar İnternet üzerinden herkese açıktır. Çalışma gruplarına ve toplantılarına katılım için herhangi bir kısıtlama bulunmamaktadır.

Tüm RFClerin listesi: http://www.ietf.org/iesg/1rfc_index.txt

#### Protokol nedir?
İnsan protokolleri
- Saat kaç?
- Bir sorum var
- Başlangıç - Merhaba

Spesifik bir mesaj gönderilir, bu mesaja göre muhabbet başlatılır.

Bir __protokol__, iletişim halinde iki ya da daha fazla bilgisayar ortamı varlığı arasında gönderilip alınan mesajların biçim ve sıralamasını ve bir mesajın alınması ya da gönderilmesi durumunda yapılması gereken eylemleri belirler.

### Servis Odaklı Yaklaşım
Dağıtık uygulamalara servis sağlayan iletişim altyapısı:
- Web, e-posta, oyunlar, e-ticaret, dosya paylaşımı
- Birden fazla uç sistem içerir.
  - İstemci / Sunucu
  - Eşler Arası (P2P)

Uygulamalara sağlanan iletişim servisi:
- Connetionless (unreiable): Bağlantısız, güvenilmez
- Connection Oriented (reliable): Bağlantı yönelimli, güvenilir
  - TCP (Transmission Control Protocol)

 

## 1.2 Ağ Sınırı

### Bağlantı-Yönelimli Servis (Connection Oriented)
Her iki serviste de amaç, uçbirimler arası veri iletimi
- Handshaking: Veri iletimine önceden hazırlanma
  - İnsan protokolü
    - +Merhaba
    - -Sana da merhaba
  - İki iletişim uç biriminde durumu (state) ayarlamak
 - TCP - Transmission Control Protocol
   - İnternetin bağlantı temelli servisi
 
#### TCP Servisi (RFC 793)
Güvenilir, sıralı byte-stream veri transferini sağlar.
- Paket transferi öncesi uç sistemler arasında kontrol sağlanır.
- Paketler ile iletişim sağlanır.
- Bağlantı sanal / gevşektir. Paket iletiminden yalnızca uç sistemler haberdar.
- Paketin kaynaktan hedefe tam, doğru ve sıralı teslimini garantiler.

##### Özellikleri
- Kayıp (loss): _Doğrulama_ (acknowledgements) ve _tekrar gönderme_ (retranmisions) sağlar.
- Akış (flow) kontrolü: Gönderici alıcıyı _boğmaz_. Göndericinin gönderim hızını, alıcının alabildiği hıza göre ayarlar.
- Tıkanıklık (congestion) kontrolü: Ağ tıkandığında gönderici gönderme hızını _azaltır_.


### Bağlantısız Servis (Connectionless)
Her iki serviste de amaç, uçbirimler arası veri iletimidir.

#### UDP Servisi (RFC 768)
Hiçbir servis sağlamaz. (Buraya sonraki derslerde değinilecek. Hiçbir servis sağlamıyorsa neden kullanıyoruz?)
- Bağlantısız
- Güvenilir olmayan (unreliable veri iletimi)
- Akış kontrolü yok
- Tıkanıklık kontrolü yok

### Uygulamalar

##### TCP Kullanan uygulamalar:
- HTTP
- FTP
- TELNET
- SMTP

##### UDP Kullanan Uygulamalar
- Streaming media
- Telekonferanslar
- DNS
- Internet telefonları

## 1.3 Ağ çekirdeği

### Ağ sınıflandırılması
- Telekomünikasyon Ağları
  - Devre Anahtarlama Ağları
    - FDM
    - TDM
  - Paket Anahtarlama Ağları
    - VC Ağları
    - Datagram Ağlar

### Devre anahtarlama
Kaynakların rezerve edildiği durum. Devre, ona bağlı anahtar ve belil bir bant genişliğine bir iletim çiftine adanır.
Rezervasyonlu restoran örneği: Her zaman sizin için yeri var, hizmet anında gelir.
- Hat bant genişliği, anahtar kapasitesi (switch capacity)
- Adanmış kaynaklar: __Paylaşım yok__
- Devre performansı (garantili iletim)
- Bağlantı tesisi gerekli
- Network kaynakları (bandwith) parçalara bölünür.
  - Parçalar bağlantılara atanır
  - Adanmış devreler kullanılmadığı zaman boş kalır
 
#### FDM (Frequency Division Multiplexing)
Bant genişliği frekanslara ayrılır. __Frekans spekturumu__, hat üzerinde kurulan bağlantılara paylaştırılır.
Örnek: Geleneksel telefon ağları.

##### Dezavantajları
- Sessiz zamanlarda kaynaklar boşa harcanır.
- Kurulumu oldukça karmaşık ve maliyetlidir.

#### TDM (Time Division Multiplexing)
Zaman, sabit boyutlardaki __zaman dilimlerine (çerçevelere)__ bölünür. Her bir çerçeve bellli sayıda __zaman yuvasına__ ayrılır.
- Zaman çerçevelerine ayrılır
- Her çerçeve içerisinde zaman yuvaları belirlenir
- Yuvalar iletim çiftlerine atanır

##### Örnek:
 640.000 bitlik bir dosyayı A sisteminden B sistemine devre anahtarama ağında göndemek ne kadar sürer?
- Tüm hatlar 1,536 Mbpsdir.
- Her hat 24 yuvalık (slot) TDM kullanır
- Baştan sona devreyi kurmak için gerekli zaman 500 milisaniyedir.

##### Çözüm:
- R: 1536 Kbps
- Her bağlantı 24 yuva/sn
- Devre oluşturma süresi = 0.5sn
- Her devre 1536 Kbps/24 = 64Kbps iletim hızına sahip olur.
- Bu veri, 640.000/64.000 = 10sn'de iletilir.
- Toplam geçen süre: 10+0.5 = 10.5sn 


### Paket anahtarlama
Fiziksel olarak yaklaşık en yüksek veri aktarım hızına yakın bir hız ile paketlerin iletimi sağlanabilmektedir.
- Kaynak, uzun mesajları paket adı verilen küçük veri parçalarına böler.
- A ve B kullanıcılarının paketleri aynı ağ kaynaklarını kullanır.
- Her paket bant genişliğinin tamamını kullanır.
- Kaynaklar ihtiyaç duyuldukça kullanılır.

#### Özellikleri
- Kaynak mücadelesi: Toplam kaynak ihtiyacı varolan miktarı aşabilir.
- Tıkanıklık: Paket kuyrukları ve hat kullanımı için bekleme olabilir.
- Depola ve ilet (Store and forward): Anahtar iletmeye başlamadan önce paketin tamamı alınmalıdır.

#### Depola ve İlet
- L bitlik paketi R bps lik bir hat üzerinde iletmek için L/R saniye gereklidir
- Bir sonraki hatta iletilmeden önce paketin tamamının yönlendiriciye ulaşmış olması gereklidir

##### Örnek
![enter image description here](https://i.resimyukle.xyz/bfIGC8.png)
L = 7.5 Mbits
R = 1.5 Mbps
Gecikme = **Toplam bağlantı sayısı * (L / R)** saniye
Gecikme = 3 * (7.5/1.5) = 15 saniye

#### İstatistiksel Çoklama
Göndericilerin paketleri belli bir şekil ve düzen ölçüsünde takip etmeden yönlendiricilerden göndermektedir. **TDM ile zıttır.**

##### Avantajları
- Bant genişliği paylaşımı etkinleştirir.
- Daha basit ve ucuzdur.

##### Dezavantajları
- Gerçek zamanlı uygulamalar için yetersizdir.

A ve B paketlerinin sabit bir sırası yoktur.
![enter image description here](https://i.resimyukle.xyz/5zW12c.png)

#### Sanal Devre Ağlar
Devre anahtarlama ağlar gibi davranır. Kaynak ve hedef arası aynı paket anahtarları kullanılır, ancak kota rezervasyonu yoktur.
Paketler, sanal devre etiketlerini kullanır.
Sanal devre ağlarda bağlantı kurulması belirlenen yol daha sonra değişmez.?????

#### Datagram Ağlar
Ne bağlantılı, ne bağlantısızdır. Paket başlığındaki hedef adres, IP adresidir.


Paket anahtarlama **"kesin kazanan"** mıdır?
- Çok fazla veri için uygundur
  - Kaynak paylaşımı
  - Basit, bağlantı kurumuna gerek yoktur
- Fazla tıkanıklık (congestion): paket gecikmesi ve kaybı
  - Güvenli veri iletimi ve tıkanıklık kontrolü iiçin protokoller gereklidir
- Soru: Devre kurulmuş gibi davranması nasıl sağlanabilir?
  - Ses ve görüntü uyglamaları için bant genişliği garantisi gereklidir.
  - Hala çözülememiş bir problemdir.
