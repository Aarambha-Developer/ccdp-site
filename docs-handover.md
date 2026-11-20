# CCDP Website — Setup Instructions for the IT Team

Creative Children Development Programme (CCDP), Pokhara, Nepal.

This is a **static website**: plain HTML, CSS and JavaScript plus images and one video.
There is no database, no CMS and no build step. Any ordinary web hosting will work.

---

## 1. What's in this folder

```
ccdp-website/
├── index.html          ← the whole website (all pages, styles and scripts)
├── video.mp4           ← opening film on the home page (~10 MB)
├── README.md           ← this file
└── img/
    ├── header.jpg, logo.png, logo-mark.png, video-poster.jpg
    ├── odahare-village-school-*.jpg
    ├── scholarship-*.jpg
    ├── children-home-*.jpg
    ├── farm-featured.jpg
    ├── shankar-portrait.jpg, shankar-bishnu.jpg, shristhi.jpg
    ├── agm-*.jpg
    └── board/          ← one portrait per board member
```

Keep the folder structure exactly as it is. The site loads files by relative path (`img/...`, `video.mp4`).

## 2. How to upload

**Shared hosting (cPanel, Plesk, etc.)**
1. Unzip this folder on your computer.
2. Open File Manager, or connect by FTP/SFTP (for example with FileZilla).
3. Upload the **contents** of the folder (`index.html`, `video.mp4`, `img/`) into the web root, usually `public_html/` or `www/`.
   Don't upload the outer folder itself, or the site will appear at `yourdomain.org/ccdp-website/`.
4. Visit the domain. The home page should open with the video.

**Free static hosts (alternatives)**
- **Netlify:** drag and drop the unzipped folder at app.netlify.com/drop, then connect your domain.
- **GitHub Pages / Cloudflare Pages:** push the folder to a repository and enable Pages. No build command is needed, and the output directory is the root.

**Required:** enable HTTPS (free Let's Encrypt certificate in most control panels).

## 3. How the pages work

All pages live inside `index.html` and switch using the part of the URL after `#`:

| Page | URL |
|---|---|
| Home | `/` or `/#home` |
| About Us | `/#about` |
| Gallery | `/#gallery` |
| Odahare Village School | `/#odahare-school` |
| Scholarship Programme | `/#scholarship` |
| Children Home | `/#children-home` |
| The Farm | `/#farm` |
| Shankar's Story | `/#story-shankar` |
| Shristhi's Story | `/#story-shristhi` |
| 14th AGM & New Board | `/#story-agm` |
| Home sections | `/#projects`, `/#stories`, `/#donate`, `/#contact` |

These links can be shared directly, for example `ccdp.org.np/#donate`.

## 4. ⚠️ Placeholders to replace before going live

Open `index.html` in any text editor (VS Code, Notepad++), use **Find** (Ctrl+F) for each item below, and replace it.

| What | Search for | Replace with |
|---|---|---|
| Phone number | `+977 98XX-XXXXXX` and `tel:+9779800000000` | the real number, in both places |
| Bank name | `[Bank name]` | e.g. `Nabil Bank Ltd.` |
| Account number | `XXXX XXXX XXXX` and `data-c="XXXXXXXXXXXX"` | the real account number, in both places |
| SWIFT code | `XXXXNPKA` (appears twice) | the real SWIFT/BIC code |
| PayPal | `business=ccdpnepal%40gmail.com` (appears twice) | the email of CCDP's PayPal account, or a PayPal *hosted button* link (see below) |
| Facebook | `https://www.facebook.com/` | the CCDP Facebook page URL |
| Instagram | `https://www.instagram.com/` | the CCDP Instagram URL |
| YouTube | `https://www.youtube.com/` | the CCDP YouTube URL |
| WhatsApp | `https://wa.me/` | `https://wa.me/9779XXXXXXXXX` (number with no + or spaces) |
| Placeholder notes | `PayPal account to be confirmed` and `Bank details are placeholders` | delete these two sentences once the details are real |

**PayPal (recommended):** in the PayPal Business account, go to *Pay & Get Paid → Donate button*, create a button, and copy its link
(`https://www.paypal.com/donate/?hosted_button_id=XXXX`). Then, in `index.html`, find `function bindDonate` and the `id="ppbtn"` link and use that URL instead of the `business=` one.
The PayPal account must be verified and set up for donations.

## 5. Optional: embed a live Google Map

The footer currently shows a map graphic that opens Google Maps when clicked.
On a real host you can replace it with an embedded map:

1. Open Google Maps, find the CCDP Children Home, then click **Share → Embed a map → Copy HTML**.
2. In `index.html`, find `<a class="map"` and replace that whole `<a>…</a>` block with:
   ```html
   <div class="map"><iframe src="PASTE_EMBED_URL_HERE" style="border:0;width:100%;height:100%" loading="lazy" allowfullscreen></iframe></div>
   ```

## 6. Editing content later

Everything editable is near the top of the `<script>` section in `index.html`:

- **`PHOTOS`**: every gallery photo, with its title (`t:`) and caption (`c:`). Edit the text between the quotes.
  To add a photo, put the file in `img/` and add a line such as
  `{f:'new-photo.jpg',p:'scholarship',t:'Title',c:'Caption'},`
  (`p:` must be `odahare-school`, `scholarship`, `children-home` or `farm`).
- **`BOARD`**: board member names and roles. Portraits are in `img/board/`.
- **`PROJECTS`**: the text, quote and four highlight boxes for each project page.
- **Story text**: search for `function pageShankar`, `function pageShristhi` or `function pageAgm`.
  **Shristhi's story is a draft written without real details, so please replace it with her actual story.**
- **About Us text**: search for `function pageAbout`.

Use the straight quote `'` carefully inside these texts. If a sentence needs an apostrophe, use the curly `’` (as the existing text does), or the page may break.
After any edit, open the site and check that it still loads. If it comes up blank, the last edit has a typing error.

**Images:** use JPG, landscape where possible, about 1600–2200 px wide and under 500 KB each. Big phone photos should be resized first.

## 7. Recommended extras (optional)

- **Contact email:** create `info@yourdomain` and forward it to `ccdpnepal@gmail.com`.
- **Analytics:** add a Google Analytics or Plausible snippet before `</head>`.
- **Video size:** `video.mp4` is about 10 MB. If hosting bandwidth is limited, upload the film to YouTube or Vimeo and keep this file as is.
- **Backups:** keep a copy of this zip. It *is* the whole website.

## 8. Technical notes

- No server-side code. It works on Apache, Nginx, IIS or any static host.
- Fonts load from Google Fonts (Fraunces and Manrope). Everything else is local.
- It works in all modern browsers and on mobile. The home video autoplays muted, which is a browser rule, and visitors can turn the sound on.
- Registration details shown in the footer: Reg. No. 2973/069, SWC Affiliation No. 37106.
