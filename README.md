# 🕌 Bakı Namaz Vaxtları — Telegram Bot

Bakı şəhəri üçün namaz vaxtlarını bildirən, Hicri təqvim, Ramazan rejimi, oruc izləmə, rəqəmsal təsbeh, gündəlik hədis və admin paneli olan **çoxdilli** (🇦🇿 Azərbaycanca / 🇹🇷 Türkcə) Telegram botu.
**Cloudflare Workers** üzərində pulsuz işləyir — server lazım deyil.

[![Cloudflare Workers](https://img.shields.io/badge/Cloudflare-Workers-F38020?logo=cloudflare&logoColor=white)](https://workers.cloudflare.com/)
[![Telegram Bot](https://img.shields.io/badge/Telegram-Bot-26A5E4?logo=telegram&logoColor=white)](https://core.telegram.org/bots)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## ✨ Xüsusiyyətlər

### 📅 Namaz Vaxtları
- Gündəlik, sabahkı, həftəlik və aylıq namaz vaxtları
- İstənilən tarix üzrə axtarış (`/tarix 25.03.2026` və ya `/tarix 25 mart`)
- Növbəti namaza qalan vaxtın göstərilməsi (◀️ ilə işarələnir)
- 9 vaxt: İmsak, Sübh, Gün çıxır, Zöhr, Əsr, Gün batır, Məğrib, İşa, Gecə yarısı

### 🔔 Avtomatik Bildirişlər
- Hər namaza **15, 10, 5 dəqiqə** qalmış xəbərdarlıq
- Namaz vaxtı gəldikdə bildiriş
- Hər gün səhər **05:00**-da avtomatik gündəlik cədvəl
- Cloudflare KV ilə təkrar bildirişlərin qarşısının alınması (dedup)
- 🌍 **Ağıllı Saat Qurşağı İdarəetməsi:** İstifadəçinin şəhərinə görə (məs. Türkiyə UTC+3, Bakı UTC+4) bildirişlərin gecikmə və ya tez getməsinin qarşısını alan avtomatik offset sistemi
- 🚀 **Limitsiz Bildiriş Yayımı:** Cloudflare Workers-in 50 *subrequest* limitini aşmaq üçün **Batching & Self-Chaining** arxitekturası (Minlərlə istifadəçiyə kəsintisiz bildiriş)

### 🌙 Ramazan Rejimi
- Ramazan ayında avtomatik aktivləşir
- İmsak (Səhər) və İftar (Məğrib) vaxtları vurğulanır
- 🕌 Teravih namazı vaxtı əlavə göstərilir
- İftara **30, 15, 5 dəqiqə** qalmış xüsusi xatırlatma
- Gündəlik hədis / ayə mesajları (30 gün üçün)
- Qadr gecəsi xəbərdarlıqları

### 📊 Oruc İzləmə & Statistika
- İnteraktiv oruc qeydi (✅ Tutdum / ❌ Tutmadım)
- Ardıcıl oruc günləri izləmə (streak)
- Nailiyyətlər sistemi (🥇 İlk Oruc, 🔥 3 Gün, ⚡ 7 Gün, 💪 Yarısı, 🏆 Tam Ramazan, ⭐ Qadr Gecələri)
- Progress bar ilə statistika
- Motivasiya mesajları (hər gün fərqli)
- İftar sonrası avtomatik "Oruc tutdunuzmu?" sualı

### 🤲 Dua & Əlavə
- İftar, İmsak (Niyyət) və ümumi Ramazan duaları
- ⚙️ Fərdi bildiriş ayarları (hansı namazlar, hansı xatırlatmalar)

### 🕌 Qəza Namazı Hesablayıcısı
- Qılınmamış namazların qeydiyyatı (Sübh, Zöhr, Əsr, Məğrib, İşa, Vitr)
- `+` və `-` düymələri ilə asan idarəetmə
- Məlumatlar Cloudflare KV-də daimi saxlanılır

### 📅 Dini Günlər Təqvimi
- 2026-cı il üçün bütün İslam bayramları və mübarək gecələr
- Keçmiş və gələcək tarixlərin avtomatik hesablanması
- Qalan gün sayının göstərilməsi

### 📿 Əsma-ül Hüsna (99 Ad)
- Allahın 99 adı, ərəbcə yazılışı və mənası (AZ + TR)
- Təsadüfi ad öyrənmə rejimi
- Siyahı şəklində baxış (33-lük səhifələr)

### ✨ Cümə Təbrikləri
- Cümə günləri üçün xüsusi təbrik mesajları
- Hədis və dualarla zənginləşdirilmiş mətnlər
- Dostlarla paylaşmaq üçün hazır format

### ☪️ Hicri Təqvim
- Bütün namaz vaxtları mesajlarında Hicri tarix göstərilir
- `/cevir` əmri ilə istənilən tarixi Hicri təqvimə çevirin

### 📿 Rəqəmsal Təsbeh (Zikr)
- Bot daxilində interaktiv zikr sayğacı
- 6 fərqli zikr: SubhanAllah, Əlhəmdulillah, Allahu Əkbər, La iləhə illəllah, Əstağfirullah, Salavat
- Hər zikr üçün hədəf sayı və progress göstəricisi

### 📖 Günün Hədisi
- Hər gün fərqli hədis/ayə mesajı
- 60+ hədis və ayə bazası
- Təsadüfi hədis düyməsi

### 📢 Admin Sistemi & Veb Panel
- İstifadəçi izləmə (ad, username, qoşulma tarixi KV-də saxlanılır)
- `/broadcast` əmri ilə bütün istifadəçilərə toplu mesaj
- 🔒 Şifrə ilə qorunan **Admin Web Panel** (`/admin`)
- Dashboard: Ümumi istifadəçi sayı, aktiv istifadəçilər, istifadəçi cədvəli
- Veb interfeysdən toplu yayım göndərmə
- 📡 **Kanal İdarəetməsi:** Admin `/kanal_ayarlar` gizli əmri ilə kanala gedən bildirişləri (İmsak, Sübh, İftar və s.) dərhal aktiv/deaktiv edə bilər.

### 🌐 Çoxdilli Dəstək (i18n)
- 🇦🇿 **Azərbaycanca** (default) və 🇹🇷 **Türkcə** interfeys
- Bütün mesajlar, düymələr, toast bildirişləri lokalizasiya edilib
- Ramazan hədisləri, nailiyyətlər, dini günlər, Əsma-ül Hüsna — hər iki dildə
- İstifadəçi `/ayarlar` → Dil ilə dəyişdirə bilər
- Türkcə əmr alias-ları: `/namaz`, `/tarih`, `/istatistik` və s.

## 📍 Dəstəklənən Şəhərlər

- **Azərbaycan**: Bakı, Gəncə
- **Türkiyə**: Adana, Ankara, Antalya, Bursa, Diyarbakır, Erzurum, Eskişehir, Gaziantep, İstanbul, İzmir, Kayseri, Konya, Mersin, Samsun, Trabzon, Şanlıurfa, Van (və digər 81 vilayət)

Şəhəri bot daxilində `/ayarlar` düyməsi ilə dəyişə bilərsiniz. Türkiyə vilayətlərinin məlumatı **Diyanət İşləri Başqanlığının** (API) təqviminə, Azərbaycan şəhərlərinin məlumatı isə **Qafqaz Müsəlmanları İdarəsinin** təqviminə əsaslanır.

### 🖲️ İnteraktiv İnterfeys
- İnline düymələr ilə tam idarə — əmr yazmağa ehtiyac yoxdur
- Ramazan təqvimi səhifələmə (3 səhifə × 10 gün)

---

## 🤖 Bot Əmrləri

| Əmr | Təsvir |
|------|--------|
| `/start` | Bot haqqında məlumat + bugünkü vaxtlar |
| `/vaxtlar` | Bugünkü namaz vaxtları |
| `/sabah` | Sabahkı namaz vaxtları |
| `/heftelik` | 7 günlük namaz cədvəli |
| `/ay` | Cari ayın cədvəli |
| `/ay mart` | Müəyyən ayın cədvəli |
| `/tarix 25.03.2026` | Tarix üzrə namaz vaxtları |
| `/tarix 25 mart` | Tarix üzrə (cari il) |
| `/ramazan` | Ramazan təqvimi + oruc izləmə |
| `/statistika` | Oruc statistikası və nailiyyətlər |
| `/dua` | İftar / İmsak / Ramazan duaları |
| `/namazlarim` | Namazlarım (Gündəlik namaz izləmə və statistika) |
| `/quran` | Quran Menyusu və 114 surə oxunuşu |
| `/sureler` | Namazda ən çox oxunan qısa surələr |
| `/aye` | Gündəlik Quran ayəsi |
| `/dualar` | Gündəlik dualar (Müsəlmanın Qalası) |
| `/zikr` | Rəqəmsal Təsbeh (sayğac) |
| `/qeza` | Qəza namazı hesablayıcısı |
| `/teqvim` | Dini günlər təqvimi (2026) |
| `/asma` | Əsma-ül Hüsna (99 Ad) |
| `/cume` | Cümə təbrikləri |
| `/hedis` | Günün hədisi |
| `/cevir` | Bugünkü Hicri tarix |
| `/cevir 25.03.2026` | Miladi → Hicri çevirici |
| `/ayarlar` | Bildiriş ayarlarını idarə et |
| `/broadcast <mesaj>` | Admin: Bütün istifadəçilərə mesaj (yalnız admin) |
| `/help` | Bütün əmrlərin siyahısı |

> 💡 **Alias-lar (AZ/TR/EN):**
> - `/vaxtlar` → `/bugün`, `/bugun`, `/today`, `/namaz`
> - `/sabah` → `/tomorrow`, `/yarin`
> - `/heftelik` → `/həftəlik`, `/weekly`, `/heftə`, `/haftalik`
> - `/ay` → `/aylıq`, `/ayliq`, `/monthly`, `/aylik`
> - `/tarix` → `/date`, `/tarih`
> - `/ramazan` → `/ramadan`, `/oruc`, `/oruç`
> - `/statistika` → `/stats`, `/istatistik`
> - `/cevir` → `/çevir`, `/hicri`
> - `/hedis` → `/hadis`, `/hadith`
> - `/zikr` → `/tesbeh`, `/təsbeh`, `/tespih`
> - `/qeza` → `/qəza`, `/kaza`
> - `/teqvim` → `/təqvim`, `/calendar`, `/takvim`
> - `/asma` → `/esma`, `/husna`, `/99`
> - `/cume` → `/cümə`, `/friday`, `/juma`, `/cuma`
> - `/help` → `/komek`, `/kömək`, `/yardim`, `/yardım`
> - `/ayarlar` → `/settings`, `/ayarlar`

---

## 🛠️ Texnologiyalar

| Texnologiya | İstifadə |
|-------------|----------|
| [Cloudflare Workers](https://workers.cloudflare.com/) | Serverless runtime (pulsuz tier) |
| [Cloudflare KV](https://developers.cloudflare.com/kv/) | Ayarlar, oruc statusu, dedup saxlanması |
| [Cron Triggers](https://developers.cloudflare.com/workers/configuration/cron-triggers/) | Hər dəqiqə bildiriş yoxlaması |
| [Telegram Bot API](https://core.telegram.org/bots/api) | Webhook vasitəsilə əmrləri qəbul etmə |
| JavaScript (ES Modules) | Worker kodu |

---

## 🚀 Qurulum

### Tələblər
- [Node.js](https://nodejs.org/) (v18+)
- [Cloudflare hesabı](https://dash.cloudflare.com/sign-up) (pulsuz)
- Telegram bot token ([@BotFather](https://t.me/BotFather)-dən)

### 1. Layihəni klonla
```bash
git clone https://github.com/akm096/Baku-ucun-namaz-vaxti-botu.git
cd Baku-ucun-namaz-vaxti-botu
```

### 2. Asılılıqları qur
```bash
npm install
```

### 3. Cloudflare-ə giriş et
```bash
npx wrangler login
```

### 4. KV Namespace yarat
```bash
npx wrangler kv namespace create NOTIFICATIONS_KV
```
Çıxışdakı `id` dəyərini `wrangler.toml` faylındakı `id = "YOUR_KV_NAMESPACE_ID_HERE"` ilə əvəz et.

### 5. Secret-ləri təyin et
```bash
npx wrangler secret put BOT_TOKEN
# Soruşanda Telegram bot tokenini yapışdır

npx wrangler secret put ALLOWED_CHAT_ID
# Soruşanda chat/qrup ID-ni yaz (admin əmrləri üçün)

npx wrangler secret put ADMIN_PASSWORD
# Soruşanda admin panel şifrəsini yaz
```

> 💡 **Chat ID-ni tapmaq:** botu qrupa əlavə edib `/start` göndər, sonra `https://api.telegram.org/bot<TOKEN>/getUpdates` linkini açıb `chat.id` dəyərini tap.

### 6. Deploy et
```bash
npx wrangler deploy
```

### 7. Telegram Webhook-u təyin et
```bash
curl "https://api.telegram.org/bot<BOT_TOKEN>/setWebhook?url=https://baku-namaz-bot.YOUR_SUBDOMAIN.workers.dev/webhook"
```

> 📖 Ətraflı qurulum təlimatı üçün [DEPLOY.md](DEPLOY.md) faylına baxın.

---

## 📁 Layihə Strukturu

```
Baku-ucun-namaz-vaxti-botu/
├── src/
│   └── worker.js          # Əsas Cloudflare Worker kodu
│                            #   - Telegram Bot handler
│                            #   - Admin Panel (HTML/JS)
│                            #   - API endpoints
├── data/
│   ├── 2026-01.json       # Yanvar namaz vaxtları
│   ├── 2026-02.json       # Fevral namaz vaxtları
│   └── ...                # Hər ay üçün ayrı JSON (12 ay)
├── bot.js                 # ⚠️ Legacy Node.js versiya (istifadə olunmur)
├── wrangler.toml          # Cloudflare Workers konfiqurasiyası
├── package.json
├── DEPLOY.md              # Ətraflı deploy təlimatı
├── .env.example           # Nümunə environment dəyişənləri
├── .gitignore
└── LICENSE                # MIT
```

---

## 📄 Data Formatı

Namaz vaxtları `data/` qovluğundakı aylıq JSON fayllardan oxunur.

**Format:** `data/YYYY-MM.json`

```json
{
  "year": 2026,
  "month": 2,
  "city": "Bakı",
  "days": [
    {
      "day": 1,
      "imsak": "06:23",
      "subh": "06:28",
      "gunCixir": "07:50",
      "zohr": "12:54",
      "esr": "16:17",
      "gunBatir": "17:58",
      "meqrib": "18:13",
      "isha": "19:16",
      "gecaYarisi": "00:12"
    }
  ]
}
```

> ⚠️ Yeni ay əlavə edəndə `src/worker.js` faylına `import` və `BUNDLED_DATA` giriş əlavə etmək lazımdır. Ətraflı: [DEPLOY.md](DEPLOY.md)

---

## 💰 Xərclər

Bu bot tamamilə **Cloudflare-in pulsuz tier-ində** işləyir:

| Resurs | Pulsuz limit | Botun istifadəsi |
|--------|-------------|------------------|
| Worker sorğuları | 100K/gün | ~1440/gün (cron) + mesaj sayı qədər (batching) + əmrlər |
| KV oxuma | 100K/gün | İstifadədən asılı olaraq dəyişir (minimum) |
| KV yazma | 1K/gün | ~30/gün (cədvəl qurulması) + batching yazıları |
| Cron triggers | 5 ədəd | 1 ədəd |

---

## ⚠️ Legacy Versiya

`bot.js` faylı botun köhnə **Node.js + Polling** versiyasıdır. Bu versiya **artıq istifadə olunmur** — layihə Cloudflare Workers-ə köçürülüb. Fayl yalnız istinad üçün saxlanılıb.

Əsas Worker kodu: [`src/worker.js`](src/worker.js)

---

## 📝 Lisenziya

Bu layihə [MIT lisenziyası](LICENSE) altında paylaşılır.

---

## 🤝 Töhfə

Töhfə vermək istəyirsinizsə:

1. Layihəni fork edin
2. Yeni branch yaradın (`git checkout -b feature/yeni-xüsusiyyət`)
3. Dəyişikliklərinizi commit edin (`git commit -m 'Yeni xüsusiyyət əlavə edildi'`)
4. Branch-ı push edin (`git push origin feature/yeni-xüsusiyyət`)
5. Pull Request açın

---

📍 **Mənbə:** Qafqaz Müsəlmanları İdarəsi rəsmi namaz vaxtları
