# Modular RP Preset — Blueprint v0.1 (Taslak)

Hazırlayan: Claude · Kaynak: github.com/symn3/11 · Durum: **taslak, onayına açık**

## 1. Karar Özeti

| Konu | Karar |
| --- | --- |
| Teslim | **Tek preset JSON**, tüm modüller aç/kapa |
| Kullanıcı rolü | Player / Director / Co-Writer hepsi **seçilebilir modül** (aynı anda biri) |
| Kaynak katmanlar | FF 5.4 Hapuppy Forced Reasoning, FF 5.4 Internal States, FF 5.2 Internal States (BOLT), Geechan v5.2 modülleri |
| Kural | Hiçbir domain'i iki modül birden yönetmez (**duplicate yok**) |
| Stil | FF'nin görsel/etkileşimli zenginliği korunur; Pura ve LFM'de daha iyi yapılandırılmış parçalar serbestçe alınır ve geliştirilir |
| Dil kuralı | Yönlendirme yapan modüller: **adı + açıklaması Türkçe / içeriği İngilizce**. Yönlendirme yapmayan modüller (ayraç, README, bilgi notu): **Türkçe başlık içerik** |

## 2. İsimlendirme Standardı

**Fonksiyonel modül:** `A1 · Core Contract` biçiminde. Harf = grup, rakam = sıra. Açıklaması prompt'un en üstünde `{{// ... }}{{trim}}` yorumu olarak İngilizce yazılır (modele gitmez, sadece yazara/kullanıcıya görünür). Yorum şu alanları taşır: `Purpose`, `Needs`, `Conflicts`, `Cost (tokens)`, `Best for`.

**Etkisiz modül (ayraç/bilgi):** `━━ 📖 BENİ OKU ━━` gibi Türkçe başlık, içerik boş ya da yalnızca `{{// }}` yorum. `enabled: false` kalır.

**Önemli teknik not:** FF Regex Suite panel başlıklarını İngilizce etiketlerle yakalıyor (`INTERNAL STATES`, `QUESTS`, `BONDS` vb.). Bu yüzden **state çıktısındaki etiketler İngilizce kalmalı**. Türkçe yalnızca prompt manager başlıklarında kullanılır, modelin ürettiği panel etiketlerinde kullanılmaz.

## 3. Katmanlı Mimari

| Katman | Görev |
| --- | --- |
| A · Core | Değişmez sözleşme: rol, canon, nedensellik, bilgi sınırı, OOC, hard boundary |
| B · User Role | Kullanıcının hikâyedeki yetkisi (exclusive) |
| C · Simulation | NPC, dünya, fizik, zaman, rastgelelik |
| D · Narrative Style | POV, düzyazı, diyalog, uzunluk, dil, slop koruması |
| E · Content Mode | Yetişkin içerik seviyesi (exclusive, varsayılan kapalı) |
| F · State System | Gizli GM durumu (FF 5.4 çekirdek) |
| G · Reasoning | Düşünme protokolü (exclusive) |
| H · Presentation | FF'nin görsel paketi, CYOA, stat sheet |
| I · Player Slots | Kullanıcının kendi talimatları (Geechan değişkenleri) |
| J · Post-History | En sonda çalışan kalite kapısı |
| R · Regex | Ayrı JSON, FF Regex 3.0 tabanlı, genişletilmiş |

## 4. Modül Kataloğu

Kaynak kısaltmaları: **G** Geechan, **F54** FF 5.4 Internal States, **F52** FF 5.2 BOLT, **HP** Hapuppy, **P** Pura, **L** LFM, **N** yeni yazılacak.

### A · Core (her zaman açık)

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| A1 | Core Contract | Role of narrator/GM, canon priority, causality, knowledge limits, output ownership. Stated once; no other module redefines it. | N (L, P, G'den esinli) |
| A2 | Priority & OOC Handling | Priority order between modules and how OOC notes pause the story. | F54 + L |
| A3 | Source Reader | How to read card, persona, scenario and world info. | L |
| A4 | Hard Boundaries | Non-negotiable limits that outrank every module; all sexual content involves adults only. | L + N |

### B · User Role (exclusive: birini seç)

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| B1 | Role: Player | User writes only their own character; model never writes user's actions, speech or thoughts. | G (Correct Perspective) |
| B2 | Role: Director | User gives scene direction and canon; model plays all characters and world within it. | P |
| B3 | Role: Co-Writer | Model may extend or continue the user's character when invited or when OOC allows. | L + G (impersonation) |
| B4 | Echo Policy: Anti-Parrot | Characters never repeat or rephrase the user's last lines. | F52/F54 + G |
| B5 | Echo Policy: Embellish | Model enriches the user's input with sensory detail without changing intent (experimental). | F52 |

B4 ve B5 ayrı bir exclusive grup. B2/B3 seçiliyken B4 otomatik anlam kaybeder, açıklamada belirtilir.

### C · Simulation

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| C1 | NPC Agency | NPCs act on their own wants, fears and flaws, even against the player's goals. | G + F |
| C2 | Anti-Omniscience | NPCs only know what they perceived or were told. | F54 |
| C3 | World Verisimilitude | The world follows its own rules and applies consequences to player choices. | G |
| C4 | Perception Physics | Forward field of view, sound range, wall and door occlusion. | F54 |
| C5 | Spatial Awareness | Positions, distances and proxemics stay consistent. | G |
| C6 | Temporal Continuity | Elapsed time is accounted for; skips only at player request. | G |
| C7 | Time & Place Header | Header with time, date, location and weather at the top of each reply. | F52/F54 |
| C8 | NPC Instincts + VAD Emotions | Emotion shaped by valence, arousal and dominance plus basic instincts. | F |
| C9 | Revelation Pacing | Secrets stay hidden until the player discovers them. | G + L |
| C10 | NPC Genesis (HQ) | Procedure for creating new NPCs with depth and fitting names. | F + P (naming) |
| C11 | Spectacle Combat Physics | Combat described with weight, momentum and consequence. | F |
| C12 | Add Randomness | Temporary toggle that forces an unexpected development. | G (random listesi genişletilir) |

### D · Narrative Style

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| D1 | POV: First / D2 Second / D3 Third / D4 Hybrid | Exclusive group, one narrative point of view with tense and address rules. | F |
| D5 | Prose: Cinematic Realism | Concrete, observable, sensory prose; dialogue exempt. | F |
| D6 | Prose: Story Mode | Literary, emotional, syntactically varied prose. | F |
| D7 | Prose: Balanced Guide | Mirror existing tone, tense and format; free indirect speech. | G (Style Guide) |
| D8 | NPC Voice + Dialogue Output | Dialogue ratio, idiolect, flow and emotional delivery. | F |
| D9 | Onomatopoeia Mode | Sound-effect-rich writing, off by default. | F |
| D10 | Genre Tags | Genre lexicon and pacing presets. | P |
| D11 | Length: Short / D12 Balanced / D13 Long / D14 Flexible | Exclusive group for reply size. | L + F |
| D15 | Output Language | Exclusive: Match User / Turkish / English. Turkish version covers sen/siz choice and native syntax. | L (lang-tr) + N |
| D16 | Slop Guard | One merged ban list: banned phrases, tics, scents, constructions, plus replacement rules. | G (Prose Rules + Ban Phrases) ∪ F (Banned Words) ∪ P (Grounded Prose) |
| D17 | Prose Voice Presets | Optional named voices to bias style. | L |

### E · Content Mode (exclusive, varsayılan: hiçbiri)

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| E1 | Mature: Standard | Adult themes without sanitizing, moralizing or hedging. | G (NSFW) |
| E2 | Mature: Realism | Grounded, emotionally realistic adult scenes. | F (Realism Mode) |
| E3 | Mature: Freaky | Maximum intensity adult mode. | F (Freaky Mode) |

Dört ayrı NSFW prompt'u (Geechan NSFW, Simplified NSFW, FF Realism, FF Freaky) tek gruba indirilir. Her biri A4 sınırlarının altında çalışır.

### F · State System (FF 5.4 çekirdek, 5.2'den eksikler eklenir)

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| F0 | Internal States Master | Appends the hidden GM state block wrapped in GFX tags; all sections present, empty ones marked None. | F54 |
| F1 | NPC Agendas & Locations | Off-screen NPC goals, progress and positions. | F54 |
| F2 | Factions | Faction goals, morale, conflict and relations. | F54 |
| F3 | Relationships RPG | Bond, Sparks and Grudge between characters. | F52/F54 |
| F4 | Quests | Main and side quest tracking. | F |
| F5 | Inventory, Feats, Titles | Items, skills, titles and modifiers. | F52 |
| F6 | Chekhov's Gun | Planted details and payoff tracking. | F |
| F7 | NPC Internal Thoughts | Short hidden thoughts of selected NPCs. | F |
| F8 | GM Notebook | Short and medium-term memory notes. | F |
| F9 | DnD Simulator | DC, roll and outcome for risky actions. | F52 |
| F10 | World Sim | Off-screen random events. | F |
| F11 | Physics & World Footer | Hazards, spatial and world facts. | F54 |
| F12 | State Budget Mode | Full snapshot every N turns, deltas in between. | **N (yeni)** |

### G · Reasoning (exclusive: birini seç ya da hiçbiri)

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| G0 | Native Reasoning (no prompt) | Leave reasoning to the model's own channel. | N |
| G1 | Silent Plan | Short hidden plan with persistent mindstate, stripped by regex. | L (DeepPlan) |
| G2 | Micro CoT | Smallest checklist, fastest. | F |
| G3 | BOLT CoT | Medium checklist balancing speed and rules. | F52 |
| G4 | MAX CoT | Nested gates, slowest and strictest. | F |
| G5 | Forced Reasoning (Hapuppy) | Visible Internal Monologue then Response; only for endpoints without native reasoning. | HP |
| G6 | Reduce Reasoning (add-on) | Caps drafting on native-reasoning models; incompatible with G5. | G |

### H · Presentation

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| H1 | Colored Dialogue VN | Tagged speech rendered with colors and delivery styles (tremble, measured, whisper, shout). | F |
| H2 | Pop-in Graphics | In-world documents, maps and displays as HTML. | F |
| H3 | Image Prompt Block | Hidden image prompt comment for image generation. | F |
| H4 | Social Feed | In-world social media feed artifact. | F |
| H5 | CYOA Choices + Skill Checks | Choices with skill-check resolution. | P/L |
| H6 | Persona Stat Generator | Builds and levels a stat sheet from the persona. | P |

### I · Player Slots ve J · Post-History

| ID | Module | Description | Kaynak |
| --- | --- | --- | --- |
| I1 | Custom Instructions | Variables `player-instructions` and `player-posthistory`, placed with priority. | G |
| J1 | Post-History Check | Final silent self-check: echo, perspective, knowledge limits, slop, format. | G (Prose Rules) + L (Final Silent Check) |
| J2 | Debug Engine | Optional diagnostics for testing. | F |

## 5. Duplicate Önleme Matrisi

Her domain'in tek sahibi var, diğerleri bilinçli olarak düşürülür.

| Domain | Tek sahip | Düşürülen kopyalar |
| --- | --- | --- |
| Rol ve temel sözleşme | A1 | FF Main kuralları, G Role Preamble, L/P main girişleri |
| Kullanıcıyı yazmama | B1 | G Correct Perspective, FF user-autonomy, L Player Sovereignty |
| Anti-echo | B4 | G anti-echo satırları, FF anti-parrot, J1 içindeki tekrarlar |
| NPC bilgi sınırı | C2 | G epistemic limits, FF anti-omniscient, L knowledge rules |
| Zaman | C6 + C7 | G Temporal, FF Time header (ikisi ayrı iş: kural vs çıktı) |
| Yasaklı ifadeler | D16 | G Ban Phrases, G Prose Rules listesi, FF Banned Words, P Grounded Prose |
| Uzunluk | D11–D14 | FF Total Output Length, L length modes, P length |
| NSFW | E1–E3 | G NSFW + Simplified NSFW, FF Realism, FF Freaky |
| Reasoning | G0–G5 | FF 5.2 CoT seçici, FF 5.4 Forced Reasoning, L DeepPlan (hepsi tek grup) |
| State şeması | F0 | 5.2 ve 5.4 şablonları tek şemada birleşir |
| Son kontrol | J1 | G Prose Rules + L Final Silent Check birleşik |

## 6. Exclusive Gruplar ve Bağımlılıklar

**Exclusive (birini seç):** B1/B2/B3 · B4/B5 · D1–D4 · D5/D6/D7 · D11–D14 · D15 · E1/E2/E3 · G0–G5.

**Bağımlılıklar:**

| Modül | Gerektirir |
| --- | --- |
| F0 ve F1–F11 | Regex: Context Saver, GFX repair, menu scripts. F0 kapalıysa F1–F11 çalışmaz |
| F3 | Relationship Bars regex'leri |
| H1 | Dialogue Colorizer regex'leri |
| G5 | Hapuppy Hide/Delete regex + visible monologue başlıkları |
| G1 | Silent Plan regex (`<plan>` gizleme, eski planları promptan silme) |
| G6 | G0 ile birlikte; G5 ile çakışır |
| B4 | B1 ile birlikte anlamlı |

**Uyarı:** ST'de "Pick one" yalnızca rehberdir, kilit değildir. Bu yüzden A2 içine bir **tie-break kuralı** (çakışmada hangi modül kazanır) yazılacak ve README'de profil tarifleri verilecek.

## 7. Prompt Sırası

1. README ve bilgi ayraçları (kapalı, Türkçe)
2. A1–A4 Core
3. B Role
4. C Simulation
5. D Style, E Content
6. World Info (before), Char Description, Personality, Scenario, Persona
7. F State şablonları ve F0
8. G Reasoning
9. World Info (after), Chat Examples
10. Chat History
11. I1 Custom Instructions, D16 Slop Guard, J1 Post-History Check, C12 Randomness (derinlik 0)

## 8. Regex Paketi (R)

FF Regex 3.0'ın **25 script'i** olduğu gibi taşınır: untagged thought temizleme/yakalama, GFX ve summary onarımı, 4 diyalog stili + universal colorizer, Hapuppy hide/delete, menü renkleri (Master, Purple, Teal, Orange), highlights, relationship bars (pozitif/negatif), GFX ve image-prompt stripper, Context Saver.

**Eklenecekler:**

- Silent Plan için `<plan>` gizleme ve eski planı promptan silme (G1)
- State Budget Mode için delta bloğu birleştirme (F12)
- Menü script'lerinde etiket listesini tek bir değişken kaynağından türetme (bakım kolaylığı)

Kural: her script için `placement`, `markdownOnly`, `promptOnly` ve çalışma sırası belgelenir. Silme ve gizleme script'leri aynı anda açık bırakılmaz.

## 9. Hazır Tarifler (README içinde, Türkçe)

Tek preset olduğu için profiller export değil, **toggle tarifidir**.

| Tarif | Açık olanlar |
| --- | --- |
| Lite | A1–A4, B1, C1, C2, D4, D5, D12, D16, J1, G0 |
| Standard | Lite + C3, C5, C6, C7, C8, D8, B4 |
| Immersive | Standard + F0, F1, F3, F8, F11, F12, H1, G3 |
| Director | A1–A4, B2, C1–C8, D3, D5, D13, F0, F1, F8, G1 |
| Full FF | Immersive + F2, F4–F7, F9, F10, H2–H4, G4 |

## 10. Geliştirme Önerileri (kaynaklardan öteye)

1. **Tek kaynaklı yasak listesi (D16):** dört ayrı listeyi tek yerde birleştirip kategorilere (kalıplar, tikler, kokular, isimler) ayırmak.
2. **State Budget Mode (F12):** her turda tüm state dökümü yerine N turda bir tam snapshot, aralarda delta. Token tasarrufu sağlar.
3. **Başlık/etiket ayrımı:** Türkçe yönetim arayüzü, İngilizce model etiketleri. Regex kırılmaz.
4. **Modül başlık yorumu standardı:** Purpose, Needs, Conflicts, Cost, Best for.
5. **Core'da tie-break:** exclusive grup ihlalinde modelin hangi kuralı izleyeceği tek yerde yazılı.
6. **Çıktı dili kontratı (D15):** Türkçe modunda yapısal etiketler (Narrator, panel başlıkları, tag'ler) bozulmaz.
7. **Hata modu envanteri:** README'ye "model modülü yok sayıyor / state görünür çıkıyor / uzunluk değişti" için kısa sorun giderme tablosu.

## 11. Açık Sorular

1. **Preset adı** ne olsun?
2. **E grubunun (yetişkin içerik) üç seviyesi** de kalsın mı, yoksa ikiye mi indirelim?
3. **Hedef model(ler)** hangisi? G5 (Hapuppy) ve G6 varsayılanları buna göre ayarlanır.
4. **Varsayılan çıktı dili:** Match User mı, Turkish mı?
5. **5.2 ve 5.4 state birleştirme:** önerim 5.4 şemasını çekirdek alıp 5.2'ye özgü modülleri (DnD, Inventory vb.) eklemek. Farkı JSON'lardan çıkarıp doğrulayacağım. Uygun mu?
6. **Bu blueprint'i** reponuzdaki boş `blueprint` dosyasına commit edeyim mi?

## 12. Doğrulanmamış Noktalar

- Pura, LFM ve FF JSON'larının gövdelerini bu aşamada ayrıntılı okumadım. Not dosyalarındaki arşivlere ve yapı haritasına dayandım. Modül metinlerini yazarken kaynak JSON'lardan tek tek çıkaracağım.
- 5.2 ve 5.4 state şablonlarının satır satır farkı henüz çıkarılmadı.
- Token maliyetleri ölçülmedi, tahmindir.

## 13. Sonraki Adımlar

1. Bu taslağı onayla veya düzelt
2. Core (A1–A4) ve Role (B) metinlerini yaz
3. State şemasını (F0–F12) 5.2/5.4 farkı üzerinden çıkar
4. Regex paketini genişlet
5. JSON'u derle ve Prompt Itemization ile test et
