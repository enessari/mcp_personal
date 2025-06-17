# mcp_personal

🏗️ GCP Project Yapısı ve Region Optimizasyonu
Project Naming Convention
Önerilen Project ID: mcp-personal-prod-2025
Neden bu yapı:

mcp: Proje tipi identifier
personal: Kullanım amacı
prod: Environment (production)
2025: Yıl (uniqueness için)

Region Seçimi: europe-west1 (Belçika)
Neden europe-west1:

Türkiye'ye en yakın: ~35ms latency (vs US 150ms+)
Geniş ürün yelpazesi: Tüm AI servisleri mevcut
Maliyet optimum: US'den biraz pahalı ama latency/cost dengesi en iyi
Egress maliyet: Türkiye'ye veri çıkışı daha uygun
Claude/AI API'ler: US'deki AI servislerine reasonable latency

1. Project Setup Script (setup-project.sh)
Code 
📍 İlk Dosya Kullanımı
1. Dosyayı Nereye Koyacaksınız:
bash
# Proje root dizininde oluşturun
mkdir mcp-personal-server
cd mcp-personal-server
2. Script'i Oluşturun:
bash
# Script dosyasını oluşturun
nano setup-project.sh

# Yukarıdaki kodu kopyalayıp yapıştırın
# Ctrl+X, Y, Enter ile kaydedin
3. Script'i Çalıştırılabilir Yapın:
bash
chmod +x setup-project.sh
4. Çalıştırın:
bash
./setup-project.sh
5. Prerequisites (Script çalıştırmadan önce):
A. Google Cloud CLI Kurulumu:
bash
# macOS
brew install google-cloud-sdk

# Linux
curl https://sdk.cloud.google.com | bash
exec -l $SHELL

# Windows
# https://cloud.google.com/sdk/docs/install indirin
B. Authentication:
bash
# Google Cloud'a login
gcloud auth login

# Application default credentials
gcloud auth application-default login
C. Billing Account:
https://console.cloud.google.com/billing adresine gidin
Billing account oluşturun (kredi kartı gerekli)
Not: İlk kullanıcılar $300 kredi alır
6. Script Çıktısı:
Script başarıyla çalıştıktan sonra şunları oluşturacak:

✅ GCP Project: mcp-personal-prod-2025
✅ Storage Bucket: mcp-personal-prod-2025-storage
✅ Service Account ve IAM rolleri
✅ Secret Manager secrets
✅ .env dosyası
✅ project-info.json dosyası
7. Doğrulama:
bash
# Project'in oluştuğunu kontrol edin
gcloud projects describe mcp-personal-prod-2025

# Bucket'ın oluştuğunu kontrol edin  
gsutil ls gs://mcp-personal-prod-2025-storage

# Secrets'ları kontrol edin
gcloud secrets list

