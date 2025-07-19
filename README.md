# Welcome to StarWorld Status Board

A real-time, shareable status board inspired by the golden era of AIM, Twitter’s status roots, and early Facebook check‑ins. This lightweight JAMstack app lets **anyone** on the web update their status and watch it propagate instantly to every visitor.

---

## 🎯 Purpose

- **Bring back the spirit of status**: In the era of ephemeral Stories and algorithmic feeds, we’ve lost the simple joy of “What are you doing right now?”. This board restores that direct connection.
- **Low‑ops, high‑velocity**: Deploy as static HTML (+ JS) on Netlify and use Firebase Realtime Database for shared persistence—zero server maintenance.
- **Community node**: Perfect for small teams, creative circles, or public gatherings; everyone sees the same single source of truth.

---

## 🚀 Tech Stack & Rationale

| Layer                   | Choice            | Why?                                                                                       |
| ----------------------- | ----------------- | ------------------------------------------------------------------------------------------ |
| **Static Hosting**      | Netlify           | - Git‑backed auto-deploys or drag‑and‑drop upload
- Built‑in CDN, HTTPS, preview deploys
- Future JAMstack add‑ons (Forms, Identity, Edge) |
| **Real‑time Database**  | Firebase RTDB     | - Tiny JS SDK, 2‑minute setup
- Real‑time `.on('value')` listeners + `.set()` writes
- Generous free tier, zero‑ops global distribution |
| **Frontend**            | HTML + Vanilla JS | - Single-file simplicity
- No build step once configured
- Easy to inspect, customize, or evolve into Python or other frameworks |

---

## ⚙️ How It Works

1. **Netlify** serves `index.html` and eight avatar images from your repo root (no build command needed).
2. On page load, we:
   - Initialize Firebase App & Database (via `<script>` tags).
   - Query `/statuses/{id}` nodes for each crew member and populate the editable fields.
3. **Live Updates**:
   - Every keystroke in a `.status` `<div contenteditable>` triggers `db.ref('statuses/'+id).set(newText)`.
   - All connected clients receive `.on('value')` events and refresh their view instantly.
4. **UI Details**:
   - **Shimmering header**: CSS gradient + keyframes for that AIM‑style sparkle.
   - **Avatars**: Circular masks with dynamic zoom to hide square edges.
   - **Save indicator**: Per‑card timestamp in the lower-right, updated with each write.
   - **Placeholders**: Subtle `:empty:before` hint to “Click to leave a status…”

---

## 📂 File Structure

- `index.html` — The entire app in one file, with inline CSS & JS.
- `*.png`       — Avatar images for each crew member (same directory).

---

## 🔧 Next Steps & Customization

- **Styling**: Tweak CSS variables (colors, spacing, font) at the top of `index.html`.
- **New Members**: Copy a `.crew-member` block, assign a unique `data-id`, name, title, and avatar.
- **Access Control**: Lock down reads/writes in Firebase Console → Database Rules.
- **Offline Support**: Add Firebase’s offline persistence or local‑cache fallback.

---

_*Inspired by AIM, early Twitter status, and the lost craft of simple presence updates. May your statuses always sparkle.*_

