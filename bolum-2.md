
# Bilgisayar Ağları 3. Hafta

48-87 arası slaytlar burada anlatılmıştır.

## 1.4 Erişim Ağları ve Fiziksel Ortam

Soru: Uç sistemi sınır yönlendiricisine nasıl bağlanır?

- Yerleşim yerine ait erişim (residential access nets)
- İş veya eğitim kurumu erişimi (institutional access networks)
- Kablosuz erişim (mobile access networks)

HATIRLA:
Erişim ağının bant genişliği (bandwidth - saniyedeki bit sayısı - bps) nasıl bulunuyordu?
Paylaşma (shared) veya adanma (dedicated) neydi?

### Noktadan noktaya erişim

#### Çevirmeli modem (Dialup via modem)
- 56 Kbps hıza kadar yönlendiriciye (router) direk erişim sağlar.
- Aynı anda internette gezip telefonu kullanmaya izin vermez.

#### Asimetrik dijital abone hattı:  ADSL (asymmetric digital subscribler line)
- 50kHz’den 1 MHz banda kadar yüksek hızlı aşağı akım (downstream) kanalı vardır.
- 4kHz’den 50kHz banda kadar orta hızlı yukarı akım (upstream) kanalı vardır.
- 0 ile 4 kHz bant arasında sıradan iki yönlü telefon kanalı vardır.
- Adından anlaşılacağı gibi asimetrik bir bağlantıdır. İndirme ve gönderme hızları eşit değildir.
 
### Kablo modem altyapısı
- Melez fiber eş eksenli kablo kullanır: **HFC** (Hybrid Fiber Coax)
  - **Asimetriktir:** 30Mbps a kadar downstream (yüksek hızlı aşağı akım), 2 Mbps e kadar upstream (yüksek hızlı yukarı akım) kullanır.
- Kablo ve fiber ağ evleri ISS yönlendiricilerine bağlar
  - Evler yönlendiricilere erişimi paylaşır
- Kurulum: Kablo TV aracılığı ile yapılır.

![HFC Yapısı](https://i.resimyukle.xyz/1OyM4H.png)

### Yerel Alan Ağı / Şirket Erişimi
Şirketlerde veya üniversite kampüslerinde bir uç sistemi sınır yönlendiricisine bağlamak için yerel alan ağı (LAN) kullanılır.
- Ethernet:
  - Uç sistem ve yönelndiricileri (routers) ortak veya adanmış olarak birbirine bağlar.
  - 10 Mbps, 100Mbps, Gigabit Ethernet

### Kablosuz erişim ağları
- Paylaşımlı kablosuz erişim ağı uç sistemleri yönelndiriciler (routers) ile bağlar.
  - Temel istasyon (base station) ya da erişim noktası (access point)
- Kablosuz Local Area Networkler
  - 802.11b (WiFi): 11Mbps
- Geniş alan kablosuz erişim ağı (Wider area wireless access)
  - Bir telekomünikasyon sağlayıcısı tarafından yönetilir.
  - 3G ~ 384kbps
  - WAP/GPRS in Europe

### Ev ağları
Tipik ev ağı bileşenleri:
- ADSL veya kablo modem
- Yönlendirici (router)/firewall/NAT
- Ethernet
- Kablosuz erişim noktası (Wirelss Access Point)

### Fiziksel Ortam
- Bit: Alıcı ve verici çiftleri arasında seyahat eder.
- Fiziksel hat: Alıcı ve verici arasındaki hat.
- Kılavuzlu ortam (Guided media)
  - Dalgalar düz bir ortam boyunca gider: Bakır, fiber, eş eksenli
- Kılavuzsuz ortam (Unguided media)
  - Dalgalar yayılır: Radyo sinyalleri

#### Çift Sarımlı (Twister Pair, TP)

#### Eş ekesenli kablo
- İki ortak merkezli bakır iletken
- İki yönlü (bidirectional)
- Baseband
  - Tek kanal
- Broadband
  - Kablo üzerinde birden fazla kanal bulunur.
  - HFC (Hybrid Fiber Coax)

#### Fiber optik kablo:
- Cam fiber ışık darbesini iletir, her darbe bir biti temsil eder.
- Yüksek hızlı noktadan noktaya iletim sağlar
- Düşük hata oranı vardır. Repeaterlar uzak yerleştirilir. Elektromanyetik girişimden etkilenmezler.

#### Radyo
- Sinyal, elektromanyetik spektrum içerisinde taşınır.
- Kablosuz iletim sağlar
- İki yönlüdür (bidirectional)
- Yayılma ortamına bağlıdır:
  - Yansıma (reflection) yapar.
  - Nesneler tarafından engellenebilir
  - Girişim (interference)

#### Uydu radyo kanalları:
- Yeryüzü tabanlı mikrodalga (terrestrial microwave)
  - Örnek: 45 Mbps'e kadar olan kanallar
- LAN (Örnek: Wifi)
  - 2Mbps, 11Mbps
- Geniş alan (wide-area) (Örnek: Hücresel Veri)
  - Örnek: 3G, yüzlerce kbps
- Uydu (satellite)
  - 50Mbps'e kadar olan kanal (veya daha küçük kanallar)
  - 270 milisaniye uçtan uca gecikme
  - Coğrafi istasyon ya da düşük dünya yörüngesi (geosynchronous versus low altitude)

## 1.5 İnternet yapısı ve internet servis sağlayıcıları
Kabaca hiyeraşiktir.

![ISS](https://i.resimyukle.xyz/QxJ028.png)

#### Kat 1 ISS
Merkezdeki internet servis sağlayıcılarıdır. Ulusal veya uluslar arası kapsamdadırlar.
- Birbirlerine eşit davranırlar
- Örnek: UUNet, BBN/Genuity, Sprint, AT&T
- Kat 1 sağlayıcıları birbirlerine özel olarak bağlanırlar.
- Kat 1 sağlayıcılar genel ağ erişim noktalarına (NAPs) da bağlanırlar.

#### Kat 2 ISS
Daha küçük internet servis sağlayıcılarıdır. Genellikle bölgeseldirler.
Bir ya da daha fazla Kat-1 ISS e ve diğer Kat-2 ISS lere bağlıdırlar
- Kat 2 sağlayıcılar internet bağlantısı için Kat 1 sağlayıcılara para öderler. Kısaca, Kat 2'ler, Kat 1 sağlayıcıların müşterisidir.
- Kat 2 sağlayıcılar özel olarak birbirlerine ve genel ağ erişim noktalarına  (NAPs) bağlıdır.

#### Kat 3 ISS
Son kullanıcılara en yakın internet servis sağlayıcısıdır. Bu yüzden **Son hat ağ** da denir.
- Yerel ve Kat-3 internet servis sağlayıcıları, üstteki katlardaki servis sağlayıcıların müşterileridir ve onlar aracılığıyla Internet’e bağlanırlar.

## 1.6 Paket anahtarlama ağlarında gecikme, kayıp ve akış
Paketler ağ üzerinde yol alırken yönlendiricilerde düğümsel gecikmelere tabii olurlar.

### Düğümsel gecikme (Nodal delay)

![Gecikmeler](https://i.resimyukle.xyz/PIObeb.png)

**T**nodal = **T**proc + **T**queue + **T**trans + **T**prop
**T**gecikme = **T**işleme + **T**kuyruklama + **T**iletim + **T**yayılma

- **T**proc: İşleme gecikmesi. Paketin başlığını açıp, okuyup, bu paketi nereye göndermesi gerektiğine karar vermesi için geçen süre + pakette gelirken oluşmuş bit hatalarının belirlenmesi için geçen süre. Bu süre birkaç mikrosaniye civarındadır.
  - Bit hataları kontrol edilir.
  - Çıktı hattı belirlenir.
- **T**queue: Kuyruklama gecikmesi. Yönlendirici paketin hangi iletim hattına aktarılacağını belirledikten sonra ilgili hattın tamponuna koyar. Bekleyen başka paket olması durumunda paket sayısıyla orantılı bekleme süresine maruz kalır. Bu süre tıkanıklığa bağlı olarak değişir. Genellikle milisaniye civarındadır. Bekleyen paket yoksa sıfırdır.
  - İletim için çıktı tamponunda beklenen süre.
  - Yönlendiricinin (router) tıkanıklık düzeyine bağlıdır.
- **T**trans: İletim gecikmesi. Kuyruklamadan sonra, bu paketin iletim hattına bit by bit konulması gerekiyor. Bu aynı zamanda depola ve ilet gecikmesi olarak da adlandırılır. Paket boyutu (L)'ye ve aktarım oranına \(R\) bağlıdır. 
  - **L (Length):** Paketteki bit miktarı, paket uzunluğu (bits).
  - **R (Rate):** Bağlantının aktarım oranı, bant genişliği (bps).
  - **L/R:** Bitleri hatta göndermek için gerekli zaman. 
- **T**prop: Yayılma gecikmesi. Bir bit hatta iletildikten sonra bir sonraki düğüme doğru ilerler. Bit, hattın yayılma hızında yayılır. Bu hız, hattın fiziksel özelliğiyle ilişkilidir. Bu hız 2*10^8^ ve 3x10^8^ arasındadır. Kablonun uzunluğuna (D) ve ortamın yayılma hızına (S) bağlıdır.
  - **D (Distance):** Kablonun uzunluğu.
  - **S (Speed):** Ortamın yayılma hızı.
  - **D/S:** Yayılma gecikmesi.

### Gerçek internet gecikme ve yolları
#### Traceroute programı
Kaynaktan yönlendiricilere ve hedefe kadar gecikme ölçülerini verir.
- Hedefe ulaşacak 3 paket gönderir.
- Router paketleri göndericiye geri gönderir.

### Paket kaybı (Packet loss)
- Kuyruk (ya da tampon (buffer)) sınırlı kapasitededir.
- Paket dolu kuyruğa ulaştığında kabolur.
- Kaybolan paketin bir önceki düğüm ya da kaynak sistem tarafından yeniden gönderilmesi gerekebilir ya da hiç gönderilmeyebilir.

### Protokol katmanları ve servis modelleri
Ağlar karmaşıktır ve pek çok parçadan oluşur:
- Ana sistemler
- Yönlendiriciler
- Farklı ortam hatları
- Uygulamalar
- Protokoller
- Donanımlar ve yazılımlar

**Ağın yapısını organize edebilecek bir umut var mı?**
Var. Katmanlama kullanılarak basitleştiriliyor. Amaç, karmaşık sistemler ile baş etmek.
- Açık bir yapı karmaşık bir sistemin parçalarınına arasındaki ilişkileri tanımlamayı sağlar.
  - Tartışma için **katmanlı referans modeli**
- Modülerlik bakım ve sistemin güncellenmesini kolaylaştırır.
  - Herhangibir katmandaki bir servisin değişmesi sistem tarafında farkedilmez.
  - Örneğin kapı numaralarının değiştirilmesi sistemin geri kalanını değiştirmez.
- Katmanlama tehlikeli olabilir mi?

#### Katman fonksiyonları
- Hata denetimi: İki eş network elemanı arasındaki mantıksal bağlantının daha güvenilir olmasını sağlar.
- Akış Denetimi: Daha yavaş network eşlerinin kaldıramıyacağından fazla PDU ile şişirilmesini engeller.
- Parçalama ve Tekrar Birleştirme: Büyük veriyi daha küçük parçalara ayırır, gönderir ve tekrar birleştirilir.
- Çoklama: Bir çok üst seviye oturumunun (session) tek bir alt seviye bağlantısını paylaşmalarını sağlar.
- Bağlantı kurulumu: Ağ üstündeki eşle el sıkılmaya olanak tanır.

#### İnternet protokol yığını:
- **Uygulama Katmanı:** Ağ uygulamalarını destekler.
  - FTP, SMTP,  HTTP
- **Taşıma Katmanı:** Uç birimden uç birime veri transferi sağlar.
  - TCP, UDP
- **Ağ Katmanı:** Datagramların kaynaktan hedefe yönlendirilmesini sağlar.
  - IP, Routing Protocols
- **Bağlantı Katmanı:** Birbirine komş ağ elemanları arasında veri iletimi
  - PPP, Ethernet
- **Fiziksel Katman:** Hat üzerindeki bitlerle ilgilenir. Bu derste gösterilmeyecek.

Paketlere header eklenmesine **encapsulation (sarmalama)** denir.

Sarmalama örneği:
![Sarmalama](https://i.resimyukle.xyz/GCISaO.png)

# Özet
- Internet
- Protokol
- Ağ sınırı
- Ağ çekirdeği
- Ağ erişimi
- Paket anahtarlama
- Devre anahtarlama
- Internet/ISS yapısı
- Performans
  - Kayıp
  - Gecikme
- Katmanlama
- Servis modelleri