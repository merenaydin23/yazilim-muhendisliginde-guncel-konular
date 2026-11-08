# 📊 SWOT Analizi — Mirka Smart WoodSander 5000
**Tarih:** 8 Kasım 2026  
**Hazırlayan:** Eren Aydın (@Eren Aydın)  
**Makine:** Mirka Smart WoodSander 5000 (Endüstriyel Ahşap Zımpara Makinesi)  
**Kapsam:** Safety 4.0 & Cyber-Physical Systems (LAB 1–7 Föyleri Analizi)  

---

## 📌 Genel Değerlendirme

Mirka Smart WoodSander 5000, yüksek devirli zımpara kafalı ve akıllı (bağlantılı) bir makine olarak güçlü bir üretim ve kalite avantajına sahip; en büyük açığı, bu bağlantının getirdiği siber-emniyet riskidir. Asıl strateji, safety fonksiyonunu dijital ağdan ayırarak bu riski kapatmak ve bunu bir güven avantajına çevirmektir.

*Analiz, makine üzerinde doldurduğumuz LAB 1–7 föylerine ve tipik endüstriyel ahşap zımpara makinesi kabullerine dayanır; üretici verisi veya gerçek saha sonuçları içermez. Kendi rakamlarınızla (verim, arıza süresi, maliyet) doğrulayıp düzeltin.*

---

## 🧭 SWOT Matrisi

### 🏢 İç Faktörler

| Güçlü Yönler (Strengths - S) | Zayıf Yönler (Weaknesses - W) |
| :--- | :--- |
| • **Yüksek devirli zımpara kafaları:** Hızlı, yüksek verimli yüzey işleme kapasitesi. | • **Uzak erişim yolu dijital kesişim noktası:** Yanlış kurulursa safety konfigürasyonuna ulaşır. |
| • **Akıllı yapı:** Kamera tabanlı kusur denetimi ve parametre önerisiyle tutarlı kalite. | • **Paylaşılan hesap riski:** Sürekli açık erişim ve eksik oturum kaydı riski. |
| • **Ayrı safety yolu:** E-stop, kapı kilidi, ışık perdesi $\to$ Safety PLC $\to$ STO ile insan korunması. | • **PLC firmware kütüphanelerindeki zafiyetler:** (örn. Component X 2.4) ve yama sonrası safety yeniden doğrulama yükü. |
| • **Uzaktan servis ve güncelleme:** Hızlı bakım, kısa duruş süresi. | • **YZ modelinin kırılganlığı:** Yanlış sınıflandırmaya ve manipüle edilmiş girdiye açık olması. |
| • **Savunulabilir mimari:** Net bölge/geçit (zone/conduit) yapısıyla koruma. | • **Doğuştan tehlikeler:** Yanıcı ahşap tozu ve yüksek devirli kafaların oluşturduğu fiziksel riskler. |

---

### 🌐 Dış Faktörler

| Fırsatlar (Opportunities - O) | Tehditler (Threats - T) |
| :--- | :--- |
| • **Siber güvenlik ve emniyet kanıtı:** Evidence Pack müşteri güveni ve satışta fark yaratır. | • **Yetkisiz erişim:** Çalınmış servis hesabıyla yetkisiz erişim ve konfigürasyon değişikliği. |
| • **Akıllı fabrika talebi:** Veri odaklı kalite taleplerinin sektörde artması. | • **Üretim durması:** Fidye yazılımı (ransomware) veya ofis ağından yayılan saldırılarla üretimin durması. |
| • **Tahmine dayalı bakım:** Kafa/bant aşınması izleme ile ek servis ve hizmet geliri. | • **Tedarik zinciri zafiyetleri:** Üçüncü taraf bileşenler, SBOM eksiği. |
| • **Mevzuata erken hazırlık:** CRA (Cyber Resilience Act) ve Makine Emniyeti Yönetmeliği erken uyum avantajı. | • **Yasal yaptırımlar:** Bildirim yükümlülükleri (24s / 72s / 14 gün) ve uyumsuzluk cezaları. |
| • **Sürdürülebilirlik:** Toz yönetimi ve enerji verimliliğiyle sürdürülebilirlik avantajı. | • **Pazar rekabeti:** Rakiplerin daha güvenli veya daha ucuz akıllı makinelerle pazara girmesi. |

---

## 🎯 Stratejik Çıkarımlar

| Strateji Türü | Tanım | Eylem ve Uygulama |
| :--- | :--- | :--- |
| **SO (Güçlüyü Fırsatla Büyüt)** | Güçlü yönleri fırsatlarla eşleştirme | Ayrı safety mimarisini ve Evidence Pack'i satış argümanı yap; *"İnsan güvenliği ağdan bağımsız"* mesajıyla akıllı fabrika müşterilerini hedefle. |
| **WO (Zayıfı Fırsatla Kapat)** | Zayıf yönleri fırsatlarla iyileştirme | Uzak erişimi Jump Server + VPN + MFA + kişisel hesap + tam oturum kaydı + varsayılan kapalı modeline taşı; tahmine dayalı bakım hizmetini bu güvenli kanal üzerinden sun. |
| **ST (Güçlüyü Tehditle Koru)** | Güçlü yönlerle tehditlere kalkan olma | Safety zone'u normal kontrol ve uzak erişimden izole tut; saldırgan içeri girse bile STO'nun donanımsal çalışmasını düzenli test et. |
| **WT (Zayıf ve Tehdit Birleşimini Önle)** | Savunma ve kriz yönetimi | SBOM'u canlı tut, kritik CVE'lerde önce testli yama uygula; YZ girdi doğrulama, güven eşiği ve fallback ekle; olay müdahale akışını (24s / 72s / 14 gün) önceden prova et. |

---

## 🚀 İlk 5 Öncelikli Eylem

1. [ ] **Uzak erişim güvenliği:** Uzak erişimi paylaşılan hesaptan kişisel hesaba, MFA'ya ve tam oturum kaydına geçir.
2. [ ] **Safety izolasyonu:** Safety PLC'yi ayrı bölgeye al; program yüklemeyi yalnızca yerel ve donanımsal anahtarlı yap.
3. [ ] **SBOM & Zafiyet denetimi:** SBOM çıkar; Component X 2.4 için üç şartı (bileşen, sürüm, ulaşılabilirlik) kontrol et.
4. [ ] **Toz emme & Emniyet entegrasyonu:** Toz emme durumunu makine durdurma mantığına bağla ve bağımsız izleme ekle.
5. [ ] **YZ Fail-Safe kurgusu:** YZ modeli için güven eşiği (confidence threshold), çapraz sensör kontrolü ve güvenli fallback tanımla.

---
*Çıktı Belgesi: Evidence Pack EP 02, EP 03, EP 04, EP 05, EP 09, EP 13, EP 15 Stratejik Değerlendirme Özeti.*

