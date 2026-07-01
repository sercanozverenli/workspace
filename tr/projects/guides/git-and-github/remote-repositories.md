# Uzak Depo Entegrasyonu ve Takım Çalışması (GitHub/GitLab)

Bu doküman; yerel bilgisayarınızda (local) geliştirdiğiniz Git projelerini bulut tabanlı uzak sunuculara (remote) bağlamayı, ekip arkadaşlarınızla kod senkronizasyonu yapmayı ve veri aktarım komutlarının arka plan mimarisini eksiksiz kapsar.

---

## Bölüm 1: Projeyi Kopyalama ve Sunucu Bağlantısı

Yerel ortamınız ile uzak sunucu arasındaki köprüyü kurmak için iki temel senaryo mevcuttur: Sıfırdan bir projeyi bilgisayarınıza indirmek veya yereldeki mevcut bir projeyi uzak sunucuya tanıtmak.

### 1. git clone

#### Açıklama
Uzak sunucuda (GitHub, GitLab, Bitbucket vb.) halihazırda var olan bir depoyu, tüm geçmiş commit kayıtları, dalları (branch) ve etiketleriyle birlikte yerel bilgisayarınıza bir klasör olarak kopyalar. Bu işlem otomatik olarak uzak depo bağlantısını da yapılandırır.

```bash
# 1. Senaryo: Projeyi mevcut terminal konumuna, uzak depodaki aynı klasör ismiyle indirme
git clone https://github.com

# 2. Senaryo: Projeyi indirirken yerel bilgisayardaki hedef klasör adını kendiniz belirleme
git clone https://github.com ozel-klasor-adi
```

### 2. git remote

#### Açıklama
Yerelde başlatılmış (`git init`) bir projenin, buluttaki hangi uzak depo adresiyle haberleşeceğini yönetir. Bir projenin birden fazla uzak depo bağlantısı olabilir.

```bash
# 1. Senaryo: Yerel depoya "origin" takma adıyla yeni bir uzak sunucu adresi ekleme
git remote add origin https://github.com

# 2. Senaryo: Yerel deponun bağlı olduğu uzak sunucu adreslerini ve takma adlarını listeleme
git remote -v
# Çıktı:
# origin  https://github.com (fetch)
# origin  https://github.com (push)

# 3. Senaryo: Mevcut bir uzak deponun URL adresini değiştirme/güncelleme
git remote set-url origin https://github.com
```

---

## Bölüm 2: Veri Gönderimi ve Senkronizasyon

Kodların yerel ve uzak depolar arasında güvenli bir şekilde taşınması, belirli akış parametrelerine tabidir.

### 1. git push

#### Açıklama
Yerel bilgisayarınızda tamamladığınız ve `git commit` ile mühürlediğiniz kayıtları uzak sunucuya yükler.

```bash
# 1. Senaryo: Yeni bir dalı uzak sunucuya İLK KEZ gönderirken yukarı akış (upstream) bağı kurma
# Bu komut yerel "main" dalını uzak "origin/main" dalına kalıcı olarak bağlar.
git push -u origin main

# 2. Senaryo: Upstream bağı kurulduktan sonraki süreçlerde sadece standart push yapma
# Git otomatik olarak hangi dalın nereye gideceğini bilir.
git push

# 3. Senaryo: Yerel bir dalı uzak sunucuda farklı bir isimle yayınlama
git push origin main:sunucu-main-dali
```

### 2. git fetch

#### Açıklama
Uzak depoda meydana gelen tüm değişiklikleri, yeni dalları ve commit'leri yerel bilgisayarınıza indirir; ancak **üzerinde çalıştığınız aktif kodlara kesinlikle dokunmaz**. Sadece yerelinizdeki uzak depo haritasını (metadata) günceller.

```bash
# Tüm uzak dallardaki güncel commit bilgilerini yerele indirme
git fetch origin
```

### 3. git pull

#### Açıklama
Uzak depodaki güncel değişiklikleri bilgisayarınıza indirir ve üzerinde çalıştığınız aktif kod dalıyla **otomatik olarak birleştirir**.

```bash
# Uzak depodaki main dalını çekip aktif yerel dala entegre etme
git pull origin main
```

---

## Bölüm 3: Mimari Analiz: git fetch vs git pull

Bu iki komut arasındaki fark, kod güvenliği ve ekip çalışması senaryolarında kritik bir öneme sahiptir.

### 1. git pull Komutunun Arka Planı
`git pull` aslında tek başına bir komut değildir. Arka planda sırasıyla şu iki komutu ardışık olarak çalıştıran bir kısayoldur:
\[\text{git pull} = \text{git fetch} + \text{git merge}\]

```text
[Uzak Sunucu] ------( git fetch )------> [Yerel Uzak Haritası (origin/main)]
                                                        |
                                                 ( git merge )
                                                        |
                                                        v
                                             [Aktif Çalışma Alanınız]
```

### 2. Yapısal Karşılaştırma

| Özellik | git fetch | git pull |
| :--- | :--- | :--- |
| **Kod Güvenliği** | Güvenlidir. Mevcut kodlarınızı değiştirmez veya bozmaz. | Risk barındırır. Yereldeki satırların üzerine yazabilir veya Merge Conflict tetikleyebilir. |
| **İşlev** | Sadece bilgiyi ve commit geçmişini indirir. | Hem bilgiyi indirir hem de yerel kod tabanına hemen birleştirir. |
| **Kullanım Amacı** | Ekip arkadaşlarının ne yaptığını, hangi dalları açtığını güvenle incelemek için. | Kendi kodunuzu geliştirmeye başlamadan önce projeyi en güncel haline getirmek için. |

---

## Bölüm 4: Güvenli Çalışma Pratiği

Büyük projelerde doğrudan `git pull` yapmak yerine, önce `git fetch` ile değişiklikleri incelemek, ardından kontrollü bir şekilde birleştirmek kod sağlığı açısından daha profesyonel bir yaklaşımdır:

```bash
# Adım 1: Uzaktaki durum bilgilerini güvenle indir
git fetch origin

# Adım 2: Kendi dalınız ile uzaktan gelen dal arasındaki farkları inceleyin
git diff main..origin/main

# Adım 3: Herhangi bir çakışma riski görmüyorsanız güvenle birleştirin
git merge origin/main
```

