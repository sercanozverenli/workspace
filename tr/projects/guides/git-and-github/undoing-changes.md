# Kod Geri Alma ve Hata Kurtarma Yöntemleri (Reset vs Revert)

Bu doküman; projede yapılan hatalı geliştirmeleri, yanlış atılan commit'leri veya istenmeyen kod satırlarını geçmiş yapısını bozmadan veya kontrollü bir şekilde geriye sararak temizleme yöntemlerini ve bunların altyapı mimarisini kapsar.

---

## Bölüm 1: Mimari Farklar: git reset ve git revert

Hatalı bir işlemi geri alırken seçilecek komut, projenin tek başınıza mı yoksa bir ekiple (uzak sunucu üzerinde ortaklaşa) mi geliştirildiğine göre değişir.

### 1. git reset (Geçmişi Yeniden Yazmak)
*   **Çalışma Mantığı**: HEAD işaretçisini ve aktif dalın ucunu geçmişteki belirli bir commit noktasına doğrudan geri çeker. O noktadan sonra atılmış olan tüm commit'leri geçmiş listesinden tamamen siler.
*   **Güvenlik Riski**: Sadece henüz uzak sunucuya (`push` edilmemiş) gönderilmemiş yerel commit'lerde kullanılmalıdır. Uzak sunucuya gönderilmiş dallarda `reset` kullanımı, takım arkadaşlarınızın commit geçmiş haritasını bozacağı için senkronizasyon krizlerine yol açar.

```text
[Önce]
A --- B --- C --- D (main, HEAD)

[git reset --hard B sonrası]
A --- B (main, HEAD)   [C ve D commit'leri geçmişten tamamen silindi]
```

### 2. git revert (Güvenli Geçmiş Oluşturmak)
*   **Çalışma Mantığı**: Geçmişteki hatalı bir commit'i listeden silmez. Aksine, o commit'in yaptığı tüm değişikliklerin tam tersini yapan **yeni bir düzeltme commit'i (anti-commit)** oluşturur.
*   **Güvenlik Avantajı**: Geçmişi silmediği, üzerine yeni bir kayıt eklediği için uzak sunucuya gönderilmiş (`public`) ortak dallarda kullanımı tamamen güvenlidir. Takım çalışmasını bozmaz.

```text
[Önce]
A --- B --- C --- D (main, HEAD)

[git revert C sonrası]
A --- B --- C --- D --- E (main, HEAD)  [E commit'i, C'nin yaptığı değişiklikleri iptal eder]
```

---

## Bölüm 2: git reset Modları ve Derinlemesine İnceleme

`git reset <commit-id>` komutu çalıştırılırken yanına eklenen parametreler (flag), geri çekilen commit'lerin içindeki kod dosyalarının bilgisayarınızda hangi aşamada (Sahne, Çalışma Alanı veya Çöp) kalacağını belirler.

### 1. --soft Modu (En Güvenli Geri Sarım)
*   **Açıklama**: Belirtilen commit noktasına geri dönerken, silinen commit'lerin içindeki kod değişikliklerine kesinlikle dokunmaz. Bu kodları doğrudan **Hazırlık Alanında (Staging Area / Sahne)** tutar.
*   **Kullanım Senaryosu**: Son attığınız commit'in mesajını değiştirmek veya son 2-3 commit'i tek bir temiz commit halinde yeniden birleştirmek istediğinizde tercih edilir.

```bash
# Son yapılan commit'i iptal et ama kodları sahnede hazır tut
git reset --soft HEAD~1
```

### 2. --mixed Modu (Varsayılan Mod)
*   **Açıklama**: Eğer komutun yanına hiçbir parametre yazmazsanız bu mod çalışır. Belirtilen commit noktasına geri dönerken, iptal edilen commit'lerdeki kodları **Çalışma Alanına (Working Directory)** yani un-staged aşamasına geri bırakır. Kodlarınız silinmez ancak `git add` yapılmamış ham haline döner.
*   **Kullanım Senaryosu**: Kodlar üzerinde biraz daha çalışıp, dosyaları farklı parçalar halinde yeniden organize ederek ayrı ayrı commit atmak istediğinizde kullanılır.

```bash
# Son commit'i iptal et, kodları çalışma alanına ham değişiklik olarak bırak
git reset --mixed HEAD~1
# Veya parametresiz doğrudan kullanım:
git reset HEAD~1
```

### 3. --hard Modu (Tehlikeli ve Geri Dönüşsüz)
*   **Açıklama**: Belirtilen commit noktasına geri dönerken, o noktadan sonra yapılan tüm commit'leri, hazırlık alanındaki verileri ve çalışma alanında yazdığınız tüm kod satırlarını **tamamen siler ve yok eder**.
*   **Kullanım Senaryosu**: Yaktığınız geliştirmeler tamamen çıkmaza girdiğinde, yazdığınız her şeyi çöpe atıp projenin çalışan son kararlı commit haline tertemiz geri dönmek istediğinizde kullanılır.

```bash
# Son commit'ten sonra yapılan HER ŞEYİ tamamen sil ve o ana geri dön
git reset --hard HEAD~1
```

---

## Bölüm 3: git revert ile Güvenli Geri Alma

### git revert
*   **Açıklama**: Belirtilen commit ID'sinin içeriğini analiz eder, o kayıtta eklenen satırları siler, silinen satırları geri ekler ve bu zıt işlem için terminalde otomatik bir commit mesajı ekranı açarak yeni bir kayıt oluşturur.

```bash
# 1. Senaryo: Geçmişteki spesifik bir hatalı commit'i güvenle iptal etme
git revert a1b2c3d

# 2. Senaryo: Otomatik commit mesajı editörünün açılmasını engelleyerek direkt revert etme
git revert --no-commit a1b2c3d
```

---

## Bölüm 4: Durum Kontrolü ve Kod Karşılaştırma (git diff)

Geri alma operasyonlarından önce veya sonra, projenin hangi sürümünde neyin değiştiğini anlamak için `git diff` ile doğrulama yapılması sürecin hatasız ilerlemesini sağlar.

```bash
# 1. Senaryo: Şu anki çalışma alanınız ile geçmişteki bir commit arasındaki farkı görme
git diff HEAD~2

# 2. Senaryo: Revert atmadan önce o commit'in tam olarak neyi değiştirdiğini inceleme
git diff a1b2c3d~1..a1b2c3d
```

