## Taşıma Katmanı

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

Ağ katmanı: İki uç sistem arasında teslim servisi sunar.
Taşıma katmanı: İki uç sistem üzerinde çalışan uygulama süreçleri arasında teslim servisi sunar.

Uygulama süreçleri arasında mantıksal bağlantı sağlar.
Mantıksal Bağlantı: Sanki süreçleri çalıştıran ana sistemler birbirine direk bağlı gibi.



## 3.1 Taşıma Katmanı Servisleri ve Protokolleri
- Farklı ana sistemlerde çalışan uygulama süreçleri arasında **mantıksal bir bağlantı** sağlar.
- Taşıma katmanı protokolleri ağ yönlendiricilerinde değil, uç sistemlerde uygulanır
  - **Gönderici tarafı:** Gönderici uygulama süreci tarfından aldığı mesajları segmentlere çevirir ve ağ katmanına geçirir.
  - **Alıcı tarafı:** Segmentleri mesaj haline birleştirir ve uygulama katmanına geçirir.
- Uygulamalar için birden fazla taşıam katmanı protokolü mevcuttur.
  - TCP ve UDP

### Taşıma ve Ağ Katmanları
- Ağ katmanı: Ana sistemler arasında mantıksal bağlantı sunar.
- Transport Layer: Farklı ana sistemler üzerinde çalışan süreçler arasında mantıksal bağlantı sunar.
  - Ağ katmanı üzerinde yer alır ve onun sunduğu servislere dayanır.


##### Ağ katmanı
- En iyi çabayla iletim servisidir. (Best effort)
- Taşıma katmanı segmentlerini teslim etmek için elinden gelen en iyisini yapar, ama garanti vermez.
- Yani, güvenilmez (unreliable) bir servistir.
- Ağ katmanı protokolü: IP ile sağlanır.

##### Taşıma katmanı
- İki uç sistem arasındaki IP'nin teslim servisini, uç sistemler üzerinde çalışan iki sürecin arasındaki teslim sürecine genişletir.

Ana sistemden ana sisteme teslimi, süreçten sürece teslime çevirmeye **Multiplexing (Çoklama)** ve **Demultiplexing (Çoklamanın Çözülmesi)** denir.

UDP | TCP 
--- | ---
Multiplexing / Demultiplexing | Multiplexing / Demultiplexing
Doğruluk Kontrolü | Doğruluk Kontrolü
Yok | Güvenilir veri iletimi (Bağlantı kurulumu, tıkanıklık kontrolü, akış kontrolü)
Bağlantısız, güvenilmez servis | Güvenilir, bağlantı-yönelimli servis

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

Gönderici (Multiplexing): Farklı süreçlerden gelen veriler toplanır, header (başlık) bilgileri ile zarflanır, segmentler oluşturulur ve ağ katmanına iletilir.

Alıcı (Demultiplexing): Taşıma katmanı protokolü, ağ katmanından gelen segmentteki belli alanlara bakar, alıcı sürece karar verir ve segmenti süreçle ilgili sokete ileterek gönderir.

Gelen verinin hangi sürece ait oldğunu gösteren segment başlığında bir grup alan bilgisi vardır. Bunlar, kaynak ve hedef port numaralarıdır. Port numaraları 0-65535 arasında değişen 16 bitlik sayılardır.

0 ile 1023 arasındakiler bilinen uygulamalara atanmıştır.

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

### UDP ile Multiplexing / Demultiplexing

A sunucusu | B sunucusu
--- | ---
Kaynak IP: A | Kaynak IP: B
Kaynak Port: 9157 | Kaynak Port: 46428

Üstteki örnek için, A sunucusundan B sunucusuna bir veri gönderelim.

Gönderi | 
---
Hedef IP: B | 
Hedef Port: 46428 | 

UDP soketi: Bir hedef IP ile bir hedef port numarası ile tanımlanır. Sonuçta da farklı adres ve/veya kaynak port numarası olan IP datagramları hedef port numarası ayın ise aynı sokete yönlendirilir.

### TCP ile Multiplexing / Demultiplexing

A sunucusu | B sunucusu
--- | ---
Kaynak IP: A | Kaynak IP: B
Kaynak Port: 9157 | Kaynak Port: 46428

Üstteki örnek için, A sunucusundan B sunucusuna bir veri gönderelim.

Gönderi | 
---
Kaynak IP: A | 
Kaynak Port: 9157 |
Hedef IP: B | 
Hedef Port: 46428 | 

Üstte görüldüğü gibi, UDP soketinde yalnızca 2 değişken gerekirken (Hedef IP ve Hedef Port), TCP soketinde 4 değişken tanımlanır (Kaynak IP, Hedef IP, Kaynak Port, Hedef Port).

Aynı hedef port numarasına sahip segmentler geldiğinde, aynı kaynak port numarasına ya da kaynak IP'ye sahip olsalar bile her biri için ayrı soket açılır ve bu soketlere yönlendirilirler.

> Öğrendin: Segmentler soketlere yönlendirilirler.

### UDP segment yapısı
2 Bayt (16 bit) | 2 Bayt (16 bit)
| -------------  | ------------ |
| Kaynak Port #  | Hedef Port # | 
| Uzunluk        | Checksum     |
|          32 Bitlik veri       |

Kaynak ve hedef port, mutliplexing ve demultipleing için kullanılır.
Kontrol toplamı (Checksum): Veride hata olup olmadığının kontrolünü sağlar.
Uzunluk (Length): Header dahil o segmentin boyutunu ifade eder.

### UDP kontrol toplamı (Checksum)
Amaç: İletilen segmentteki hataları (örneğin değişen bitler) tespit etmek.

Gönderici:
- Segment içeriklerini 16 bitlik sözlükler olarak ele alır.
- Kontrol toplamı (checksum): Segment içeriğini 1 tümleyicinin toplamı olarak toplar.
- Sonuç UDP segmentindeki checksum alanına yazılır.
- Gönderici UDP kontrol tplamı alanına kontrol toplamı değeri ekler.

Alıcı:
- Alınan segmentin kontrol toplamını hesaplar (sözcükler toplanır).
- Sonra checksum alanındaki değer ile de toplama işlemi gerçekleştirilir.
- Toplam sonucunda 0 var ise veride hata var demektir. Segment atılır (DUMP).
...

Örnek:
İki 16 bit integerı toplayalım

Toplam |
--- |
01010101 |
01110000 |
+ |
11000101 | 
01001100 |
+ |
00010010 |
00000001 |
+ |
00010010 |

Toplamın 1 tümleyeni = Checksum: 11101101

--- False positive anlat


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

### RDT 1.0
- Güvenilir bir kanal üzerinde güvenilir veri iletimi
- Bit hataları yok
- Paketler kaybolmuyor

### RDT 2.0
- Bit hatalarına sahip kanal
- Hatayı tespit etmek için **checksum** kullanılır.
- Hatanın üstesinden gelmek için geribildirim gönderilir.
  - ACK: ACKnowledgement
  - NAK: Negative AcKnowledgement
    - Tekrar iletim gerçekleştirilir.

Gönderici ACK ya da NAK gelmesini beklediği durumlarda üst katmandan daha fazla veri alamıyorsa, bunlara **DUR ve BEKLE Protokoller** denir. Gönderici paket gönderince, alıcıdan cevap bekler.

### RDT 2.1
- ACT ya da NAK bozulursa ne olacak?
  - Ona da checksum ekleyerek bu sorunu çözebiliriz.
- Alıcı, kopya paketlerin üstesinden gelebilmek için başlık alanına sequence number (dizi numarası) alanı eklenir.
- Dizi numarası için DUR ve BEKLE protokollerde (ACK veya NAK beklerken başka paket yollamadığı için) 1 bitlik dizi numarası alanı ile [0,1] dizi numaraları yeterlidir.

### RDT 2.2
- NAK Kullanmayan protokol olması gerekirse ne olması gerekir?
- Sadece NAK göndermek yerine son doğru alınan paket yerine ACK yollandığında gönderici, alıcının hangi paketi en son doğru aldığını anlayabilir.
- Kopya ACK, NAK anlamına gelir ve paket yeniden iletilir.

Üstteki durumlar, paketlerin illa ulaşacağı durumları kapsar. Diyelim ki ikisi de ulaşmadı, ne olacak? Dağ dağa küsmüş modunda oluyor bu sefer. Kimsenin haberi yok. Sonsuza kadar bekleyecek mi?

### RDT 3.0
- Göndericinin ACK almak için **makul** bir süre kadar beklemesi sağlanır. Bunun için geri sayım zamanlayıcısı (timeout) kullanılır.
- Bu süre, minimum 2RTT+iletim zamanı kadar tanımlanabilir. 
- Güvenilir veri iletimi sağlar ancak dur ve bekle olduğundan performans (verimlilik) problemi vardır.
- RTT+(L/R) kadar zamanda kanalın sadece (L/R)'lık kapasitesini kullanır. **U***gönderici* = (L/R) / ((L/R) + RTT)

DUR ve BEKLE şeklidne işlemek yerine bir paket için ACK beklemeden birden çok paket gönderilmesine izin verilirse fayda artar.

RTT + (L/R) kadar sürede en az 3 tane gönderiyor olsak, 3(L/R)'lık kapasite kullanımında 3 kat artış olur.

> Göndericiden alıcıya iletilen çok sayıda paket ardı ardına gönderilir. Bu yaklaşıma **pipelined (boru hattı)** denir. Burada takibi yapabilmek için iki güncelleme gerekiyor. 

- Güncelleme 1: **Sequence Number (Dizi Numarası)** alanını genişletilir.
- Güncelleme 2: Sırasız gelen paketler için alıcı/gönderici tarafta **tampon alanları** olması gerekir.

Boru hattında yaşanabilecek problemleri çözmek için iki farklı yaklaşım kullanılır.

#### N Kadar Geri Git (Go back N)

N: İletilmiş ya da iletilebilecek, henüz ACK mesajı alınmamış paketler için verilen dizi numarası aralığı. Pencere boyutu.

Nextseqnum: Kulanılmamış en küçük dizi numarası. Yani, üst kamandan veri geldiğinde segmente atanabilecek numara.

Sendbase: Alındı bilgisi alınmamış en eski paketin dizi numarası.

Aralık | Açıklama
--- | ---
[0, sendbase-1] | Halihazırda iletilmiş ve alındı bilgisi alınmış paketlere karşılık gelir.
[Sendbase, Nextseqnum-1] | Gönderilmiş, ancak alındı (ACK) mesajı alınmamış paketlere karşılık gelir.
[Nextseqnum, Sendbase+N-1] | Üst katmandan gelince paketlere atanabilecek dizi numaralarına karşılık gelir.

Dizi numarası >= Sendbase+N: Halihazırda boru hattında alındı bilgisi gönderilmemiş bir paketin alındı bilgisi gelene dek kullanılamaz.

K: Paket dizi numarası alanındaki bit sayısı

Örn: RDT 3.0 için 1 bitlik dizi numarası aralığı kullanıldığıdna tanımlanabilecek dizi numarası [0, 2^1-1] = [0,1]

Verimlilik problemi: Paket 1,2,3,4,5 iletimi için 2. pakette sıkıntı olduğunda, paket 2 ack timeout yenene kadar alıcı diğer paketleri discard eder. 

#### Seçici Tekrarlama

Alıcı tarafta da bir tampon alanı belirlenir.
- Gönderici
  - Eğer penceredeki bir sonraki dizi numarası msüsaitse paketi gönderir.
  - Zamana aşımı (n): Pkaket n'i tekrar gönder, zamanlayıcı yeniden başlatılır.
  - ACK(n) in [sendbase, sendbase+N]
    - Paket n'i alındı olarak işaretler
    - Eğer n ...
    - ... 
- Alıcı
  - ...

Pencere boyutunun. dizi numarasının yarısından küçük veya dizi numarasının yarısına eşit olması gerekiyor.

## 3.5 TCP ...

### Genel Bakış
- Noktadan noktaya
- Güvenilir, sıralı bayt akışı
- Boru hattı
- Göndermek ve alma tamponları
- Tam dubleks veri
- Bağlantı yönelimli
- Akış kontrolü

### TCP Segment Yapısı

- Kaynak Port | Hedef Port
- Dizi Numarası
- Alındı (ACK) Numarası
- (Başlık uzunluğu | Kullanılmaz | U | A | P | R | S | F) | Alıcı Penceresi
- Internet kontrol toplamı | Acil veri işaretçisi
- Seçenekler
- Veriler

### TCP Dizi numarası ve ACK

Random sayıdan başlatılır
Paketler bölünür
ACK, aldığı en son paket + 1 için gönderilir
