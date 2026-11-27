# write-your-letter 💌

A small one-page site that shows a love letter. It opens on a sealed envelope that says "tap to open", and tapping it reveals the letter. It's designed for phones, so someone can tap an **NFC tag** and read your letter right away.

*Optional:* you can make the letter open only with a secret link (`?k=your-secret-key`). See [Optional: secret link](#optional-secret-link).

---

## How it works

```
index.html     ← the page (you don't need to edit this)
letter.js      ← your letter text goes here
robots.txt     ← asks search engines not to list the site
```

The page reads your letter from `letter.js`. To keep the letter behind a secret link, see [Optional: secret link](#optional-secret-link) below.

---

## 1. Make your own private copy

This repo is a **public template**, so **don't write your letter here**. Put it in your own private copy:

1. Click **Use this template → Create a new repository** at the top of this page.
2. Name it whatever you like, e.g. `my-letter`, and choose **Private**.
3. Clone it to your computer.

Or use the GitHub CLI:
```bash
gh repo create my-letter --private --template <owner>/write-your-letter --clone
```

---

## 2. Write your letter

Open `letter.js` in any text editor:

```js
window.LETTER = {
  greeting: "My love,",
  paragraphs: [
    "The first time I saw you...",
    "Every day with you...",
  ],
  signoff: "Forever yours,",
  name: "Your Name",
};
```

- Each item in `paragraphs` is one paragraph. Wrap it in `"quotes"` and end it with a comma.
- To use a quote mark inside the text, write `\"`. For example: `"You said \"hi\" and I melted."`
- If `paragraphs` is empty, the letter shows blank lined paper.

**Preview locally:** double-click `index.html`.

---

## 3. Save and push

```bash
git add -A
git commit -m "Write the letter"
git push
```

---

## 4. Host it for free (Netlify)

GitHub Pages doesn't work with private repos on a free account, so use **Netlify** instead:

1. Go to **https://app.netlify.com** and **sign in with GitHub**.
2. Click **Add new site → Import an existing project → GitHub**.
3. Give Netlify access to **your private copy**. You can choose to give access to only that repo.
4. Leave the **build command** empty and set the **publish directory** to `.` (or leave it empty).
5. Click **Deploy**. You get a URL like `https://random-name-123.netlify.app`.
6. *(Optional)* Go to **Site configuration → Change site name** to get a nicer link.

Each `git push` **redeploys automatically**, and the URL stays the same.

> ⚠️ If your site shows **401 Unauthorized** to other people, turn off visitor protection: **Site configuration → Access & security → Visitor access → No protection**.

> Vercel (https://vercel.com) also works: import the repo and deploy with the default settings.

---

## 5. Write the link to an NFC tag

Use the **NFC Tools** app (iOS or Android):

1. Open **NFC Tools** and go to the **Write** tab.
2. Tap **Add a record → URL / URI**.
3. Enter your site URL, including `https://` (and `?k=...` if you use a secret link).
4. Tap **OK**, then **Write / X bytes**.
5. Hold the tag against the back of your phone until you see **"Write complete"**.

### Test it
Close the app, unlock your phone, and bring the tag close to it:
- **iPhone (XS or newer):** a notification appears at the top. Tap it to open the letter.
- **Android:** turn on NFC (*Settings → Connected devices → NFC*). The link opens automatically or after one tap.

### Tips
- **Write the tag once.** The link never changes, so you can edit the letter later just by pushing.
- **Antenna spots:** near the top of the back on iPhone, and the middle of the back on most Android phones.
- **Capacity:** small tags (NTAG213) hold about 130 characters, so keep the URL short.
- **Metal surfaces** block NFC. Use an "anti-metal" tag if you're sticking it on metal.
- **Locking** (*NFC Tools → Other → Lock tag*) stops anyone from rewriting the tag, but it's **permanent**.

---

## Optional: secret link

By default, anyone with your site URL can read the letter. If you want it to open **only** with a secret link (`?k=your-key`):

1. Pick a random key (letters, numbers, `-` and `_` only, up to 64 characters):
   ```bash
   openssl rand -base64 12 | tr -dc 'A-Za-z0-9' | head -c 12; echo
   ```
2. Move your letter into a `letters/` folder, named after the key:
   ```bash
   mkdir -p letters
   git mv letter.js letters/x7Gq92LmPz4.js
   ```
   ⚠️ Don't leave a copy of `letter.js` behind, or the plain URL will still show the letter.
3. Push. Your letter now opens only at:
   ```
   https://your-site.netlify.app/?k=x7Gq92LmPz4
   ```
   The plain URL, or a wrong key, shows a sealed envelope that won't open.
4. Write the **full** link, including `?k=...`, to your NFC tag.

**Preview locally:** paste the file path with the key into your browser's address bar, e.g. `file:///Users/you/my-letter/index.html?k=x7Gq92LmPz4`.

To go back, run `git mv letters/x7Gq92LmPz4.js letter.js`.

---

## How private is it?

- ✅ Your letter text lives only in your **private** repo.
- ✅ Search engines are asked not to list the site (`robots.txt` plus a `noindex` tag).
- ⚠️ Without a secret link, anyone with your site URL can read the letter.
- ⚠️ With a secret link, anyone who **has the full link** can read it, including someone who scans the tag. It's hard to guess, but it isn't a password.
