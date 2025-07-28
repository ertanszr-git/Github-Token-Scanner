# GitHub Token/Bilgi Sızıntı Tarayıcı

Bu proje GitHub commit'lerinde veya public repolarda açıkta kalan API token'ları, şifreler veya gizli dosyaları bulmak için geliştirilmiştir.

## Özellikler

- 🔍 **Çoklu Token Desteği**: AWS anahtarları, Slack token'ları, API anahtarları, veritabanı şifreleri
- 🎯 **Regex Tabanlı Tarama**: Güçlü regex pattern'ler ile hassas bilgi tespiti  
- 🚀 **GitHub API Entegrasyonu**: PyGithub ile otomatik repo tarama
- 📊 **Detaylı Raporlama**: JSON ve konsol çıktısı ile sonuç raporlama
- 🎨 **Renkli Terminal Çıktısı**: Kolay takip için renklendirilmiş sonuçlar

## Kurulum

1. Repository'yi klonlayın:
```bash
git clone <repo-url>
cd github-leak
```

2. Sanal ortam oluşturun ve aktifleştirin:
```bash
python3 -m venv venv
source venv/bin/activate  # Linux/Mac
# veya
venv\Scripts\activate  # Windows
```

3. Gerekli paketleri yükleyin:
```bash
pip install -r requirements.txt
```

4. Çevre değişkenlerini ayarlayın (opsiyonel):
```bash
cp .env.example .env
# .env dosyasını düzenleyerek GitHub token'ınızı ekleyin
# Not: Token olmadan da çalışır, ancak API limitleri uygulanır
```

## Hızlı Test

Demo'yu çalıştırarak araçun çalıştığını doğrulayın:
```bash
python demo.py
```

Manuel testler:
```bash
python test_scanner.py manual
```

## Kullanım

### Temel Kullanım

```bash
# Belirli bir kullanıcının repolarını tarayın
python scanner.py --user octocat

# Belirli bir repo'yu tarayın
python scanner.py --repo octocat/Hello-World

# Belirli dosya türlerini tarayın
python scanner.py --user octocat --file-types .env,.json,.yaml

# Sonuçları dosyaya kaydedin
python scanner.py --user octocat --output results.json
```

### Gelişmiş Kullanım

```bash
# Sadece belirli pattern'leri ara
python scanner.py --user octocat --patterns aws,slack

# Derinlemesine tarama (commit geçmişi dahil)
python scanner.py --user octocat --deep-scan

# Maksimum repo sayısını sınırla
python scanner.py --user octocat --max-repos 50
```

## Tespit Edilen Pattern'ler

- **AWS Anahtarları**: Access Key, Secret Key
- **Slack Token'ları**: Bot tokens, User tokens
- **API Anahtarları**: Generic API keys
- **Veritabanı Bilgileri**: DB passwords, connection strings
- **SSH Anahtarları**: Private keys
- **JWT Token'ları**: JSON Web Tokens
- **Google API**: Service account keys
- **Ve daha fazlası...**

## Proje Yapısı

```
github-leak/
├── scanner.py              # Ana tarayıcı modülü
├── patterns.py             # Gelişmiş pattern tanımları
├── security_advisor.py     # Güvenlik önerileri
├── demo.py                 # Demo ve örnekler
├── test_scanner.py         # Test dosyası
├── requirements.txt        # Python bağımlılıkları
├── .env.example           # Örnek environment dosyası
├── README.md              # Proje dokümantasyonu
├── .github/
│   └── copilot-instructions.md
└── .vscode/
    └── tasks.json         # VS Code görevleri
```

## Test Etme

```bash
# Unit testleri çalıştır
python -m unittest test_scanner.py

# Manuel testleri çalıştır
python test_scanner.py manual

# Demo'yu çalıştır
python demo.py

# Pattern'leri test et
python patterns.py

# Güvenlik önerilerini gör
python security_advisor.py
```

## Güvenlik Uyarısı

⚠️ **Önemli**: Bu araç sadece etik hacking ve güvenlik araştırmaları için tasarlanmıştır. 
- Sadece kendi repolarınızı veya izniniz olan repoları tarayın
- Bulunan hassas bilgileri kötüye kullanmayın
- Sorumlu açıklama (responsible disclosure) prensiplerine uyun
- Araç eğitim amaçlıdır, ticari kullanım için uygun olmayabilir

## Katkıda Bulunma

1. Fork edin
2. Feature branch oluşturun (`git checkout -b feature/yeni-pattern`)
3. Değişikliklerinizi commit edin (`git commit -am 'Yeni AWS pattern eklendi'`)
4. Branch'inizi push edin (`git push origin feature/yeni-pattern`)
5. Pull Request oluşturun

## Lisans

Bu proje MIT lisansı altında lisanslanmıştır.
