# Skill: YouTube Video Scraper & Summarizer

## Deskripsi
Skill untuk scrape video YouTube dan bikin summary dari konten video tersebut.

## Kemampuan
- Ambil metadata video (judul, channel, durasi, views, tanggal upload)
- Ambil deskripsi video
- Ambil transcript/subtitle video
- Generate summary dalam bahasa Indonesia (atau sesuai request)
- Generate key points / highlights
- Suggest title dan hashtag

## Cara Pakai

### 1. Scrape Video Tunggal
Ketika user kasih link YouTube, langsung bisa diproses.

**Input yang didukung:**
- Full URL: `https://www.youtube.com/watch?v=VIDEO_ID`
- Short URL: `https://youtu.be/VIDEO_ID`
- Video ID saja: `VIDEO_ID`

**Contoh prompt:**
> "Summary video ini: https://www.youtube.com/watch?v=..."

### 2. Scrape Playlist
**Contoh prompt:**
> "Summary semua video di playlist ini: https://www.youtube.com/playlist?list=..."

## Tools yang Dipakai
1. **browser_use** - Untuk akses YouTube dan ambil transcript
2. **grep_search** - Cari info tambahan
3. **write_file** - Simpan hasil summary ke file (opsional)

## Step-by-Step Process

### Step 1: Buka Video dengan Browser
```
browser_use action=open url={YOUTUBE_URL}
```

### Step 2: Scroll ke bagian deskripsi
Ambil metadata dan deskripsi dari page.

### Step 3: Cek Transcript
- Coba klik "Show transcript" atau akses langsung via:
  - `https://youtubetranscript.com/?v={VIDEO_ID}`
  - Atau pake YouTube Transcript API

### Step 4: Generate Summary
Kirim transcript + metadata ke LLM untuk dibuatkan:
- Summary ringkas (3-5 kalimat)
- Key points (bullets)
- Timestamp highlights (kalau ada)

### Step 5: Formatting Output
Kasih output dalam format:
```
📺 {Judul Video}
👤 {Nama Channel}
📅 {Tanggal Upload} | 👁️ {Views} | ⏱️ {Durasi}

📝 SUMMARY:
{summary}

🔑 KEY POINTS:
- {point 1}
- {point 2}
...

🏷️ #{hashtag1} #{hashtag2}
```

## Batasan
- Transcript tidak selalu tersedia (video возраст restricted, CC disabled)
- Video sangat panjang (>1 jam) mungkin perlu waktu lebih lama
- Playlist besar mungkin perlu proses per-video

## Contoh Output

```
📺 Cara Membuat SaaS dalam 30 Menit - Tutorial Lengkap
👤 Tech Indonesia
📅 15 Jan 2024 | 👁️ 125RB views | ⏱️ 32:15

📝 SUMMARY:
Video ini menjelaskan step-by-step cara membangun Software as a Service (SaaS) 
dari nol sampai launch. Mulai dari ideation, tech stack, database design, 
sampe deployment dan marketing strategy.

🔑 KEY POINTS:
• Ide SaaS yang profitable biasanya solve masalah spesifik
• Tech stack: Next.js + Supabase + Vercel = combo minimalist
• Penting banget: authentication & payment integration dari day 1
• MVP harus launch dalam 2-4 minggu, bukan 6 bulan
• Growth strategy: content marketing + cold email + partnership

⏱️ TIMESTAMPS:
00:00 - Intro
02:30 - Ideation & Validation
08:15 - Tech Stack Selection
15:00 - Database Design
22:30 - MVP Development
28:00 - Launch Strategy
30:45 - Q&A

🏷️ #saas #startup #tutorial #tech #indonesia
```

## Tips
- Kalau transcript gak ada, bisa pakai audio extraction + whisper AI
- Untuk video tutorial, minta breakdown per section
- Untuk podcast/interview, minta highlight quote terbaik
