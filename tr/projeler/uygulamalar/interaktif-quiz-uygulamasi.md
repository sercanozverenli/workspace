# İnteraktif Quiz Uygulaması (Sınav Simülatörü)

Bilişim sistemleri ve bilgisayar programcılığı müfredatında yer alan (Veri Yapıları, Unix Sistem Yönetimi, Mobil Uygulama Geliştirme vb.) birçok farklı dersi tek bir çatı altında toplayan; öğrencilerin vize, final ve ünite sonu değerlendirmelerini pratik etmelerini sağlayan kapsamlı bir sınav simülatörüdür.

### ⚙️ Sistem Mekaniği ve Özellikler
Uygulama, bilişsel yükü azaltan ve öğrenmeyi pekiştiren bir mimariyle tasarlanmıştır:

* **Çoklu Ders ve Kategori Seçimi:** Kullanıcılar; ilgili dönemi, çalışmak istedikleri spesifik dersi ve test türünü (Ünite Testi, Ara Sınav veya Final) seçerek spesifik bir soru havuzuna giriş yaparlar.
  
  ![Dönem ve Ders Seçimi](../../../docs/assets/interactive-quiz-app/int_quiz_1.PNG ':size=35%')  ![Alt Kategori Seçimi](../../../docs/assets/interactive-quiz-app/int_quiz_2.PNG ':size=35%')

* **Anında Geri Bildirim ve Detaylı Açıklamalar:** Klasik test çözme mantığının ötesinde, kullanıcı bir şıkkı işaretlediğinde sistem anında renk kodlarıyla (Doğru: Yeşil, Yanlış: Kırmızı) tepki verir. Ayrıca her sorunun altında yer alan "Açıklama" butonu ile hatanın nedeni veya konunun detayı anında öğrenilebilir. Testler arası geçişi kolaylaştırmak için sayfalandırma (Part 1, Part 2) özelliği bulunmaktadır.
  
  ![Quiz Arayüzü](../../../docs/assets/interactive-quiz-app/int_quiz_3.PNG ':size=35%')

* **Karanlık Mod (Dark Mode) Entegrasyonu:** Uzun süreli çalışmalarda göz yorgunluğunu önlemek amacıyla sisteme tam entegre bir Karanlık Mod eklenmiştir. Kullanıcının tema tercihi tarayıcı önbelleğinde (`localStorage`) tutularak sayfa geçişlerinde kalıcılık sağlanır.
  
  ![Karanlık Mod](../../../docs/assets/interactive-quiz-app/int_quiz_4.PNG ':size=35%')

* **Gelişmiş Sonuç Analizi (Modal):** Test bitirildiğinde tetiklenen algoritma, kullanıcının sınav performansını hesaplayarak doğru, yanlış ve boş bırakılan soru sayılarını dinamik bir pop-up (modal) ekranında raporlar. Rastgelelik (randomization) algoritmalarıyla desteklenen soru yapıları, ezberden ziyade öğrenmeyi test eder.
  
  ![Sonuç Ekranı](../../../docs/assets/interactive-quiz-app/int_quiz_5.PNG ':size=35%')


### Kullanılan Teknolojiler (Tech Stack)
* **Arayüz ve Mobil Uyumluluk:** HTML5, CSS3, Bootstrap 4.5.2
* **DOM Manipülasyonu ve Etkileşim:** jQuery 3.5.1, Vanilla JS *(Soru validasyonları, tema geçişleri, filtreleme mantığı ve asenkron veri işlemleri)*
* **Durum Yönetimi (State Management):** LocalStorage *(Kullanıcı arayüzü tercihlerinin hafızada tutulması için)*
* **Mobil Dağıtım:** Geliştirilen web mimarisi, APK Builder aracı kullanılarak dağıtıma hazır Android (`.apk`) formatına dönüştürülmüştür.

---

### Kaynak Kodları ve Kurulum
Uygulamanın web tabanlı kaynak kodlarına ve derlenmiş Android sürümüne aşağıdaki bağlantılardan ulaşabilirsiniz:

**[GitHub Kaynak Kodları](https://github.com/sercanozverenli/web_and_mobile_apps/tree/main/Interactive_Quiz_App/HTML_Source)** <br>
**[Android APK Dosyası](https://github.com/sercanozverenli/web_and_mobile_apps/blob/main/Interactive_Quiz_App/Android_Build/Interactive_Quiz_App_1_1.0.apk)**

---

> <small>*⚠️ **Yasal Uyarı ve Sorumluluk Reddi (Disclaimer)**<br> Bu proje tamamen eğitim, araştırma ve kişisel portföy sergileme amacıyla ticari bir amaç güdülmeden geliştirilmiştir. Proje içeriğinde yer alabilecek üçüncü taraflara ait her türlü materyalin (görsel, ses, metin vb.) telif ve fikri mülkiyet hakları asıl sahiplerine aittir.*</small>
> 
> <small>*Projeyi veya kaynak kodlarını kullanan, çoğaltan veya kendi çalışmalarına entegre eden üçüncü şahıslar, ilgili materyallerin lisans ve telif gereksinimlerine uymakla yegâne sorumludur. Proje geliştiricisi; içeriklerin veya kodların yetkisiz ticari kullanımından, dağıtımından veya doğabilecek herhangi bir telif hakkı ihlalinden dolayı hiçbir yasal sorumluluk kabul etmez. Projeyi kullanan herkes bu şartları peşinen kabul etmiş sayılır.*</small>
