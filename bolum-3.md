
# Bilgisayar Ağları 4. ve 5. Hafta


## 2.1 Ağ uygulamalarının prensipleri

### Uygulama mimarileri
- İstemci sunucu (Client-server)
- Eşler arası (Peer-to-peer (P2P))
- İstemci sunucu ve P2P karışımı melez mimari (Hybrid of client-server and P2P)

#### İstemci sunucu mimarisi
##### Sunucu
- Daima açık bir ana sistemdir.
- Sabit bir IP adresi vardır.
- Ana sistem kümesi – sunucu çiftliği (server farms) yapılabilir.

##### İstemci
- Sunucu ile iletişim kurar.
- Her zaman açık olmak zorunda değildir.
- Dinamik (değişebilir) IP adresine sahip olabilir.
- Birbirleriyle direk olarak iletişime geçmezler.

#### P2P mimarisi
- Her zaman açık olan sunuculara ihtiyaç yoktur.
- Gelişigüzel uç sistemler birbirleriyle direk olarak iletişime geçerler.
- Uç sistemler birbirleriye ara sıra bağlanırlar ve IP adreslerini değiştirirler.
- Örn: Gnutella

#### İstemci-sunucu ve P2P mimarilerini birleştiren melez mimariler
##### Napster
- Dosya transferi P2P olarak gerçekleştirilir.
- Dosya arama merkezidir:
  - Eşler merkezi sunucuda içerik kaydı yapar.
  - Eşler, içeriği bulmak için aynı merkezi sunucuyu sorgular.

##### Anında mesajlaşma
- İki kullanıcının mesajlaşması P2P dir
- Varlık tespiti/bulması (presence detection/location) merkezidir:
  - Kullanıcılar IP adreslerini çevrimiçi olunca merkezi sunucuya kayıt ederler.
  - Kullanıcılar diğerlerinin IP adreslerini bulmak için merkezi sunucu ile iletişime geçerler.

---

### Süreç İletişimleri
Süreç: bir uç sistemde çalışan program.
- Aynı uç sistem üzerinde, iki süreç iç-süreç iletişimi (işletim sistemi tarafından tanımlanan) kullanarak birbirleriyle iletişime geçebilirler.
- Farklı sistemler üzerinde çalışan süreçler mesaj alış verişi ile haberleşirler.

#### Süreç türleri:
- İstemci süreçleri: İletişimi başlatan süreç
- Sunucu süreçleri: İletişime geçilmeyi bekleyen süreç

Not: P2P mimarideki uygulamalarda hem istemci süreçleri hem de sunucu süreçleri yer alır.


### Süreç ve Bilgiasyar arasındaki arabirimler: Soketler
- Bir süreç mesajalra ağa soket adındaki yazılımlar aracılığıyla gönderir ve alırç.
- Soket kapı benzeşmesi:
  - Gönderici süreç mesajı kapıya (sokete) doğru iter.
  - Gönderici süreç, kapının diğer tarafında mesajı hedef sürecin kapısına taşıyacak olan bir taşım altyapısının olduğunu varsayar.

### Süreçleri işaret etmek
- Bir sürecin mesaj alabilmesi için bir tanımlayıcısı (identifier) olması gerekir.
- Bir ana sistem 32 bit'lik benzersiz bir IP adresine sahiptir.
- Soru: Süreci tanımlayabilmek için sürecin çalıştığı sistemin sadece IP adresini bilmesi yeterli midir?
  - Cevap: ayır, aynı ana sistem üzerinde pek çok süreç çalışıyor olabilir. Tanımlayıcı hem IP adresini hem de süreçle ilgili hedef bağlantı numarasına (port number) sahiptir.
  - Örnek port numaraları:
    - HTTP: 80
    - Posta (SMTP): 25

#### Uygulama katmanı protokolleri neleri tanımlar?
- Karşılıklı iletilen mesajlar: Örneğin istek ve cevap mesajları
- Mesajların syntax'ı: Mesajlardaki alanlar ve bu alanların nasıl tanımlandığı
- Alanların anlamları: Alanlardaki bilgilerin anlamları
- Süreçlerin ne zaman mesajları alıp göndereceklerine dair kurallar

##### Genel etki alanı protokolleri
- RFClerde tanımlanmıştır. (RFC = Request for Comment, Yorumlar İçin Talep)
- Birlikte işlerliğe (interoperability) olanak sağlar.
- Örnek genel protokoller: HTTP, SMTP
- Örnek özel protokoller: KaZaA

#### Veri kaybı
- Bazı uygulamalar bir miktar veri kaybını tolere edebilir. Örneğin: Ses, video
- Diğerleri 100% güvenli veri transferine ihtiyaç duyar. Örneğin: Dosya transferi, telnet

#### Zamanlama
- Bazı uygulamalar "etkili" olabilmek için az gecikme gerektirirler. Örneğin: İnternet telefonu, etkileşimli oyunlar

#### Bant genişliği
- Bazı uygualmalar "etkili" olabilmek için belli bir miktarda bant genişliğine ihtiyaçç duyarlar. Örneğin: Multimedya
- Diğerleri bant genişliğinin ne kadarını kullanabilirlerse onunla idare edebilirler. Bunlara elastik uygulamalar denir.

#### Güvenlik
- Bir taşıma katmanı protokolü bir ya da daha fazla güvenlik servisi sunabilir
- Veri gizliliği
- Veri doğruluğu (Verinin değiştirilememesi için)
- Son nokta kimlik denetimi
- Gönderici tarafında şifreleme, alıcı tarafında şifre çözümü (Middleman Attack olmaması için)

### TCP Servisleri
- **Bağlantı-Yönetilimli (Connection-Oriented)**: İstemci ve sunucu süreçler arasında bağlantı kurulumu gerekir.
- **Güvenilir Taşıma (Reliable Transport)**: Gönderici ve alıcı süreçler arsaında güveniir taşıma.
- **Akış Kontrolü (Flow Control)**: Gönderici alıcıyı sıkıştırmaz
- **Tıkanıklık Kontrolü (Congestion Control)**: Ağ çok yüklendiğinde göndericinin gönderdiği veri miktarını kısar.
- Zamanlama, minimum bant genişliği garantisi **sağlamaz**.

### UDP Servisleri
- Gönderici ve alıcı süreçler arasında güvenilir olmayan veri iletimi
- Bağlantı kurulumu (connection setup), güvenilirlik (reliability), akış kontrolü (flow control), tıkanıklık kontrolü (congestion control), zamanlama (timing), veya bant genişliği garantisi (bandwith guarantee) **SAĞLAMAZ**.
- Soru: O zaman bununla neden ilgileniyoruz? Neden UDP var?
  - Cevap: 

Ne TCP, ne de UDP "güvenlik" **sağlamaz**.

Güvenlik ve Güvenilirlik aynı şey **değil**:
Güvenlilirlik: Tam ve doğru şekilde taşınması
Güvenlik: Verinin değiştirilememesi, şifrelenmesi

> Ancak, TCP, SSL ile güvenlik sağlayabilir. Dikkat: SSL bir protokol değildir. SSL, uygulama katmanı protokolünün hemen altında, TCP üzerinde çalışır. Bir eklenti yazılımıdır ve geliştiriciler tarafından uygulamaya güvenlik katmak için dahil edilir.

## 2.2 Web ve HTTP

### Web terminolojisi
- Bir web sayfası, nesnelerden oluşur.
- Bir nesne bir  HTML dosyası, bir JPEG görüntüsü, bir Java appleti veya bir video klip olabilir.
- Çoğu web sayfası birçok başvuru nesnesini içeren temel bir HTML dosyasından meydana gelir.
- Her nesne sadece bir tek URL ile adreslenebilen bir dosyadır.
- Örnek URL: [www.someschool.edu][/someDept/pic.gif]

Kısaltmalar:
  - URL: Uniform Resource Locator
  - HTTP: Hypertext transfer protocol

#### HTTP
- Web'in yugulama katmanı protokolüdür.
- İstemci/sunucu modeli
  - İstemci: Web nesnelerini isteyen, alan ve gösteren tarayıcı
  - Sunucu: İsteklere karşılık olarak nesneleri gönderen web sunucusu.
- TCP kullanılır. Port 80'den yayınlanır.

- Kalıcı olmayan (nonpersistent) HTTP
  - Genellikle bir TCP bağlantısı ile bir nesne gönderilir.
  - HTTP/1.0 kalıcı olmayan (nonpersistent) HTTP‘yi kullanır.
- Kalıcı olan (persistent) HTTP
  - İstemci ile sunucu arasında tek bir TCP bağlantısı ile birden fazla nesne gönderilebilir.
  - HTTP/1.1 varsayılan modunda kalıcı (persistent) bağlantı kullanır

##### Kalıcı olmayan (nonpersistent) HTTP 
Her nesne ayrı TCP bağlantısında iletilir.

Süreç:
- HTTP istemcisi port 80 üzerinden www.someschool.edu sunucusunda bir TCP bağlantısı başlatır.
  - Port 80 üzreinde TCP bağlantılarını bekleyen www.someschool.edu HTTP sunucusu bağlantıyı kabul eder ve istemciye haber verir.
- HTTP istemcisi sunucuya soketi aracılığıyla bir HTTP istek mesajı (URL içeren) gönderir. 
- Mesaj istemcinin someDepartment/home.index nesnesini istediğini belirtir
  - HTTP sunucusu istek mesajını alır, istenen mesajı içeren cevap mesajı oluşturur ve mesajı soket aracılığıyla istemciye iletir.
  - HTTP sunucusu TCP bağlantısını kapatır.
- HTTP istemcisi HTML dosyası içeren cevap mesajını alır ve HTML'yi görüntüler. HTML dosyasını ayrıştırınca 10 tane jpeg görüntüsüne olan referansı bulur.

**Tüm 10 nesne için üstteki adımlar tekrar edilir.**

---

RTT (Round Trip Time): İstemciden sunucuya giden bir paketin gidiş dönüş zamanı. Küçük bir paketin istemciden sunucuya ve tekrar istemciye veri ulaşması için geçen süre.
Cevap zamanı (Response time):
- TCP bağlantısını başlatmak için bir RTT
- HTTP isteği ve HTTP evabının ilk birkaç bitinin dönüşü için bir RTT
- Dosya iletim zamanı toplam 2RTT + İletim zamanı kadar sürer.

Gidiş geliş için yapılan bağlantılar:
TCP-İSTEK
TCP-YANIT
--- bir rtt bitti ---
HTML-İSTEK
HTML-YANIT


##### Kalıcı bağlantı (persistent) HTTP
Her nesne tek TCP bağlantısında iletilir.
- Pipelined: Paralel, eşzamanlı, asenkron
- Without Pipelined: Seri, ardışık, senkron

#### HTTP istek mesajı (Request) ve cevap mesajı (Response)
- İki çeşit HTTP mesajı var: İstek, cevap
- ASCII (insanlar tarafından da anlaşılabilir)

#### HTTP Durum kodları:
200, 301, 400, 404, 505 gibi.

HTTP durumsuzdur (stateless). Bir linke iki kere tıklarsanız, iki kere cevap alırsınız.

#### Cookies
Bir çok web sitesi çerez kullanır.
Dört bileşen:
- HTTP cevap mesajındaki bir cookie başlık satırı
- HTTP istek mesajındaki bir cookie başlık satırı
- Kullanıcının uç sisteminde tutulan ve tarayıcı tarafından yönetilen bir cookie dosyası
- Web sitsindeki bir arka uç veritabanı

Örnek:
Suzan Internet’e her zaman aynı PC den ulaşmaktadır

Diyelim ki bir e-ticaret sitesini ilk defa ziyaret ediyor

İstek siteye ilk defa ulaştığında, site benzersiz bir tanımlama numarası oluşturur ve arka-uç veritabanında sunucu tanımlama numarası ile indekslenen bir giriş oluşturur.

Cookielerin sağladıkları:
- Yetkilendirme (Authorization)
- Alışveriş sepeti (Shopping cards)
- Tavsiyeler
- Kullanıcı oturum durumu (User session state)

Cookieler ve gizlilik
- Cookieler sitelerin sizin hakkkınızda pek çok şey öğrenmesine izin verir.
- Sitelere e-mail ve isim bilgilerinizi verebilirsiniz.
- Arama motorları daha fazlasını öğrenmek için redirection & cookieleri kullanırlar.
- Reklam şirketleri sitelerden bilgileri alırlar.

#### Web tampon belleği (Caches) (Vekil sunucusu, Proxy server)
Amaç: HTTP istekerlini köken Web sunucusu yerine karşılayan bir ağ varlığdıır.
- Kullanıcı tarayıcısını, kullanıcının tüm HTTP isteklerini önce bu tampon belleğe yönlendireceği şekilde yapılandırabilir.
- Tarayıcı tüm HTTP isteklerini bu tampon belleğe yönlendirir.
  - Nesne tampon bellekte ise, tampon bellek nesneyi istemciye döndürür.
  - Nesne tampon bellekte değilse, tampon bellek köken sunucudan nesneyi ister ve sonrasında nesneyi istemciye döndürür.
- Tampon bellek aynı anda hem sunucu hem istemci gibi davranır
- Genel olarak tampon bellekler bir ISP tarafından kurulurlar (üniversite, şirket, yerleşim yeri ISP’si)

Neden lazım?
- Cevap zamanını azaltır
- Kurumun erişim hattındaki trafiği azaltır
- Tampon belleklerin yoğun olduğu bir İnternet "zayıf" içerik sağlayıcıların içerği daha iyi sunmalarını sağlar. (Fakat aynısını P2P dosya paylaşımı da yapabilir)

### Tampon belleği örneği

#### Varsayımlar
- Ortalama nesne büyüklüğü = 100,000 bits
- Kurumun tarayıcılarından köken sunuculara gelen ort. istek oranı = 15 istek/saniye
- Kurumsal yönlendiriciden köken sunuculara ya da geri yönlendiricilere olan gecikme = 2 saniye

#### Sonuçlar
- LAN’daki ağ yükü/trafik yoğunluğu= 0.15
- Erişim hattındaki ağ yükü/trafik yoğunluğu = 1
- Toplam gecikme= Internet gecikmesi + erişim gecikmesi + LAN gecikmesi = 2 saniye + dakikalar + millisaniyeler

#### Olası çözüm
Erişim hattının bant genişliğini diyelim ki 10 Mbps’ye arttırırsak

#### Sonuçları
- LAN’daki yarar = 15%
- Erişim hattındaki yarar = 15%
- Toplam gecikme= Internet gecikmesi + Erişim gecikmesi + LAN gecikmesi = 2 saniye + millisaniyeler + millisaniyeler
Maliyetli bir artırım

#### Tampon bellek kurarsak
- Hit alma oranı .4 varsayılırsa
  - İsteklerin 40%'ı neredeyse hemen karşılanır
  - İsteklerin 60%'ı köken sunucular tarafından karşılanır
  - Erişim hattının kullanılması 60 % ‘a azaltıldı, önemsiz gecikmeler olabilir (10 milisaniye kadar)
  - Toplam ort. gecikme = Internet gecikmesi + erişim gecikmesi + LAN gecikmesi

### Koşullu GET
- Amaç: eğer tampon bellek güncel sürüme sahipse nesneyi gönderme
- Tampon bellek: HTTP isteği içerisinde belleğe alınmış kopyanın tarihini belirler.
  - If-modified-since: **\<date\>**
- Sunucu: eğer tampondaki kopya güncelse cevapta nesne bulunmaz:
  - HTTP/1.0 304 Not Modified


## 2.3 FTP
Uzak anasisteme/sistemden dosya transferi yapmak için kullanılan bir protokol.

İki farklı paralel TCP bağlantısı kullanır:
- Dosya transferi için istemci ve sunucu arasında bir **veri bağlantısı** oluşturur.
- Kimlik denetleme için bir **kontrol bağlantısı** oluşturur.
- Kontrol bilgisini **bant dışı** gönderir.
- Durum korumalıdır. Kim olduğunuzu, hangi dizinde olduğunuzu hatırlar.
- Komutlar, 7 bit ASCII biçiminde kontrol bağlantısı boyunca gönderilir.

Örnek komutlar:
- USER kullanıcıadı
- PASS parola
- LIST sunucuda halihazırda bulunan dizindeki dosyaları listeler
- RETR dosyaadı dosya almak için kullanılır
- STOR dosyaadi uzaktaki sisteme dosya depolamak için kullanılır

Örnek durum kodları:
- 331 Username OK, password required
- 125 data connection already open; transfer starting
- 425 Can’t open data connection
- 452 Error writing file

HTTP | FTP
---|---
Dosya transfer protokolü | Dosya transfer protokolü
Durumsuz | Durum korumalı (User Authentication zorunlu)

## 2.4 E-Posta (SMTP, POP3, IMAP)
Üç ana bileşen:
- User agents (Posta okuyucuları)
  - Mesaj okuma, cevap verme, iletme, kaydetme ve oluşturma
  - Örneğin: Outlook, Eudora, Geary
  - Sunucuda depolanan, gelen ve giden mesajları listeler.
- Mail servers (Posta sunucuları)
  - Posta kutusu: Kullanıcıya gelen mesajları içerir.
  - Mesaj kuyruğu: Giden (gönderilecek) mesajları içerir.
  - SMTP: Simple mail transfer protocol: Posta sunucuları arasında posta göndermek için kullanılır.
    - İstemci: Gönderen posta sunucusu
    - Sunucu: Alıcı posta sunucusu

### SMTP
- İstemciden sunucuya eposta mesajlarını güvenilir olarak transfer etmek için port 25 üzerinden TCP kullanır.
- Direk transfer: gönderen sunucudan alıcı sunucuya
- Üç fazlı transfer
  - El sıkışma (greeting)
  - Mesajın iletimi
  - Kapatma (closure)
- Komut /cevap etkileşimi (command/response interaction)
  - **Komutlar:** ASCII metin
  - **Cevaplar:** durum kodları ve ilgili deyimler
- Mesajlar 7 bit’lik ASCII metinleridir.

#### Senaryo: Alice, Bob’a mesaj gönderir
1) Alice kullanıcı temsilcisi kullanarak mesaj gönderir ve “to” satırına bob@someschool.edu yazar
2) Alice’in kullanıcı temsilcisi mesajı kendi posta sunucusuna gönderir; mesaj mesaj kuyruğuna konur
3) SMTP’nin istemci tarafı Bob’un posta sunucusuna TCP bağlantısı açar
4) SMTP istemcisi Alice’in mesajını TCP bağlantısı üzerinden gönderir.
5) Bob’un posta sunucusu mesajı Bob’un posta kutusuna koyar
6) Bob mesajı okumak için kendi kullanıcı temsilcisini çalıştırır.

Alice | Kullanıcı temsilcisi | | Alice'in Sunucusu | | Bob'un sunucusu | | Kullanıcı temsilcisi | Bob
--- | --- | --- | --- | --- |--- | --- | --- | ---
| | | SMTP | | SMTP | | SMTP, POP3 

#### Notlar

- SMTP kalıcı (persistent) bağlantı kullanır.
- SMTP mesajları 7 bit’lik ASCII metinden oluşur (Header & Body).
- SMTP sunucusu msaj sonlarını belirtmek için **CRLF.CRLF** kullanır
  - **CR:** carriage return
  - **LF:** line feed

#### HTTP ile farkı

HTTP | SMTP
--- | ---
Dosya transfer protokolü | Dosya transfer protokolü 
ASCII komut ve cevapları kullanılır | ASCII komut ve cevapları kullanılır
Çekme (Pull) | İtme (Push)
Her nesne ayrı HTTP cevabı | Tüm nesneler tek mesaj içerisine yerleştirilir
Bant içi kontrol kullanılır | Bant dışı kontrol kullanılır 
Kalıcı veya kalıcı olmayan bağlantı kullanılabilir | Kalıcı bağlantı kullanılır

Kendime soru: Bant içi ve bant dışı kontrol nedir?

#### Posta mesajı biçimleri
- SMTP: eposta mesajlarının gönderimi için bir protokoldür
- RFC 822: metin mesaj biçimini belirleyen standarttır:
- Başlık satırları (Header)
  - To:
  - From:
  - Subject:
- Gövde (Body)
  - Sadece ASCII karakterlerden oluşan mesaj buraya yazılır.

##### Örnek posta:
>From: kelmange@ka.co
>Subject: Olduramadım
>
>Uzun zamandır görüşemiyoruz. Nerelerdesin?
>Beter Ali
> .

#### Mesaj biçimi: Multimedia için
- MIME: çok amaçlı Internet posta uzantıları (multi purpose mail extension), RFC 2045, 2056
- MIME içerik tipini tanımlamak için mesaj başlığına ek başlıklar eklenmelidir

### Posta erişim protokolleri
- SMTP: alıcı sunucuya gönderme/depolama ile ilgilidir
- Posta erişim protokolleri: sunucudan alma ile ilgilidir
- POP: Post Office Protocol [RFC 1939] 
  - yetkilendirme (agent <--> server) ve download
- IMAP: Internet Mail Access Protocol [RFC 1730]
  - Daha fazla özellik (daha karmaşık)
  - Sunucuda depolanan mesajların idaresi
- HTTP: Hotmail , Yahoo! Mail, etc.

## 2.5 DNS

[//]: # (TODO: Burası düzenlenecek. Bilgisayar ağları 3. slaytta daha ayrıntılı anlatılmış.)

- Domain name system (Etki alan adı sistemi)
- Dağıtık bir veri tabanı kullanır.
- Ana sistem adreslerinin sorgulanmasını sağlar.
- UDP üzerinden çalışır.
- **Ana sistem lakapları sağlar:** Kolay hatırlanan adlarla eşleme
- **Posta sunucusu lakapları sağlar:** Posta adreslerinin kolay olmasını sağlar
- **Yük dağıtımı sağlar:** Çok sunuculu sistemlerde
- Hiyeraşik sunucu yapısındadır:
  - **Kök DNS:** Toplamda 13 adet var.
  - **Üst düzey DNS:** Com, Edu, Tr, Fr
  - **Yetkili DNS:** Kurum DNSleri
  - **Yerel DNS:** Şirket veya Üniversitelerde

Gecikmeyi azaltmak ve performansı arttırmak için tampon bellekte kaynak kayıtları (Resource Records, RR) tutulur.
 
Tekrarlanan sorgu: 
- Eşleşmeyi bulmak yerel DNS sunucusunun görevidir.
- Yerel DNS'in iletişim kurduğu sunucular, "bende yok, ancak şuraya sor" yanıtı döner.
- Böylece son yetkili DNS'e ulaşıp sonuca ulaşır.

Yinelenen sorgu:
- Her sunucu diğeri adına sorguyu yayarak eşleştirme sonuçlarını geri döndürür.

> Editör notu: (Y)ineleme, (Y)ayma'dan aklına gelsin. 

## 2.6 Eşler arası uygulamalar
**Napster:** Merkez sunucu üzerinden varlık tespiti yapar. Dosya paylaşımı eşler arasındadır.
**Gnutella:** Sorgu baskını ile çalışır. İstekler tüm komşulara, komşular da kendi komşularına gönderirken yanıt doğrudan istekte bulunan eşe gönderilir.
**Kazaa:** Grup liderleri vardır. Eşlerin taleplerini diğer grup liderlerine iletir. Grup lideri üzerinden aktarım sağlanır.
