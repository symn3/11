# Modular RP Preset v0.3+ — Modül Kataloğu

Otomatik üretilmiştir. Maliyetler tahmindir (karakter sayısı bölü 4). Konum: **göreli** = sistem katmanı, **D0** = sohbet içi derinlik 0 (en sona yakın), sayı = sıra.

| ID | Başlık | Varsayılan | Konum | ~Token | Gerekir | Çakışır |
|---|---|---|---|---|---|---|
| | **━━ A · ÇEKİRDEK ━━** | | | | | |
| a1-core | A1 · 🎭 Çekirdek Sözleşme | AÇIK | göreli | 380 | Yok | Yok |
| a2-priority | A2 · ⚖️ Öncelik, OOC ve Çakışma Kuralı | AÇIK | göreli | 350 | A4 | Yok |
| a3-sources | A3 · 📚 Kaynak Okuyucu | AÇIK | göreli | 470 | Yok | Yok |
| a4-bounds | A4 · 🚫 Sert Sınırlar | AÇIK | göreli | 230 | Yok | Yok |
| a5-frame | A5 · 🧱 Kaynak Çerçevesi | AÇIK | göreli | 110 | Yok | Yok |
| | **━━ B · KULLANICI ROLÜ ━━** | | | | | |
| b1-player | B1 · 🎮 Rol: Oyuncu | AÇIK | göreli | 290 | Yok | B2, B3 (seç-biri) |
| b2-director | B2 · 🎬 Rol: Yönetmen | kapalı | göreli | 200 | Yok | B1, B3; B4 anlamını yitirir |
| b3-cowriter | B3 · ✍️ Rol: Ortak Yazar | kapalı | göreli | 130 | Yok | B1, B2; B4 anlamını yitirir |
| b4-antiparrot | B4 · 🦜 Yankı: Papağan Yasağı | AÇIK | göreli | 180 | B1 | B5 (seç-biri) |
| b5-embellish | B5 · ✨ Yankı: Süsleme | kapalı | göreli | 100 | B1 veya B3 | B4 (seç-biri) |
| | **━━ C · SİMÜLASYON ━━** | | | | | |
| c1 | C1 · 🧍 NPC İnisiyatifi | AÇIK | göreli | 300 | Yok | Yok |
| c2 | C2 · 👁️ Her Şeyi Bilmeme | AÇIK | göreli | 230 | Yok | Yok |
| c3 | C3 · 🌍 Dünya, Sürtünme ve Ağırlık | AÇIK | göreli | 300 | Yok | Yok |
| c4 | C4 · 🚪 Algı Fiziği | kapalı | göreli | 150 | C2 ile birlikte iyi çalışır | Yok |
| c5 | C5 · 📏 Mekân ve Duruş | AÇIK | göreli | 120 | Yok | Yok |
| c6 | C6 · ⏳ Zaman Sürekliliği | AÇIK | göreli | 170 | Yok | Yok |
| c7 | C7 · ⏰ Zaman ve Yer Başlığı | kapalı | D0 · 30 | 160 | C6 önerilir | Yok |
| c8 | C8 · 💓 VAD ve İçgüdü | AÇIK | göreli | 260 | Yok | Yok |
| c9 | C9 · 🔒 Sır Hızı | AÇIK | göreli | 130 | Yok | Yok |
| c10 | C10 · 🆕 NPC Doğuşu ve İsimler | kapalı | göreli | 280 | Yok | Yok |
| c11 | C11 · ⚔️ Dövüş Fiziği | kapalı | göreli | 200 | C5 önerilir | Yok |
| c12 | C12 · 🎲 Rastgelelik | kapalı | D0 · 600 | 240 | Yok | C14 ile aynı anda açma (Pura: en fazla ikisi) |
| c13 | C13 · 🧬 Canlı Bedenler ve Süreklilik | kapalı | göreli | 330 | C5, C6 ile birlikte iyi çalışır | Yok |
| c14 | C14 · 🧩 Gerçekçi Komplikasyon | kapalı | D0 · 610 | 320 | Yok | C12 ile birlikte açma |
| c15 | C15 · 🧭 Sahne Sürücüsü | kapalı | D0 · 620 | 200 | Yok | Yok |
| | **━━ D · ANLATI ━━** | | | | | |
| d1-pov | D1 · 👀 Birinci Şahıs (karakter) | kapalı | göreli | 40 | Yok | D2, D3, D4 (seç-biri) |
| d2-pov | D2 · 👀 İkinci Şahıs (kullanıcı) | kapalı | göreli | 60 | Yok | D1, D3, D4 (seç-biri) |
| d3-pov | D3 · 👀 Üçüncü Şahıs | kapalı | göreli | 40 | Yok | D1, D2, D4 (seç-biri) |
| d4-pov | D4 · 👀 Hybrid POV (3. şahıs + dokunsal 2. şahıs) | AÇIK | göreli | 150 | B1 ile uyumlu istisna olarak çalışır | D1, D2, D3 (seç-biri) |
| d5-prose | D5 · 🎬 Nesir: Sinematik Gerçekçilik | AÇIK | göreli | 310 | Yok | D6, D7 (seç-biri) |
| d6-prose | D6 · 📖 Nesir: Hikâye Kipi | kapalı | göreli | 150 | Yok | D5, D7 (seç-biri) |
| d7-prose | D7 · 🪞 Nesir: Dengeli Rehber (Ayna) | kapalı | göreli | 90 | Yok | D5, D6 (seç-biri) |
| d8-voice | D8 · 🎤 NPC Sesi ve Diyalog | AÇIK | göreli | 400 | Yok | Yok |
| d9-sfx | D9 · 💥 Onomatope | kapalı | göreli | 40 | Yok | Yok |
| d10-genre | D10 · 🏷️ Tür Sözlüğü | kapalı | göreli | 140 | Yok | Yok |
| | **── D · Uzunluk (seç-biri D11-D14) ──** | | | | | |
| d11-len | D11 · 📏 Uzunluk: Kısa | kapalı | göreli | 40 | Yok | D12, D13, D14 (seç-biri) |
| d12-len | D12 · 📏 Uzunluk: Dengeli | AÇIK | göreli | 50 | Yok | D11, D13, D14 (seç-biri) |
| d13-len | D13 · 📏 Uzunluk: Uzun | kapalı | göreli | 60 | Yok | D11, D12, D14 (seç-biri) |
| d14-len | D14 · 📏 Uzunluk: Esnek | kapalı | göreli | 50 | Yok | D11, D12, D13 (seç-biri) |
| | **── D · Dil ve Biçim ──** | | | | | |
| d15-lang | D15 · 🌐 Çıktı Dili: Kullanıcıyı Eşle | AÇIK | göreli | 70 | Yok | D15b, D15c (seç-biri) |
| d15-tr | D15b · 🇹🇷 Çıktı Dili: Türkçe | kapalı | göreli | 410 | Yok | D15, D15c (seç-biri) |
| d15-en | D15c · 🇬🇧 Çıktı Dili: İngilizce | kapalı | göreli | 60 | Yok | D15, D15b (seç-biri) |
| d16-slop | D16 · 🧹 Slop Koruması (birleşik yasak listesi) | AÇIK | D0 · 800 | 650 | Yok | Yok |
| d17-voice | D17 · 🎙️ Ses Önayarı (anlatıcı sesi) | kapalı | göreli | 240 | Özel talimatta ses adı | Yok |
| d18-fmt | D18 · 🧾 Biçim: Düz Anlatı + Tırnaklı Diyalog | AÇIK | göreli | 90 | Yok | D19 (seç-biri) |
| d19-fmt | D19 · 🧾 Biçim: *Yıldızlı Aksiyon* + Tırnaklı Diyalog | kapalı | göreli | 70 | Yok | D18 (seç-biri) |
| | **━━ E · İÇERİK (+18) ━━** | | | | | |
| e1 | E1 · 🔞 Yetişkin: Standart | kapalı | göreli | 90 | Yetişkin karakterler, açık bağlam | E2, E3 (seç-biri) |
| e2 | E2 · 🔞 Yetişkin: Gerçekçilik | kapalı | göreli | 140 | Yetişkin karakterler, açık bağlam | E1, E3 (seç-biri) |
| e3 | E3 · 🔞 Yetişkin: Yoğun (Freaky) | kapalı | göreli | 140 | Yetişkin karakterler, oyuncunun açık isteği | E1, E2 (seç-biri) |
| | **━━ F · DURUM SİSTEMİ ━━** | | | | | |
| f0 | F0 · 🗂️ Dahili Durumlar (ana şablon) | kapalı | D0 · 200 | 430 | Regex: MRP Durum scriptleri + FF Menü scriptleri | Yok |
| f1 | F1 · 🗺️ NPC Gündemleri ve Konumları | kapalı | D0 · 210 | 290 | F0 | Yok |
| f2 | F2 · 🏴 Gruplar (Factions) | kapalı | D0 · 220 | 110 | F0 | Yok |
| f3 | F3 · 💞 İlişkiler (BOND / SPARKS / GRUDGE) | kapalı | D0 · 230 | 430 | F0, regex: Relationship Bars | Yok |
| f4 | F4 · 📜 Görevler | kapalı | D0 · 240 | 100 | F0 | Yok |
| f5 | F5 · 🎒 Envanter, Yetenek, Unvan | kapalı | D0 · 250 | 210 | F0; F9 ile birlikte iyi çalışır | Yok |
| f6 | F6 · 🔫 Chekhov'un Silahı | kapalı | D0 · 260 | 260 | F0 | Yok |
| f7 | F7 · 💭 NPC Düşünceleri | kapalı | D0 · 270 | 130 | F0 | Yok |
| f8 | F8 · 📓 GM Defteri | kapalı | D0 · 280 | 150 | F0 | Yok |
| f9 | F9 · 🎲 Zar Simülatörü (DnD Task Sim) | kapalı | D0 · 290 | 310 | F0; F5 ile modifier bağı | Yok |
| f10 | F10 · 🌐 Dünya Simülasyonu | kapalı | D0 · 295 | 340 | F0 | Yok |
| f11 | F11 · 🧱 Fizik ve Dünya Notları | kapalı | D0 · 298 | 110 | F0 | Yok |
| f12 | F12 · 📉 Lean Modu (Token Tasarrufu) | kapalı | D0 · 299 | 150 | F0 | Yok |
| | **━━ G · AKIL / DÜŞÜNME ━━** | | | | | |
| g0 | G0 · 🤫 Yerel Akıl (promptsuz) | AÇIK | D0 · 400 | 60 | Yok | G1-G5 (seç-biri) |
| g1 | G1 · 🫥 Sessiz Plan + Zihin Belleği (mindstate) | kapalı | D0 · 410 | 700 | Regex: MRP Plan scriptleri (gizle, mindstate koru) | G0, G2-G5 (seç-biri) |
| g2 | G2 · ⚡ Micro Kontrol | kapalı | D0 · 420 | 60 | Yok | G0, G1, G3-G5 (seç-biri) |
| g3 | G3 · ⚙️ BOLT Kontrol | kapalı | D0 · 430 | 110 | Yok | G0-G2, G4, G5 (seç-biri) |
| g4 | G4 · 🧱 MAX Kontrol | kapalı | D0 · 440 | 230 | Yok | G0-G3, G5 (seç-biri) |
| g5 | G5 · 🧠 Zorunlu Monolog (Hapuppy) | kapalı | D0 · 450 | 160 | Regex: Hapuppy gizle/sil | G0-G4, G6 (seç-biri) |
| g6 | G6 · ✂️ Reasoning'i Azalt (G0 eki) | kapalı | D0 · 460 | 80 | G0 | G1-G5 |
| | **━━ H · SUNUM / RPG ÇIKTISI ━━** | | | | | |
| h1 | H1 · 🌈 Renkli Diyalog | kapalı | D0 · 100 | 180 | Regex: Diyalog renklendirici (FF) | D19 ile yıldız stili karışabilir; ST'nin kendi diyalog renklendirme eklentisini kapat |
| h2 | H2 · 🖼️ Pop-in Grafikler | kapalı | D0 · 110 | 260 | Regex: Pop-in eski blokları temizle | Yok |
| h3 | H3 · 🎨 Görsel Prompt Yorumu | kapalı | D0 · 120 | 60 | Regex: IMG_PROMPT temizleyici | Yok |
| h4 | H4 · 📱 Sosyal Akış | kapalı | D0 · 130 | 90 | Regex: Akış katlanır | Yok |
| h5 | H5 · 🔀 CYOA Seçenekleri | kapalı | D0 · 140 | 120 | Regex: Seçenek kutusu + eski seçenekleri temizle | H7, H8 (seç-biri) |
| h6 | H6 · 📊 Stat Sayfası ve Seviye | kapalı | D0 · 150 | 180 | F5 önerilir | Yok |
| h7 | H7 · 🧭 Yön Menüsü (olay örgüsü seçenekleri) | kapalı | D0 · 160 | 200 | Regex: Yön menüsü kutusu + eski menüleri temizle | H5, H8 (seç-biri) |
| h8 | H8 · 🎯 CYOA + Skill Check (gizli d100) | kapalı | D0 · 170 | 270 | Regex: Seçenek kutusu + eski seçenekleri temizle | H5, H7 (seç-biri) |
| | **━━ I · OYUNCU YUVALARI ━━** | | | | | |
| i1 | I1 · 📝 Özel Talimat (sistem katmanı) | kapalı | göreli | 10 | Gövdeyi sen doldur | A1/A4 aşılamaz |
| i2 | I2 · 📝 Özel Talimat (son kontrol katmanı) | kapalı | D0 · 700 | 20 | Gövdeyi sen doldur | A1/A4 aşılamaz |
| | **━━ J · SON KONTROL ━━** | | | | | |
| j1 | J1 · ✅ Son Kontrol | AÇIK | D0 · 900 | 320 | Yok | Yok |
| j2 | J2 · 🐞 Debug | kapalı | D0 · 950 | 40 | Yok | Yok |

## Tarif başına tahmini kural yükü

- **Lite**: ~3950 token
- **Standart**: ~5620 token
- **Immersive**: ~8050 token
- **Director**: ~6540 token
- **Full FF**: ~10310 token
