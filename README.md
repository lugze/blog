# 🐧 LugZe Blog

> **Linux User Group of Zenica** — tutorijali, savjeti i resursi iz svijeta Linuxa, open-source-a i programiranja.

🌐 **Live:** [lugze.github.io/blog](https://lugze.github.io/blog/)

---

## 📖 Sadržaj bloga

| Sekcija | Opis |
|---------|------|
| 📝 **Blog postovi** | Tutorijali o Linuxu, Rubyju, shell skriptama i više |
| 🐧 **Mala Škola Linux-a** | Osnove Linux-a — filesystem, korisnici, permisije, procesi, mreža |
| 🔧 **Linux komande** | Kompletna referenca Linux komandi od A do Z |
| 📂 **Kategorije** | Postovi organizovani po temama: Linux, Ruby, Blog, LugZe |
| ❓ **FAQ** | Često postavljana pitanja |
| 🗄️ **Arhiva** | Link na arhivu stare stranice |

## 🚀 Lokalni razvoj

### ✅ Preduvjeti

- [Ruby](https://www.ruby-lang.org/) instaliran na sistemu
- [Bundler](https://bundler.io/) gem

### 📥 Kloniranje i pokretanje

```bash
# Kloniraj repo
git clone git@github.com:lugze/blog.git
cd blog

# Instaliraj bundler (ako nemaš)
gem install bundler
bundle update --bundler

# Instaliraj zavisnosti
bundle install

# Pokreni lokalni server
bundle exec jekyll serve
```

🌍 Otvori u browseru: **http://localhost:4000/blog/**

## 🛠️ Tehnologije

| Alat | Verzija |
|------|---------|
| 💎 Jekyll | ~> 3.8 |
| 🎨 Tema | Minima ~> 2.0 (prilagođena) |
| ✍️ Markdown | Kramdown (GFM) |
| 📡 Feed | jekyll-feed |
| 🎬 Terminal snimci | jekyll-asciinema |

## 📁 Struktura projekta

```
blog/
├── _config.yml          # ⚙️  Jekyll konfiguracija
├── _posts/              # 📝 Blog postovi (Markdown)
├── _layouts/            # 🎨 Prilagođeni layout-i
├── _includes/           # 🧩 Header, footer, head
├── assets/
│   ├── css/style.scss   # 🎨 Custom SCSS stil
│   └── images/          # 🖼️  Slike za postove
├── index.md             # 🏠 Početna stranica
├── kategorije.md        # 📂 Kategorije postova
├── msl.md               # 🐧 Mala Škola Linux-a
├── linux-komande.md     # 🔧 Linux komande A-Z
├── about.md             # ℹ️  O nama
├── faq.md               # ❓ FAQ
├── arhiva.md            # 🗄️  Arhiva
├── Gemfile              # 💎 Ruby zavisnosti
└── README.md            # 📄 Ovaj fajl
```

## 🤝 Doprinos

1. 🍴 Forkuj repo
2. 🌿 Napravi branch (`git checkout -b moj-post`)
3. ✍️ Dodaj post u `_posts/` (format: `YYYY-MM-DD-naslov.md`)
4. 💾 Commituj promjene
5. 🚀 Otvori Pull Request

## 📜 Licenca

Otvoreni sadržaj za zajednicu. 🐧❤️
