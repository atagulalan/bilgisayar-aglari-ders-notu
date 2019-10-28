## 3 Taşıma Katmanı

Hedefler:
- Taşıma katmanı servislerinin prensiplerini anlamak
  - oklama/Çoklamanın çözülmesi (multiplexing/demultiplexing)
  - Güvenilir veri iletimi (reliable data transfer)
  - Akış kontrolü (flow control)
  - Tıkanıklık kontrolü (congesiton control)
- İnternetdeki taşıma katmanı protokollerini öğrenmek
  - UDP: Bağlantısız taşıma (connectionless transport)
  - TCP: Bağlantı yönelimli taşıma (connection-oriented transport)
  - TCP tıkanıklık kontrolü (congestion control)

## 3.1 Taşıma Katmanı Servisleri ve Protokolleri
- Farklı ana sistemlerde çalışan uygulama süreçleri arasında **mantıksal bir bağlantı** sağlar.
- Taşıma katmanı protokolleri ağ yönlendiricilerinde değil, uç sistemlerde uygulanır
  - **Gönderici tarafı:** Gönderici uygulama süreci tarfından aldığı mesajları segmentlere çevirir ve ağ katmanına geçirir.
  - **Alıcı tarafı:** Segmentleri mesaj haline birleştirir ve uygulama katmanına geçirir.
- Uygulamalar için birden fazla taşıam katmanı protokolü mevcuttur.
  - TCP ve UDP

### Taşıma ve Ağ Katmanları
- Ağ katmanı: Ana sistemler arasında mantıksal bağlantı sunar.
- Tarnsport Layer: Farklı ana sistemler üzerinde çalışan süreçler arasında mantıksal bağlantı sunar.
  - Ağ katmanı üzerinde yer alır ve onun sunduğu servislere dayanır.

#### Ev halkı benzeştirmesi:
Birbirine mektup gönderen bir evdeki 12 çocuk ile diğerindeki 12 çocuk düşünelim.
- **Süreçler:** Çocuklar
- **Uygulama mesajları:** Zarf içindeki mektuplar
- **Ana sistemler:** Evler
- **Taşıma katmanı protokolü:** Ann ve Bill
- **Ağ katmanı protokolü:** Posta servisi

### İnternette taşıma katmanı protokolleri
Güvenilir, sıralı teslim (TCP)
  - Tıkanıklık kontrolü
  - Akış kontrolü
  - Bağlantı kurulumu
- Güvenimez, sırasız teslim (UDP)
  - IP'nin en iyi çabayla teslim servisi üzerinde bir eklenti yoktur.
- Uygun olmayan servisler
  - Gecikme garnatii
  - Bant genişliği garantisi

Uygulama | TCP | UDP
--- | --- | ---
Taşıma | TCP Servisi | UDP Datagramı
Ağ (IP) | Datagram | Datagram
Ethernet | Çerçeve | Çerçeve

### 3.2 Çoklama (Multiplexing) ve Çoklamanın Çözülmesi (Demultiplexing)
**Alıcı ana sistemde çoklamanın çözülmesi:** Alınan segmentlerin doğru soketlere teslimi
**Gönderici ana sistemde çoklama:** Pek çok paketten verinin alınması, verinin başlık ve zarflanması (daha sonra çoklamanın çözülmesinde kullanılmak için)

#### Çoklamanın çözülmesi (demultiplexing) nasıl çalışır?
- Ana sistem IP datagramınnı alır.
  - Her datagramın bir kaynak bir de hedef IP adresi vardır.
  - Her datagram 1 taşıma katmanı segmenti taşır.
  - Her segmentin kaynak ve hedef port numarası vardır. (Hatırla: Bazı ççok bilinen uygulamaların port numaraları)
- Ana sistem IP adresi ve port numarasını kullanark segmenti uygun sokete yönlendirir.

#### Bağlantısız çoklamanın çözülmesi

UDP soketler iki değişken tarafından tanımlanır.
- Hedef port numarası
- Hedef IP numarası

...


#### Bağlantı yönelimli çoklamanın çözülmesi

TCP soketler dört değişken tarafınadn tanımlanır.
- Hedef port numarası
- Kaynak port numarası
- Hedef IP numarası
- Kaynak IP numarası

...

> Aynı Port numarası dahi olsa, IP'ler farklı olduğundan benzersizlik sağlanır.

## Bağlantısız taşıma: UDP
- Bir taşıma protokolünün yapabilecği en az şeyi yapar.
- En iyiçaba teslim servisidir. 
- UDP Segmentleri
  - Kaybolabilir
  - Uygulamaya sırasız bir şekilde ulaşabilir
- Bağlantısız
  - UDP gönderici ve alıcısı arasında bağltnı kurulumu yotur
  - Her UDP segmenti diğerlrinden bağımsızo larak yürütülür.

Peki neden UDP var?
- Bağlantı kurulumu yok (gecikmeye yol açabilir)
- Basit: Gönderici ve alıcı taraflarında bağlantı durum yoktur.
- ...


- Genellikle multimedia uygulamalarında kullanılır: Kayıpların tolere edilebildiği ve hızın önemli olduğu uygulamalar.
- Diğer UDP kullanımları:
  - DNS
  - SNMP
- UDP üzerinden güvenilir iletim: Güvenilirlik uygulama katmanında eklenebilir.
  - Uygulamaya dayalı hata düzeltimi 

Uzunluk UDP segmentinin başlığı da kapsayan bit miktarı
... {resim eklenecek}

### UDP kontrol toplamı (Checksum)
Amaç: İletilen segmentteki hataları (örneğin değişen bitler) tespit etmek.

Gönderici:
- Segment içeriklerini 16 bitlik sözlükler olarak ele alır.
- Kontrol toplamı (checksum): Segment içeriğini 1 tümleyicinin toplamı olarak toplar.
- Gönderici UDP kontrol tplamı alanına kontrol toplamı değeri ekler.

Alıcı:
- Alınan segmentin kontrol oplamını hesaplar
...

Örnek:
İki 16 bit integerı toplayalım
----- false positive anlat


## 3.4 Güvenilir veri iletiminin prensipleri
- Sadece taşıma katmanında değil, uygulama ve bağlantı katmanlarında da meydana gelir.
- En önemli ağ konularının ilk 10 listesiin başında gelen bir konudur.
- Güvenilmeyen kanalın özellikleri güvenilir veri iletiminin (Reliable Data Transfer, RDT) karmaşıklığını belirler.
...

Güvenilir veri iletimi: Başlangıç
- Güvenilir veri iletimi protokolünü (RDT) adım adım oluşturacağız.
- Tek yönlü veri iletimi varsayalım
  - Fakat kontrol bilgisi her iki yönde de akar.
- Gönderici ve alıcıyı tanımlamak için sonlu durum makinesi kullanalım.

Durum: Bu "durumda" iken diğer durum sonraki olay ile belirlenir.


Stop and wait protocol: Verinin doğruluğunu kontrol eder. Eğer pakette bit hatası varsa aynı paketi tekrar yollar.