# write-your-letter 💌

A small one-page site that shows a love letter. It opens on a sealed envelope that says "tap to open", and tapping it reveals the letter. It's designed for phones, so someone can tap an NFC tag and read the letter right away.

---

## 1. Add your letter

Open `index.html` in any text editor and find this comment:

```html
<!-- ✍️ WRITE YOUR LETTER HERE.
```

1. **Delete the placeholder** (the lined blank space) right below it:
   ```html
   <div class="placeholder"></div>
   ```
2. **Add your paragraphs**, one `<p>` per paragraph:
   ```html
   <p>The first time I saw you...</p>
   <p>Every day with you...</p>
   ```
3. **Change the greeting.** Find `My love,` inside `<h1 class="greeting">`.
4. **Change the signature.** Find `Your Name` inside `<span class="name">`. You can also edit `Forever yours,` just above it.
5. *(Optional)* Change the browser tab title in `<title>For You ♡</title>`.

To preview it, open `index.html` in your browser by double-clicking it.

Then save your changes and push them:
```bash
git add index.html
git commit -m "Write the letter"
git push
```

---

## 2. Host it (keeping the repo private)

The NFC tag needs a **public web address**, but your code can stay in a **private** repo.

> ⚠️ GitHub Pages doesn't work with private repos on a free GitHub account. Use Netlify instead (free).

### Netlify (recommended, free)
1. Go to **https://app.netlify.com** and **sign in with GitHub**.
2. Click **Add new site → Import an existing project → GitHub**.
3. Give Netlify access to the **`write-your-letter`** repo. You can choose to give access to this repo only.
4. Build settings:
   - **Build command:** *(leave empty)*
   - **Publish directory:** `.` *(or leave empty)*
5. Click **Deploy**. You get a URL like `https://random-name-123.netlify.app`.
6. *(Optional)* Go to **Site configuration → Change site name** to get a nicer link, like `https://for-my-love.netlify.app`.

Each `git push` to `main` **redeploys automatically**, and the URL stays the same.

### Alternatives
- **Vercel** (https://vercel.com): also free and works with private repos. Import the repo, then deploy with the default settings.
- **Netlify Drop** (https://app.netlify.com/drop): drag the folder onto the page, no GitHub needed. It doesn't update automatically, though; you have to drag the folder in again after each change.

> 🔒 Your **code** stays private, but anyone with the site **URL** can read the letter. The link is hard to guess, but it isn't password protected.

---

## 3. Write the link to the NFC tag

Use the **NFC Tools** app (iOS or Android):

1. Open **NFC Tools** and go to the **Write** tab.
2. Tap **Add a record → URL / URI**.
3. Enter your site URL. Keep `https://`, e.g. `https://for-my-love.netlify.app`.
4. Tap **OK**, then **Write / X bytes**.
5. Hold the tag against the back of your phone until you see **"Write complete"**.

### Test it
Close the app, unlock your phone, and bring the tag close to it:
- **iPhone (XS or newer):** a notification appears at the top. Tap it to open the letter.
- **Android:** turn on NFC (*Settings → Connected devices → NFC*). The link opens automatically or after one tap.

### Tips
- **Write the tag once.** Because the URL never changes, you can write the tag now and edit the letter later just by pushing to GitHub.
- **Antenna spots:** near the top of the back on iPhone, and the middle of the back on most Android phones.
- **Capacity:** small tags (NTAG213) hold about 130 characters, so keep the URL short.
- **Metal surfaces** block NFC. Use an "anti-metal" tag if you're sticking it on metal.
- **Locking** (*NFC Tools → Other → Lock tag*) stops anyone from rewriting the tag, but it's **permanent**. Only lock it once you're sure of the URL.
