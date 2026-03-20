<p align="center">
  <img src="assets/logo.png" alt="Furkan Karabey Logo" width="180">
</p>

# Perraro Appointment

Perraro Appointment, Perraro Electric Bike için geliştirdiğim bir randevu ve operasyon yönetimi projesidir.

Bu proje ile test ride taleplerini, servis/teknisyen randevularını ve bazı temel iletişim akışlarını daha düzenli ve daha takip edilebilir hale getirmeyi hedefledim. Amacım sadece çalışan bir sistem kurmak değil; aynı zamanda küçük ve orta ölçekli işletmelerin daha düşük maliyetle kullanabileceği, geliştirilebilir bir yapı ortaya koymaktı.

Bu repo benim için aynı zamanda bir öğrenme ve gelişim projesi. Backend, otomasyon, sistem tasarımı ve gerçek iş problemlerine çözüm üretme tarafında kendimi geliştirmeye çalışırken ortaya çıkan ciddi portföy projelerinden biri.

## Proje Amacı

Bu sistemin ana amacı:

- test ride randevularını daha düzenli toplamak
- servis / technician appointment süreçlerini takip edebilmek
- müşteri iletişimini daha kontrollü hale getirmek
- operasyon tarafında manuel işleri azaltmak
- gerektiğinde farklı araçlarla entegre olabilecek bir temel yapı kurmak

## Kullandığım Teknolojiler

Projede kullanılan ana yapılar:

- n8n
- Supabase
- OpenPhone
- Telegram
- HTML
- CSS
- JavaScript
- Ubuntu Server
- Docker
- Traefik

## Projede Öne Çıkan Noktalar

- form tabanlı randevu toplama yapısı
- test ride ve servis süreçleri için ayrı operasyon mantığı
- otomasyon odaklı backend yaklaşımı
- verilerin daha düzenli takip edilmesi
- düşük maliyetli ve geliştirilebilir sistem kurgusu
- gerçek bir işletme ihtiyacına göre düşünülmüş yapı

## Neden Bu Projeyi Yaptım?

Ben sadece kod yazmayı değil, bir problemin uçtan uca nasıl çözüldüğünü öğrenmek istiyorum.  
Bu yüzden ilgim sadece frontend ya da sadece backend ile sınırlı değil.

Benim ilgilendiğim alanlar daha çok:

- backend geliştirme
- otomasyon sistemleri
- iş süreçlerini dijitalleştirme
- sunucu ve deployment tarafı
- veri akışı ve entegrasyon mantığı
- gerçek dünyada işe yarayan yazılım çözümleri üretmek

Perraro Appointment da bu bakış açısıyla geliştirdiğim projelerden biri oldu.

## Detaylı Dokümantasyon

Sistemin mimarisi ve çalışma yaklaşımı hakkında daha detaylı bilgi için [`docs/architecture.md`](docs/architecture.md) dosyasına bakabilirsiniz.

## Repo Yapısı

Bu repo şu anda aşağıdaki şekilde düzenlenmiştir:

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

Durum
Bu repo şu anda geliştirme ve düzenleme aşamasındadır.
Bazı dosyalar sadeleştiriliyor, bazı workflow içerikleri paylaşılabilir hale getiriliyor ve proje portföy sunumuna uygun şekilde temizleniyor.

Kullanılan Araçlar ve Çalışma Süreci Notu

Bu projeyi geliştirirken bazı aşamalarda ChatGPT ve Claude gibi AI araçlarından destek aldım.
Bu destek; fikirleri netleştirme, dokümantasyon yazımı, açıklamaları düzenleme, yapı planlama ve bazı teknik bölümlerde düşünceyi toparlama konusunda yardımcı oldu.

Ancak proje kurgusu, sistem mantığı, dosya organizasyonu, kullanılan yaklaşım ve hangi yapının neden seçildiği tarafı doğrudan benim öğrenme ve geliştirme sürecimin bir parçası olarak şekillendi.

Bu yüzden bu repo benim için sadece ortaya çıkan çıktı değil, aynı zamanda nasıl düşündüğümü ve nasıl sistem kurmaya çalıştığımı gösteren bir çalışma.

Not

Bu repodaki bazı alanlar güvenlik ve gizlilik nedeniyle örneklenmiş, sadeleştirilmiş veya gizlenmiş olabilir.
Amaç, özel bilgileri paylaşmadan sistem tasarımını, düşünce yapısını ve proje yaklaşımını gösterebilmektir.

Geliştirici Notu

Bu proje benim için sadece bir ödev ya da basit bir demo değil.
Kendimi backend, otomasyon, sistem tasarımı ve gerçek iş süreçleri tarafında geliştirmek için oluşturduğum ciddi çalışmalardan biri.

Zamanla bu repoyu daha düzenli, daha açıklayıcı ve daha güçlü hale getirmeyi planlıyorum.
