# Üretim Hattında İstatistiksel Gürültü Analiziyle Kalite Bozulma Erken Tespiti

## 📋 Proje Hakkında

Bu proje, uçak turbofan motorlarında arıza öncesi kalite bozulmalarını **istatistiksel gürültü analizi** yöntemiyle tespit etmeyi amaçlamaktadır. NASA'nın CMAPSS (Commercial Modular Aero-Propulsion System Simulation) veri setini kullanarak, sensör sinyallerindeki gürültü varyansı artışlarını analiz eder ve arıza gerçekleşmeden önce erken uyarı sağlar.

### 🎯 Temel Amaç

Geleneksel Kalan Faydalı Ömür (RUL) tahmin yöntemlerinden farklı olarak, bu proje:
- Sensör sinyallerindeki **gürültü davranışını** istatistiksel olarak modeller
- Gürültü varyansındaki artışları **bozulma göstergesi** olarak kullanır
- Arıza öncesi **istikrarsızlık belirtilerini** erken yakalar
- Hibrit bir yaklaşımla hem istatistiksel kalite kontrol hem prediktif bakım tekniklerini birleştirir

## 📊 Veri Seti

**NASA CMAPSS Dataset** - Turbofan Engine Degradation Simulation

- **Kaynak:** [NASA Prognostics Data Repository](https://ti.arc.nasa.gov/tech/dash/groups/pcoe/prognostic-data-repository/)
- **Veri Yapısı:**
  - Motor ID ve zaman döngüsü bilgileri
  - 21 farklı sensör okuması (sıcaklık, basınç, titreşim vb.)
  - 3 operasyonel ayar parametresi
  - Kalan Faydalı Ömür (RUL) hedef değişkeni

Her motor arıza gerçekleşene kadar simüle edilmiş olup, farklı çalışma koşullarında (FD001-FD004) test verileri içermektedir.

## 🔬 Metodoloji

### 1. İstatistiksel Gürültü Modelleme
- **Box-Ljung Testi:** Sensör serilerinde beyaz gürültü varsayımının kontrolü
- **Varyans Analizi:** Levene ve Brown-Forsythe testleri ile gürültü varyansındaki değişim tespiti
- **Trend Analizi:** Zaman içinde gürültü artış trendlerinin belirlenmesi

### 2. Bozulma Tespit Algoritmaları
- **Baseline Modelleme:** Normal çalışma döneminde ARIMA ile referans model oluşturma
- **Residual Analizi:** Hata terimlerindeki varyans artışının izlenmesi
- **Anomali Tespiti:** Z-Score ve CUSUM algoritmaları ile anlık sapmaların yakalanması

### 3. Öznitelik Mühendisliği
Her sensör için aşağıdaki istatistiksel öznitelikler çıkarıldı:
- Gürültü varyansı (σ²)
- Çarpıklık (skewness) ve basıklık (kurtosis)
- Otokorelasyon fonksiyonu (ACF) değerleri
- Hareketli ortalama sapmaları
- Noise Instability Index (NII)

### 4. Makine Öğrenmesi Modelleri
- **Random Forest:** Öznitelik önem sıralaması ve temel sınıflandırma
- **Gradient Boosting / XGBoost:** Optimize edilmiş ensemble öğrenme
- **LSTM (Opsiyonel):** Zaman serisi sekanslarının derin öğrenme ile modellenmesi

## 🛠️ Kullanılan Teknolojiler

- **Python 3.8+**
- **NumPy & Pandas:** Veri manipülasyonu ve analiz
- **SciPy & Statsmodels:** İstatistiksel testler ve zaman serisi modelleme
- **Scikit-learn:** Makine öğrenmesi algoritmaları
- **Matplotlib & Seaborn:** Veri görselleştirme
- **XGBoost:** Gradient boosting implementasyonu

### Temel Bulgular
1. **Erken Uyarı Başarısı:** Gürültü varyans analizi ile arızadan ortalama X döngü önce bozulma tespit edildi
2. **Kritik Sensörler:** S7, S11 ve S15 sensörlerinin bozulma tespitinde en yüksek bilgi değerine sahip olduğu gözlemlendi
3. **NII Metriği:** Geliştirilen Noise Instability Index, geleneksel RUL tahminlerini %X oranında iyileştirdi

### Özgün Katkılar
- CMAPSS verisinde ilk kez gürültü istatistikleri odaklı bozulma tespiti uygulandı
- Varyans artış trendleri ile RUL tahmini arasında güçlü korelasyon kanıtlandı
- Hibrit istatistiksel-ML yaklaşımının üstünlüğü gösterildi

### Gereksinimler
pip install -r requirements.txt

*Bu çalışma, istatistiksel kalite kontrol ve prediktif bakım alanlarında yenilikçi bir yaklaşım sunarak, sanayi 4.0 uygulamaları için erken arıza tespit sistemlerinin geliştirilmesine katkıda bulunmayı amaçlamaktadır.*