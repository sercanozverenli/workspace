# Geçici Hafıza Yönetimi (git stash)

Bu doküman; henüz commit atmaya hazır olmadığınız yarıda kalmış değişikliklerinizi kaybetmeden güvenli bir zula alanına (temporary storage) kaldırmayı, dallar arasında esnekçe hareket etmeyi ve zula verilerini yönetmenin tüm mimari detaylarını kapsar.

---

## Bölüm 1: Git Stash Mantığı ve Zulaya Ekleme Senaryoları

### 1. Git Stash Nedir, Neden Hayatidir?
Çalıştığınız dalda (branch) henüz tamamlanmamış, yarım kalmış kodlarınız varken acil bir hatayı çözmek için başka bir dala geçmeniz gerekebilir. Kodlarınız yarım olduğu için commit atmak istemezsiniz; ancak değişiklikleri kaydetmeden dal değiştirmeye çalışırsanız Git buna izin vermez veya kodlarınız kaybolma riskiyle karşı karşıya kalır. 

`git stash` komutu, çalışma alanınızdaki (Working Directory) ve hazırlık alanındaki (Staging Area) tüm değişiklikleri paketler, yerel depoda güvenli bir **geçici hafıza kuyruğuna (zula)** atar ve çalışma alanınızı tamamen temiz (clean) hale getirir.

### 2. Komutlar ve Varyasyonlar

#### git stash
*   **Açıklama**: Takip edilen (tracked) dosyalardaki tüm değişiklikleri otomatik bir isim atayarak zulanın en üstüne ekler.
```bash
# Standart zulaya kaldırma işlemi
git stash
# Çıktı: Saved working directory and index state WIP on main: c2b3a1d Initial commit
```

#### git stash save "mesaj"
*   **Açıklama**: Zulanın ileride kolayca hatırlanabilmesi için özel bir açıklama notu eklenerek kaydedilmesini sağlar. (Modern Git versiyonlarında `git stash push -m "mesaj"` kullanımı da aynı işlevi görür).
```bash
git stash save "Ödeme butonu yarıda kalan CSS düzenlemeleri"
```

#### git stash -u (veya --include-untracked)
*   **Açıklama**: Standart `git stash` komutu projeye yeni eklenmiş ve henüz Git'e tanıtılmamış (`untracked`) dosyaları kapsamaz. Yeni oluşturulan dosyaları da zulaya dahil etmek için bu parametre zorunludur.
```bash
# Yeni eklenen dosyalarla birlikte her şeyi geçici hafızaya al
git stash -u
```

---

## Bölüm 2: Zula İnceleme ve Yönetimi

Zulaya eklenen her bir işlem, bir yığın (stack) yapısında saklanır. En son eklenen zula her zaman listenin en üstünde yer alır ve `stash@{0}` indeksi ile temsil edilir.

### 1. git stash list
*   **Açıklama**: Geçici hafızaya alınmış, henüz geri yüklenmemiş tüm zula kayıtlarını indeks numaraları ve eklenen mesajlarla birlikte listeler.
```bash
git stash list
# Çıktı:
# stash@{0}: On main: Ödeme butonu yarıda kalan CSS düzenlemeleri
# stash@{1}: WIP on feature-login: d4e5f6a Login yapısı başlandı
```

### 2. git stash show
*   **Açıklama**: Zuladaki kodların içeriğini bozmadan, hangi dosyaların içinde kaç satırlık değişiklik yapıldığını özetler. `-p` parametresi eklenirse yapılan değişiklikleri satır satır kod düzeyinde (diff formatında) gösterir.
```bash
# 1. Senaryo: En son zulaya atılan kaydın dosya bazlı özetini görme
git stash show

# 2. Senaryo: Spesifik bir zula kaydının içindeki satır satır kod değişikliklerini inceleme
git stash show -p stash@{1}
```

---

## Bölüm 3: Zuladan Geri Getirme ve Temizlik Operasyonları

İşinizi tamamlayıp eski yarım kalan kodlarınıza dönmek istediğinizde, zulanın içindeki kodları çalışma alanınıza geri yüklemeniz gerekir. Bunun için iki farklı strateji mevcuttur.

### 1. git stash pop (Getir ve Zulanın İçinden Sil)
*   **Açıklama**: Belirtilen zula kaydını alır, çalışma alanınıza geri yükler ve **zula listesinden (hafızadan) kalıcı olarak siler**. Eğer indeks belirtilmezse en son eklenen `stash@{0}` kaydını işleme alır.
```bash
# En son zulaya atılan işi geri yükle ve listeden temizle
git stash pop

# Spesifik bir indeksteki işi geri yükle ve listeden temizle
git stash pop stash@{1}
```

### 2. git stash apply (Getir ama Zulada Korusun)
*   **Açıklama**: Zulanın içindeki kodları çalışma alanınıza geri yükler ancak **zula listesinden silmez**. Aynı değişiklikleri birden fazla farklı dalda (branch) denemek veya kodları hafızada bir yedek olarak tutmak istediğiniz durumlarda tercih edilir.
```bash
# Kodları geri yükle ama stash@{0} olarak zula listesinde tutmaya devam et
git stash apply
```

### 3. Zula Havuzunu Temizleme

#### git stash drop
*   **Açıklama**: Zuladan geri yükleme yapmaksızın, sadece belirtilen indeks numarasındaki zula kaydını hafızadan kalıcı olarak siler.
```bash
git stash drop stash@{0}
```

#### git stash clear
*   **Açıklama**: Zula listesindeki tüm kayıtları tek bir komutla geri dönüşü olmayacak şekilde tamamen temizler. Havuzu sıfırlar.
```bash
git stash clear
```

