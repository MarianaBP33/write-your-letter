# write-your-letter 💌

A small one-page site that shows a love letter. It opens on a sealed envelope that says "tap to open", and tapping it reveals the letter. It's designed for phones, so someone can tap an **NFC tag** and read your letter right away.

The letter only opens with a **secret link** (`?k=your-secret-key`). Anyone who visits the site without the key sees a sealed envelope and nothing else.

---

## How it works

```
index.html              ← the page (you don't need to edit this)
letters/example.js      ← your letter text goes here (rename it to your secret key)
robots.txt              ← asks search engines not to list the site
```

When someone opens `https://your-site.netlify.app/?k=x7Gq92LmPz4`, the page loads `letters/x7Gq92LmPz4.js`. Without the key there's nothing to load, so the envelope stays sealed. Your letter text is never inside `index.html`.

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

## 2. Pick a secret key

Generate a random key (letters, numbers, `-` and `_` only, up to 64 characters):
```bash
openssl rand -base64 12 | tr -dc 'A-Za-z0-9' | head -c 12; echo
```
Or just type something long and random, like `x7Gq92LmPz4`.

Then rename the letter file to match:
```bash
git mv letters/example.js letters/x7Gq92LmPz4.js
```

---

## 3. Write your letter

Open `letters/<your-key>.js` in any text editor:

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

**Preview locally:** open `index.html?k=<your-key>` in your browser. You can't double-click a link with `?k=` in it, so paste the full file path into the address bar, e.g. `file:///Users/you/my-letter/index.html?k=x7Gq92LmPz4`.

Then save your changes and push them:
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

Your **secret link** is then:
```
https://your-site.netlify.app/?k=x7Gq92LmPz4
```

> Vercel (https://vercel.com) also works: import the repo and deploy with the default settings.

---

## 5. Write the secret link to an NFC tag

Use the **NFC Tools** app (iOS or Android):

1. Open **NFC Tools** and go to the **Write** tab.
2. Tap **Add a record → URL / URI**.
3. Enter your **full secret link**, including `https://` and `?k=...`.
4. Tap **OK**, then **Write / X bytes**.
5. Hold the tag against the back of your phone until you see **"Write complete"**.

### Test it
Close the app, unlock your phone, and bring the tag close to it:
- **iPhone (XS or newer):** a notification appears at the top. Tap it to open the letter.
- **Android:** turn on NFC (*Settings → Connected devices → NFC*). The link opens automatically or after one tap.

### Tips
- **Write the tag once.** The link never changes, so you can edit the letter later just by pushing.
- **Antenna spots:** near the top of the back on iPhone, and the middle of the back on most Android phones.
- **Capacity:** small tags (NTAG213) hold about 130 characters, so keep the site name and key short.
- **Metal surfaces** block NFC. Use an "anti-metal" tag if you're sticking it on metal.
- **Locking** (*NFC Tools → Other → Lock tag*) stops anyone from rewriting the tag, but it's **permanent**.

---

## How private is it?

- ✅ Your letter text lives only in your **private** repo and in a file only the secret link points to.
- ✅ Search engines are asked not to list the site (`robots.txt` plus a `noindex` tag).
- ⚠️ Anyone who **has the full link** can read the letter. That includes someone who scans the tag or sees the link. It's hard to guess, but it isn't a password.
