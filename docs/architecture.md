
# Perraro Appointment Architecture

## Genel Bakış

Perraro Appointment, Perraro Electric Bike için geliştirdiğim randevu ve operasyon yönetimi yapısıdır. Bu sistemi oluştururken amacım sadece bir form toplamak ya da basit bir dashboard göstermek değildi. Asıl hedefim, gerçek bir işletmede kullanılabilecek kadar mantıklı, düzenli ve geliştirilebilir bir appointment akışı kurmaktı.

Bu proje iki ana ihtiyaca odaklanıyor. İlki, test ride taleplerini daha düzenli toplamak ve takip edebilmek. İkincisi ise servis veya technician tarafındaki randevu ve operasyon sürecini daha görünür hale getirmek. Özellikle küçük ve orta ölçekli işletmelerde bu tarz süreçler çoğu zaman dağınık ilerliyor. Formlar ayrı yerde, mesajlaşmalar ayrı yerde, kayıtlar başka yerde, takip ise çoğu zaman manuel yapılıyor. Ben bu projede bu dağınıklığı daha sistemli bir yapıya çevirmeye çalıştım.

Bu repo hem projenin mantığını göstermek hem de benim backend, otomasyon, sistem tasarımı ve iş akışı kurma yaklaşımımı yansıtmak için hazırlandı.

## Problem ve Amaç

Bu projeyi geliştirirken çözmeye çalıştığım temel problem şuydu: bir işletmede randevu akışları çoğu zaman sadece form almakla bitmiyor. Asıl zorluk, gelen veriyi düzgün işlemek, ilgili kişilere ulaştırmak, kayıt altına almak ve sonrasında takip edilebilir hale getirmek.

Özellikle test ride tarafında amaç sadece kullanıcının adını ve telefonunu almak değil. O bilgiyi düzgün şekilde işlemek, gerektiğinde veri tabanına yazmak, operasyon tarafına görünür hale getirmek ve sonraki adımlar için hazır hale getirmek gerekiyor.

Servis veya technician tarafında ise konu daha da operasyonel hale geliyor. Çünkü burada sadece yeni bir talep almak değil, aynı zamanda personel, işlem akışı, durum takibi ve iç iletişim tarafı da işin içine giriyor.

Bu sistemin temel amaçları şunlardır:

- test ride randevularını daha düzenli toplamak
- servis ve technician süreçlerini daha takip edilebilir hale getirmek
- manuel operasyon yükünü azaltmak
- veri akışını daha kontrollü bir yapıya oturtmak
- farklı servisler arasında entegrasyon kurulabilecek bir temel hazırlamak
- düşük maliyetli ama ciddi bir sistem mantığı kurmak

## Sistem Bileşenleri

Bu yapıyı tek parça bir uygulama gibi değil, birbiriyle bağlantılı birkaç bileşen şeklinde düşündüm. Bu yaklaşım hem geliştirmeyi kolaylaştırıyor hem de sistemi zamanla büyütmeyi daha mümkün hale getiriyor.

### 1. Test Ride Frontend

Bu bölüm, son kullanıcı tarafına bakan yüzdür. Amaç, test ride talebi oluşturacak kişinin bilgilerini mümkün olduğunca sade ve anlaşılır bir arayüz üzerinden almak.

Burada benim için önemli olan şey, sadece formu göstermek değildi. Formun, operasyon tarafında işe yarayacak temiz veri üretmesi gerekiyordu. Yani frontend tarafı sadece görsel bir katman değil, veri girişinin ilk noktası.

Bu bölüm ileride kolayca genişletilebilir. Örneğin:
- daha fazla alan eklenebilir
- tarih ve saat seçimi geliştirilebilir
- uygunluk kontrolü eklenebilir
- doğrulama ve hata yönetimi güçlendirilebilir

### 2. Dashboard Frontend

Dashboard tarafı, sistemin operasyon yüzü olarak düşünüldü. Kullanıcıya açık formdan farklı olarak burada amaç, gelen randevu veya işlem kayıtlarını daha görünür hale getirmek.

Bu bölüm sayesinde işletme tarafı:
- hangi talepler geldi
- hangi kayıtlar bekliyor
- hangi süreçler tamamlandı
- hangi alanlarda müdahale gerekiyor

gibi konuları daha rahat takip edebilir.

Bu repo içindeki dashboard yapısı temel seviyede bir iskelet gösteriyor. Ama mantık olarak büyümeye çok uygun. İleride rol bazlı erişim, filtreleme, durum güncelleme ve raporlama gibi özelliklerle daha güçlü hale getirilebilir.

### 3. n8n Workflows

Bu projenin asıl mantık merkezi workflow tarafı. Ben bu projede n8n’i sadece otomasyon aracı gibi değil, iş akışını yöneten backend mantığının önemli bir parçası olarak düşündüm.

Workflow’ların görevi temel olarak şunlar:

- frontend tarafından gelen veriyi almak
- veriyi doğrulamak veya normalize etmek
- gerekli yerlere iletmek
- kayıt sürecini başlatmak
- bildirim ve operasyon mantığını çalıştırmak
- süreci sistematik hale getirmek

Bu yaklaşımın bana göre önemli avantajı şu: bazı iş problemleri için her şeyi sıfırdan klasik backend kodu ile yazmak yerine, doğru planlanmış workflow mantığı ile hem daha hızlı hem de daha anlaşılır bir sistem kurulabiliyor.

Repo içinde şu an görünen workflow dosyaları bunu temsil eden temel örneklerdir:

- `workflows/testride.json`
- `workflows/technician/staff.json`

Bunlar sistemin tam üretim halini birebir yansıtmak zorunda değil. Ama kullanılan yaklaşımı, akış mantığını ve sistem tasarımını göstermek için önemli.

### 4. Supabase

Supabase bu yapı içinde veri saklama ve kayıt mantığı açısından önemli bir rol oynuyor. Randevu, talep veya operasyon verisini bir yerde düzenli tutmak gerekiyorsa böyle bir servis çok faydalı hale geliyor.

Benim açımdan Supabase’in bu projedeki değeri şurada:
- hızlı geliştirme imkanı sağlaması
- veri yapısını düzenli tutmaya yardımcı olması
- küçük ve orta ölçekli projelerde yeterince esnek olması
- klasik ağır kurulumlara göre daha pratik bir seçenek sunması

Bu projede Supabase sadece veri tabanı gibi değil, sistemin kayıt hafızası gibi düşünülebilir.

### 5. Telegram

Telegram tarafı daha çok bildirim ve operasyon akışını hızlandırmak için düşünüldü. Bazı sistemlerde verinin sadece kaydedilmesi yetmez; ilgili kişilere hızlı şekilde ulaşması da gerekir.

Bu yüzden Telegram entegrasyonu, özellikle iç operasyon tarafında faydalı bir katman oluşturuyor. Yeni talep, durum değişikliği veya önemli bir bilgi, doğrudan daha görünür bir şekilde iletilebilir.

### 6. OpenPhone

OpenPhone bu yapıda iletişim sürecini daha operasyonel hale getirmek için düşünülmüş servislerden biri. Özellikle müşteri iletişimi, ekip içi takip ve belirli aksiyonların daha düzenli yürütülmesi açısından önemli olabilir.

Her işletmenin kullandığı araç farklı olabilir ama bu projede benim yaklaşımım, sistemin tek bir araca bağımlı olmadan farklı servislerle entegre olabilecek şekilde düşünülmesiydi.

## Veri Akışı

Bu sistemin en önemli taraflarından biri, verinin sistem içinde nasıl hareket ettiğidir. Çünkü iyi bir sistem sadece veri toplamaz, o veriyi anlamlı bir akışa dönüştürür.

Test ride tarafından örnek bir genel akış şu mantıkla düşünülebilir:

1. Kullanıcı test ride formunu doldurur.  
2. Form verisi sistemin ilgili giriş noktasına gönderilir.  
3. Workflow gelen veriyi alır.  
4. Gerekirse veride doğrulama, düzenleme veya normalize etme işlemi yapılır.  
5. Kayıt süreci başlatılır.  
6. Uygunsa veri tabanına yazılır veya ilgili yapıya aktarılır.  
7. Operasyon tarafı için bildirim veya görünürlük sağlanır.  
8. Dashboard üzerinden takip edilebilir hale gelir.

Servis veya technician tarafında ise benzer mantık daha operasyon odaklı ilerler:

1. Talep veya işlem verisi sisteme girer.  
2. Workflow ilgili akışı çalıştırır.  
3. Operasyon tarafına bilgi iletilir.  
4. Gerekirse personel veya ilgili ekip sürece dahil edilir.  
5. Kayıt ve takip süreci başlar.  
6. Sonraki aşamalarda durum güncelleme mantığı eklenebilir.

Buradaki önemli fikir şu: veri bir yerde kaybolmuyor, bir formdan çıkıp manuel mesajlaşmalarda dağılmıyor. Belirli bir akış içinde hareket ediyor.

## Neden Bu Yapıyı Seçtim?

Bu projede özellikle daha modüler ve gerçek hayata yakın bir yapı kurmak istedim. Çünkü gerçek işletme problemlerinde çoğu zaman tek parça bir uygulama yerine birkaç sistemin birlikte çalıştığı yapılar daha yaygın oluyor.

Bu mimariyi seçmemin nedenleri şunlardı:

- düşük maliyetli ve geliştirilebilir olması
- tek seferlik demo yerine büyüyebilecek bir temel kurması
- frontend ile operasyon mantığını ayırabilmesi
- workflow yaklaşımı ile bazı süreçleri daha hızlı kurabilmesi
- veri, bildirim ve arayüz katmanlarını birbirinden ayırabilmesi
- küçük işletmeler için uygulanabilir olması

Benim için bu projede önemli olan sadece “çalışıyor” demek değildi. “Neden böyle kuruldu?” sorusuna da mantıklı cevap verebilen bir sistem ortaya koymak istedim.

## Repo Yapısı

Bu repo şu anda aşağıdaki mantıkla düzenlenmiştir:


## Repo Yapısı

Bu repo şu anda aşağıdaki mantıkla düzenlenmiştir:

```bash
assets/
docs/
frontend/
  dashboard/
    index.html
  test-ride/
    index.html
workflows/
  technician/
    staff.json
  testride.json
README.md

Klasörlerin Amacı

assets/
Logo ve görsel gibi ortak dosyalar burada tutulur.

docs/
Sistemin mantığını, mimarisini ve teknik yaklaşımını anlatan dokümantasyon dosyaları burada tutulur.

frontend/
Kullanıcıya veya operasyon tarafına görünen arayüz dosyaları burada yer alır.

workflows/
n8n iş akışları ve otomasyon mantığını gösteren dosyalar burada tutulur.

README.md
Repo’nun giriş noktasıdır. Projeyi hızlıca anlamak isteyen biri önce burayı okur.

Bu Repo Nasıl Değerlendirilmeli?

Bu repo birebir production ortamındaki tüm detayları paylaşmak için hazırlanmadı. Daha çok sistemin mantığını, kullanılan yaklaşımı ve proje düşüncesini göstermek için düzenlendi.

Bu yüzden bazı alanlar:

sadeleştirilmiş olabilir

gizlenmiş olabilir

placeholder ile değiştirilmiş olabilir

paylaşım için temizlenmiş olabilir

Bence bu tarz projelerde önemli olan sadece “tam çalışan dosyayı göstermek” değil, sistem kurma düşüncesini de gösterebilmek. Ben de bu repoda bunu öne çıkarmaya çalıştım.

Güvenlik ve Paylaşım Notu

Repo içindeki bazı workflow veya yapı dosyalarında gerçek credential, token, özel URL, gizli anahtar veya işletmeye özel hassas veriler yer almıyor olabilir. Bu bilinçli bir tercih.

Çünkü bu projeyi hem paylaşılabilir hale getirmek hem de güvenlik açısından doğru şekilde sunmak istedim. Gerçek bir sistemi portföy haline getirirken en zor ama en önemli konulardan biri bu dengeyi kurmak.

Bu Sistemi Kendi İçin Kurmak İsteyenlere Not

Ben bu yapıyı Perraro özelinde düşünerek geliştirdim ama mantık olarak farklı işletmelere de uyarlanabilir.

Kendi tarafında benzer bir sistem kurmak isteyen biri için benim önerdiğim yaklaşım şu olur:

Önce problemi net tanımla. Yani gerçekten neyi çözmek istediğini belirle. Sadece “form yapayım” diye başlamak genelde yetersiz kalıyor. Formun arkasında nasıl bir operasyon var, kim ilgilenecek, kayıt nasıl tutulacak, hangi noktada bildirim gidecek, neyin takip edilmesi gerekiyor, bunları baştan düşünmek gerekiyor.

Sonra sistemi parçalara ayırmak daha doğru oluyor:

veri girişi nereden olacak

workflow hangi adımları yönetecek

veri nerede tutulacak

ekip süreci nereden takip edecek

hangi entegrasyonlar gerçekten gerekli

Benim bu projede çıkardığım en önemli ders şu oldu: iyi bir operasyon sistemi sadece güzel arayüzle kurulmaz. Asıl değer, arka taraftaki akışın net olmasıdır.

Geliştirme Potansiyeli

Bu yapı ileride birçok yönde geliştirilebilir. Örneğin:

kimlik doğrulama ve yetkilendirme eklenebilir

dashboard daha gelişmiş hale getirilebilir

durum yönetimi eklenebilir

randevu takvimi entegrasyonu yapılabilir

daha güçlü raporlama ekranları eklenebilir

SMS veya e-posta entegrasyonları eklenebilir

admin ve staff rolleri ayrıştırılabilir

Bu yüzden ben bu projeyi bitmiş tek parça bir ürün gibi değil, büyüyebilecek bir temel sistem olarak görüyorum.

Son Not

Bu proje benim için sadece teknik bir çalışma değil. Aynı zamanda gerçek iş problemlerini anlamaya, süreç kurmaya ve yazılımı sadece kod olarak değil sistem olarak düşünmeye çalıştığım bir gelişim süreci.

O yüzden burada paylaşılan şey sadece birkaç dosya değil. Aynı zamanda bir düşünce biçimi, bir sistem kurma yaklaşımı ve gerçek dünyaya yakın çözüm üretme çabası.
