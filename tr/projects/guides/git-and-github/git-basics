# DOSYA 1: Git Temelleri (Terminal ve Git Altyapısı)

Bu döküman, bilgisayarınızda yerel bir çalışma alanı kurarak tek bir dal üzerinde dosya üretme, yönetme ve kaydetme adımlarını eksiksiz şekilde kapsar.

---

## Bölüm 1: Temel Terminal Operasyonları

Git komutlarını doğru klasörde çalıştırabilmek ve dizinler arası kaybolmadan gezinebilmek için bu komutların tüm varyasyonlarına hakim olmalısınız. *(Not: `ls` ve `touch` komutlarının Windows CMD üzerinde çalışması için Git Bash veya PowerShell kullanılmalıdır.)*

### 1. Konum Tespiti ve Listeleme

#### pwd (Print Working Directory)
*   **Açıklama**: Terminalin o an bilgisayarda odaklandığı klasör yolunu kök dizinden başlayarak gösterir. Yanlış klasörde Git komutu çalıştırmamak için her işlem öncesi kontrol edilmelidir.
```bash
pwd
# Çıktı: /c/Users/Yazilimci/Desktop/projeler/web-sitesi
```

#### ls (List)
*   **Açıklama**: İçinde bulunduğunuz aktif klasörün altındaki tüm dosya ve klasörleri listeler. Parametreleri yardımıyla gizli Git dosyalarını ve dosya detaylarını görmenizi sağlar.
```bash
# 1. Senaryo: Sadece görünür dosya ve klasörleri listeleme
ls

# 2. Senaryo: Gizli dosyaları da (.git klasörü gibi) listeleme
ls -a

# 3. Senaryo: Dosya boyutları, oluşturulma tarihi ve izinleriyle detaylı listeleme
ls -l

# 4. Senaryo: Hem gizli dosyaları göster hem de detaylı listele (En sık kullanılan)
ls -la
```

### 2. Dizin Navigasyonu

#### cd (Change Directory)
*   **Açıklama**: Klasörler arasında geçiş yapmanızı sağlar. Klasör ağacında yukarı çıkmayı, kök dizine dönmeyi ve klasör isimlerindeki boşlukları yönetmeyi bilmek gerekir.
```bash
# 1. Senaryo: Bulunduğunuz konumdaki bir alt klasörün içine girme
cd Projeler

# 2. Senaryo: Bulunduğunuz konumdan tam BİR ÜST klasöre (ana dizine) çıkma
cd ..

# 3. Senaryo: Bulunduğunuz konumdan İKİ ÜST klasöre birden çıkma
cd ../..

# 4. Senaryo: Bilgisayardaki kullanıcı ana dizinine (Home) direkt geri dönme
cd ~

# 5. Senaryo: İsmi boşluk içeren bir klasörün içine girme (Tırnak işareti kullanımı)
cd "Yeni Proje Klasoru"
```

### 3. Dizin ve Dosya Manipülasyonu

#### mkdir (Make Directory)
*   **Açıklama**: Bulunduğunuz konuma yeni klasörler açar. Tek bir komutla iç içe geçmiş klasör ağaçları oluşturma yeteneğine sahiptir.
```bash
# 1. Senaryo: Bulunduğunuz konuma tek bir boş klasör oluşturma
mkdir e-ticaret-projesi

# 2. Senaryo: Tek komutla iç içe geçmiş alt klasör yapısı oluşturma (-p parametresi)
mkdir -p mobil-uygulama/src/components
```

#### touch
*   **Açıklama**: Bulunduğunuz klasörün içerisine uzantısıyla birlikte boş bir dosya yaratır. Aynı anda birden fazla farklı dosya türünü tek satırda oluşturabilir.
```bash
# 1. Senaryo: Tek bir boş dosya oluşturma
touch index.html

# 2. Senaryo: Tek satırda birden fazla farklı uzantılı dosya oluşturma
touch styles.css app.js README.md
```

---

## Bölüm 2: Git İlk Kurulum ve İzleme

Terminal komutlarıyla projenizin içine girdikten sonra, projenizi yönetmek için kullanacağınız ilk Git yapılandırma ve takip komutları aşağıdadır.

### 1. Kimlik Yönetimi

#### git config
*   **Açıklama**: Git sistemine küresel (global) veya projeye özel (local) kimlik tanımlar. Bu ayar yapılmazsa Git commit yapmanıza izin vermez.
```bash
# 1. Senaryo: Tüm bilgisayardaki tüm projeler için geçerli global kimlik tanımlama
git config --global user.name "Ahmet Yılmaz"
git config --global user.email "ahmet@ornek.com"

# 2. Senaryo: Sadece üzerinde çalıştığınız o projeye özel farklı bir kimlik tanımlama
git config --local user.name "Ahmet Sirket"
git config --local user.email "ahmet@sirket.com"

# 3. Senaryo: Mevcut tanımlı bilgileri terminalde kontrol etme
git config --list
```

### 2. Depo Başlatma

#### git init
*   **Açıklama**: Sıradan bir klasörü yerel Git deposu (repository) haline getirir. Arka planda tüm geçmişi yazacağı gizli `.git` klasörünü oluşturur.
```bash
# 1. Senaryo: Mevcut klasörün içinde Git takibini başlatma
git init

# 2. Senaryo: Belirtilen isimde yeni bir klasör oluşturup içini Git deposu olarak başlatma
git init sıfırdan-proje
```

### 3. Durum Analizi ve Kısa Raporlama

#### git status
*   **Açıklama**: Projenin o anki durumunun röntgenini çeker. Hangi dosyaların üzerinde değişiklik yapıldığını, hangilerinin kayıt kuyruğuna (Staging Area) alındığını gösterir.
```bash
# 1. Senaryo: Detaylı ve uzun durum raporu alma
git status

# 2. Senaryo: Kalabalık projelerde durumu tek satırda, kısa ve öz özetleme
git status -s
```

---

## Bölüm 3: Takip Mekanizması ve Kayıt

Git'in dosyaları nasıl işlediğini anlamak için dosya durum döngüsünü bilmek gerekir. Dosyalar şu 4 aşamadan geçer:
1.  **Untracked (Takip Edilmeyen)**: Projeye yeni eklenmiş, Git'in henüz varlığından haberdar olmadığı dosyalar.
2.  **Modified (Değiştirilmiş)**: Git'in zaten takip ettiği ama üzerinde yeni değişiklik yapılıp henüz kaydedilmediği dosyalar.
3.  **Staging (Hazırlık Alanı / Sahne)**: Bir sonraki commit'e dahil edilmek üzere paketlenmiş dosyalar.
4.  **Unmodified (Değiştirilmemiş)**: Commit atılarak yerel depoya kalıcı olarak kaydedilmiş, güncel dosyalar.

### 1. Sahneye Alma Varyasyonları

#### git add
*   **Açıklama**: Değişiklikleri hazırlık alanına (Staging Area) taşır. Git'e "Bir sonraki kayıt işlemine bu dosyaları dahil edeceğim" talimatını verir.
```bash
# 1. Senaryo: Sadece tek bir spesifik dosyayı hazırlık alanına ekleme
git add index.html

# 2. Senaryo: Projedeki yeni, silinen veya değiştirilen TÜM dosyaları topluca ekleme
git add .

# 3. Senaryo: Sadece belirli bir formattaki (örn: tüm CSS dosyaları) dosyaları ekleme
git add *.css
```

### 2. Güvenli Kayıt ve Mesaj Standartları

#### git commit
*   **Açıklama**: Hazırlık alanındaki dosyaları, benzersiz bir kimlik (SHA-1 kodu) atayarak yerel deponun geçmişine kalıcı bir versiyon olarak işler.
```bash
# 1. Senaryo: Standart mesajlı commit atma (En sık kullanılan)
git commit -m "Ana sayfa slider alanı kodlandı"

# 2. Senaryo: git add yapmayı unuttuğunuz değiştirilmiş dosyaları otomatik ekleyip commit etme (-am)
# (Kritik Not: Bu komut tamamen yeni oluşturulmuş [untracked] dosyaları kapsamaz, sadece değiştirilenleri kapsar)
git commit -am "CSS renk düzeltmeleri yapıldı"
```

---

## Bölüm 4: Görünmez Duvar: .gitignore

### 1. .gitignore Nedir, Neden Hayatidir?
Projenizde Git tarafından takip edilmesi gerekmeleyen, uzak sunucuya (GitHub) gönderilmesi güvenlik riski yaratan veya projenin boyutunu gereksiz büyütün dosyalar vardır. 
*   **node_modules**: Harici kütüphaneler (Herkes kendi bilgisayarında indirebilir, depolanmamalıdır).
*   **Çalışma Ortamı Dosyaları (.env)**: Veritabanı şifreleri, API anahtarları gibi gizli kalması gereken bilgiler.
*   **İşletim Sistemi Dosyaları (.DS_Store, thumbs.db)**: Sistemlerin otomatik ürettiği çöp dosyalar.

Bu dosyaların isimlerini veya uzantılarını projenin kök dizinine oluşturacağınız `.gitignore` isimli düz bir metin dosyasına yazarak Git'in bunları tamamen görmezden gelmesini sağlarsınız.

### 2. Sözdizimi Kuralları
```text
# 1. Belirli bir dosyayı gizleme
.env

# 2. Belirli bir klasörü ve içindeki her şeyi gizleme
node_modules/
dist/

# 3. Belirli bir uzantıya sahip tüm dosyaları gizleme
*.log
*.exe

# 4. İstisnalar Tanımlama (Başına ünlem koyarak "bunu gizleme" denir)
# Tüm log dosyalarını gizle ama sadece önemli.log dosyasını takip et:
*.log
!önemli.log
```

### 3. Kriz Senaryosu: Geç Kalınan .gitignore Dosyası
*   **Problem**: Projenizde `.env` dosyasını oluşturdunuz, commit ettiniz ve Git hafızasına aldı. Daha sonra aklınıza geldi ve `.env` dosyasını `.gitignore` içine yazdınız. Ancak dosya hala `git status` ekranında görünmeye ve takip edilmeye devam eder. Çünkü Git, halihazırda takip ettiği dosyayı bırakmaz.
*   **Çözüm**: Dosyayı bilgisayarınızdan silmeden, sadece Git'in hafızasından (önbelleğinden) çıkarmalısınız.

```bash
# Kriz Çözüm Adımı: Dosyayı diskten silmeden sadece Git takibinden çıkarır
git rm --cached .env

# Bu işlemden sonra durumu doğrulamak için commit atılır:
git commit -m "Kriz Çözüldü: .env dosyası hafızadan silindi ve gitignore'a emanet edildi"
```
