# 🌲 Yazılım Mühendisliğinde Güncel Konular
## Safety 4.0: Siber-Fiziksel Sistemler, Fonksiyonel Emniyet & Endüstriyel Siber Güvenlik

![Safety 4.0](https://img.shields.io/badge/Safety_4.0-Bootcamp-0052cc?style=for-the-badge&logo=shield)
![Standard](https://img.shields.io/badge/IEC_62443-Security_Level_3%2F4-brightgreen?style=for-the-badge)
![Functional Safety](https://img.shields.io/badge/ISO_13849--1-PL_e_%7C_SIL_3-red?style=for-the-badge)
![Machine](https://img.shields.io/badge/Machine-Mirka_WoodSander_5000-orange?style=for-the-badge)

Bu depo, **Yazılım Mühendisliğinde Güncel Konular** dersi kapsamında hazırlanan; endüstriyel ahşap işleme sektörünün lideri **Mirka (Oy Mirka Ab)** firmasının **Mirka Smart WoodSander 5000** model endüstriyel ahşap kalibre ve zımpara makinesine ait fonksiyonel emniyet (Functional Safety) ve endüstriyel siber güvenlik (OT/IACS Cybersecurity) mühendisliği analizlerini içermektedir.

---

## 🏭 Makine Tanıtımı: Mirka Smart WoodSander 5000

| Parametre | Açıklama |
| :--- | :--- |
| **Üretici / Marka** | **Mirka (Oy Mirka Ab)** — Yüzey işleme ve zımpara teknolojilerinde küresel inovasyon lideri |
| **Model** | **Mirka Smart WoodSander 5000 (Sürüm 4.0)** |
| **Makine Tipi** | Endüstriyel Otomatik Ahşap Kalibre & Orbital / Geniş Bant Zımpara İstasyonu |
| **İşlem Kapasitesi** | Masif ahşap, MDF ve mobilya panelleri için 0.1 mm mikron toleranslı yüzey finisajı |
| **Mekanik Tahrik** | 4.000 – 10.000 RPM fırçasız robotik zımpara kafaları (Mirka AIROS entegre modülleri) |
| **Besleme & Pnömatik**| Yüksek torklu konveyör bant ve 6–8 bar pnömatik kalibre baskı merdaneleri |
| **Toz Tahliye / ATEX** | Yüksek debili antistatik emiş kanalı ve diferansiyel basınç sensörleri (**ATEX Zone 22**) |
| **Otomasyon Altyapısı**| Çift çekirdekli Safety PLC (SIL 3 / PL e) + Proses PLC'si + 10" Dokunmatik HMI |
| **Dijital / IoT** | Mirka Telematics Gateway (4G/LTE bulut telemetri, kestirimci zımpara aşınma analizi) |

### ⚠️ Kritik Tehlike ve Risk Profili
1. **Yüksek Hızlı Sürtünme ve Uzuv Kaybı:** 10.000 RPM dönen zımparalar, operatör temasında saniyeler içinde ölümcül uzuv parçalanmasına yol açar.
2. **Besleme Merdane Sıkışması:** Güçlü pnömatik merdaneler arasına el kaptırılması durumunda kemik kırılması ve uzuv kopması.
3. **ATEX Yanıcı Ahşap Tozu Patlaması:** İnce ahşap tozunun sürtünme kıvılcımı ile reaksiyona girerek patlama üretmesi riski.
4. **Siber-Fiziksel Sabotaj:** İnternete açık IoT uzak bakım kanalından girilerek emniyet duruş rampalarının ve sensör susturma (muting) parametrelerinin uzaktan manipüle edilmesi riski.

---

## 📂 Laboratuvar Çalışmaları ve Haftalık Föyler

Bu depoda 4 haftalık yoğun analiz ve mühendislik föyleri yer almaktadır:

| Hafta | Laboratuvar Adı | Temel Konu ve Mühendislik Odağı | Çıktı Belgesi |
| :---: | :--- | :--- | :--- |
| **1. Hafta** | [**1. Hafta - Safety Architecture**](1.%20Hafta%20-%20Safety%20Architecture.md) | Normal Kontrol ve Emniyet (Safety) yollarının mimari ayrımı, Normal PLC vs Safety PLC farkı, PLr = e / SIL 3 gereksinimleri, Safe State tanımı ve siber müdahale giriş noktaları. | **Evidence Pack EP 03:**<br/>Safety Function Map |
| **2. Hafta** | [**2. Hafta - IEC 62443 Mini Workshop**](2.%20Hafta%20-%20IEC%2062443%20Mini%20Workshop.md) | Varlık envanteri sınıflandırması, Zone & Conduit diyagramı, Industrial DMZ (iDMZ) kurgusu, Jump Server, MFA ve Just-In-Time uzak erişim karar matrisi. | **Evidence Pack EP 05:**<br/>Zone / Conduit Diagram |
| **3. Hafta** | [**3. Hafta - Threat and Risk Matrix**](3.%20Hafta%20-%20Threat%20and%20Risk%20Matrix.md) | 5 bileşenli tehdit modelleme ($Kim \to Kapı \to Eylem \to Zincir \to Fiziksel\ Sonuç$), $L \times S \times E$ formülüyle Risk Register puanlaması ve hayati $S=3$ kuralı. | **Evidence Pack EP 04:**<br/>Risk Register |
| **4. Hafta** | [**4. Hafta - Secure Remote Access**](4.%20Hafta%20-%20Secure%20Remote%20Access.md) | Mevcut zafiyetli mimariden 5 temel ilkeyle hedef güvenli mimariye geçiş; saldırgan sisteme sızsa dahi insan hayatını koruyan Fonksiyonel Emniyet Bağımsızlığı (SRS-042). | **Evidence Pack EP 02 + 06:**<br/>Secure Architecture |

---

## 🏛️ Mimari Özet: Güvenli Savunma ve Fonksiyonel Bağımsızlık

Mirka WoodSander 5000 sistemi iki temel eksende korunmaktadır:

```
[İNTERNET / BULUT]
        │
   (Conduit C1: TLS 1.3 / IPsec VPN)
        ▼
┌────────────────────────────────────────────────────────┐
│  Zone 1: Endüstriyel DMZ (iDMZ)                        │
│  - Mirka IoT Gateway                                   │
│  - Jump Server (Bastion Host + Video & Oturum Kaydı)   │
│  - Donanımsal Fiziksel Bakım Anahtarı (Varsayılan Kpl) │
└───────────────────────┬────────────────────────────────┘
                        │
                  (Conduit C3: OT Firewall / OPC UA DPI)
                        ▼
┌────────────────────────────────────────────────────────┐
│  Zone 3: Makine Operasyonel Kontrol                    │
│  - Normal PLC (Üretim & Konveyör Hızı)                 │
│  - VFD Motor Sürücüleri                                │
└───────────────────────┬────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        │  (Bağımsız Donanımsal Hat)    │
        ▼                               ▼
┌───────────────────────────┐   ┌──────────────────────────┐
│  Zone 4: Emniyet Adası    │   │  Mekanik Emniyet (STO)   │
│  - Safety PLC (PL e/SIL3) │──▶│  - Donanımsal Safe-Torque│
│  - Işık Perdesi (OSSD)    │   │  - Disk Fren Kitleme     │
│  - ATEX Emiş Emniyet Kilit│   │  - Pnömatik Tahliye      │
└───────────────────────────┘   └──────────────────────────┘
```

---

## 📜 İlgili Standartlar ve Yasal Mevzuat

* **ISO 13849-1:** Makine Güvenliği — Kumanda Sistemlerinin Güvenlikle İlgili Kısımları (Performance Level PL e, Kategori 4).
* **IEC 62061 / IEC 61508:** Fonksiyonel Güvenlik ve Emniyet Bütünlük Seviyesi (SIL 3).
* **IEC 62443:** Endüstriyel İletişim Ağları — IACS Siber Güvenlik Standardı (Bölüm 3-2: Bölge ve Kanal Modellemesi).
* **AB Makine Regülasyonu (EU Machinery Regulation 2023/1230):** Siber güvenlik zafiyetlerinin makine güvenliğini bozmasını engelleyen zorunlu emniyet direktifi.
* **CRA (Cyber Resilience Act):** Dijital unsurlar içeren ürünlerde SBOM, yama yönetimi ve 24s/72s olay bildirim yükümlülüğü.
* **ATEX 2014/34/EU & EN 12779:** Ağaç işleme makinelerinde yanıcı talaş ve toz tahliye emniyeti.

---

## 👤 Hazırlayan & İletişim
* **Öğrenci / Araştırmacı:** merenaydin23
* **Ders:** Yazılım Mühendisliğinde Güncel Konular
* **Proje Konusu:** Mirka Endüstriyel Ahşap Zımpara Makinesi Safety 4.0 Mühendislik Paketi
