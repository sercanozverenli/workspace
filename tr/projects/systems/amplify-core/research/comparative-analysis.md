# Amplify Core:
# Veri Güvenilirliği ve Karar Yönlendirme Sistemi (Data Reliability & Decision Routing Systemi)

## Karşılaştırmalı Analiz

Makine öğrenmesi ve veri yönetimi literatüründeki mevcut çalışmalar incelendiğinde, karar sistemlerini güvence altına almaya yönelik yaklaşımların "Veri Kalitesi ve Güvenilirlik", "Karar Yönlendirme (Routing)" ve "Karar Kaçınması (Abstention)" olmak üzere üç ana alt disiplinde toplandığı görülmektedir. 

Aşağıdaki analiz, bu disiplinlerdeki temel akademik referansları ve endüstri standartlarını, Amplify Core'un sunduğu dört temel mimari bileşen ekseninde karşılaştırmaktadır:

1. **Güvenilirlik Ölçümü:** Verinin karar öncesi istatistiksel sağlığının ölçülmesi.
2. **Yönlendirme:** Verinin durumuna göre farklı karar rejimlerine aktarılması.
3. **Karar Kaçınması:** Bilgi çöküşü anlarında tahminden kaçınma.
4. **Modelden Bağımsızlık:** Herhangi bir modele dışarıdan entegre edilebilme.

### Literatür Karşılaştırma Tablosu

| Çalışma / Yaklaşım | Güvenilirlik Ölçümü | Karar Yönlendirme | Karar Kaçınması | Modelden Bağımsızlık | Temel Sınırlılık / Odak Noktası |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Simard vd. (2019)** | ✔️ | ❌ | ❌ | ✔️ | Otonom yönlendirme veya kaçınma yoktur; statik skorlama yapar. |
| **Chug vd. (2021)** | ✔️ | ❌ | ❌ | ✔️ | Otonom karar mekanizması içermez; temel statik yapı sunar. |
| **Polyzotis & Zaharia (2021)** | ✔️ | ❌ | ❌ | ✔️ | Altyapı ve metrik izlemeye odaklanır; dinamik karar/yönlendirme sunmaz. |
| **Breck vd. (2019)** | ✔️ | ❌ | ❌ | ✔️ | Başarılı bir veri doğrulama sistemidir; ancak kalitesine göre yönlendirme yapmaz. |
| **Bayram vd. (2024)** | ✔️ | ❌ | ❌ | ❌ | Doğrudan ana modele bağımlıdır ve otonom bir yönlendirme katmanı eksiktir. |
| **Jacobs vd. (1991)** | ❌ | ✔️ | ❌ | ❌ | Veri güvenilirliğini önceden ölçmez; doğrudan sinir ağı mimarisine odaklıdır. |
| **Woods vd. (1997)** | ❌ | ✔️ | ⚠️ | ✔️ | Verinin kendisini değerlendirmez; sınıflandırıcı seçimi odaklıdır. |
| **Chen vd. (2025)** | ❌ | ✔️ | ✔️ | ❌ | Katı bir şekilde modele bağımlıdır (Sadece Text-to-SQL alanına özgüdür). |
| **Kadve vd. (2025)** | ❌ | ✔️ | ⚠️ | ✔️ | Karar öncesi veri güvenilirliği ölçümü yoktur; yalnızca çıkarım sonrası (post-inference) çalışır. |
| **Chow (1970)** | ❌ | ❌ | ✔️ | ✔️ | Karar kaçınması üzerine teorik temeller sunar; modern işlem hattına entegre yönlendirme içermez. |
| **Hendrickx vd. (2024)** | ❌ | ❌ | ✔️ | ✔️ | Tarama/teorik makalesidir; modern işlem hattına bütünleşik sistem önermez. |
| **Geifman & El-Yaniv (2017)** | ❌ | ❌ | ✔️ | ❌ | Veriyi değil, modelin güven skorunu (confidence) temel alır; tamamen modele bağımlıdır. |
| **SelectiveNet (2019)** | ❌ | ❌ | ✔️ | ❌ | Doğrudan derin sinir ağı mimarisine entegre çalışır. |
| **Amplify Core (DRDRS)** | ✔️ | ✔️ | ✔️ | ✔️ | **Tüm bileşenleri karar öncesi (pre-inference) otonom çalıştırır. (Geniş ölçekli doğrulama gerektiren PoC aşamasındadır)** |

*(✔️: Kapsar, ❌: Kapsamaz, ⚠️: Kısmen / Farklı Yöntemle)*

### Sentez

Mevcut çalışmaların büyük çoğunluğu, ilgili problemin yalnızca bir veya iki bileşenine odaklanmaktadır. Literatürde; birbirinden kopuk bu üç disiplini tek bir işlem hattında (pipeline) birleştirerek "sahte kesinlik" (false confidence) sorununa yapısal bir çözüm sunan bütünleşik bir mimari bulunmamaktadır. Amplify Core, verinin güvenilirliğini bağımsız olarak ölçüp yönlendiren yapısıyla bu eksikliği gidererek, yüksek riskli sistemler için evrensel bir denetim noktası (checkpoint) önermektedir.
