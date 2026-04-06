# 🛒 Shopping List — Smart Grocery Route Optimizer

A free, real-time shared shopping list that sorts your items in the exact order of your supermarket's layout — so you never backtrack through the store again.

---

## What makes this different?

Most shopping list apps sort by generic categories. This app sorts by **your store's actual layout** — the order you walk through it. Add items on your phone, and the Route tab shows them in the exact sequence you'll encounter them in the store.

The first version of the app takes a practical approach: you define your store's section order once in Settings, and from then on every item falls into place automatically. It takes about two minutes to set up and works perfectly for your regular store from day one.

- Your partner adds items from home → you see them instantly at the store
- Items are auto-categorized as you type (supports English, Swedish, and Finnish)
- Tap any category badge to reassign it — the app remembers your corrections
- Drag to reorder items or categories however you like
- Works on any phone, no app installation needed

---

## Features

### 📋 Smart list
- Type an item and it's instantly categorized — *bananer* → Frukter, *diskmedel* → Tvätt
- Supports Swedish, Finnish, and English item names out of the box
- Tap the colored category badge on any item to reassign it
- The app remembers your corrections and uses them next time
- Drag items to reorder them manually

### 🗺️ Route optimizer
- Items are automatically sorted by your store's walk order
- Empty categories are hidden — only sections you need are shown
- Tap any item in the Route view to check it off as you pick it up
- Progress bar tracks how many items you've collected

### 👨‍👩‍👧 Household sharing
- Create an account and invite your partner or household members
- Everyone sees the same list in real time — changes appear within a second
- Each household has completely private data
- The owner can add or remove members at any time

### ⚙️ Settings
- Define your store's category order by dragging categories into the right sequence
- Add, rename, or delete categories on the fly
- See which words are remembered for each category
- Move or delete remembered words at any time

---

## How to use

1. Open the app at your hosted URL
2. Register a free account
3. Go to **Settings → Categories** and drag the categories into the order of your local supermarket
4. Start adding items — they'll be auto-categorized and sorted instantly
5. At the store, open the **Route** tab and work through the list section by section
6. To share with your partner: **Settings → Household → Invite someone** → send them the link

### Add to your home screen (iPhone)
1. Open the app in Safari
2. Tap the Share button (box with arrow)
3. Tap **Add to Home Screen**
4. It will appear like a native app on your home screen

---

## Self-hosting

Want to run your own private instance? It takes about 10 minutes and is completely free.

### Prerequisites
- A [GitHub account](https://github.com)
- A [Firebase account](https://firebase.google.com) (free Spark plan is enough)

### Steps

**1. Fork this repository**
Click the Fork button in the top right of this page.

**2. Create a Firebase project**
- Go to [console.firebase.google.com](https://console.firebase.google.com)
- Create a new project
- Enable **Realtime Database** (choose a region close to you)
- Enable **Authentication → Email/Password**
- Register a web app and copy your config keys

**3. Update the config in index.html**
Replace the `firebaseConfig` object in `index.html` with your own keys:
```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.YOUR_REGION.firebasedatabase.app",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

**4. Set Firebase Database Rules**
In Firebase Console → Realtime Database → Rules:
```json
{
  "rules": {
    "users": {
      "$householdId": {
        ".read": "auth != null && root.child('profiles').child(auth.uid).child('householdId').val() == $householdId",
        ".write": "auth != null && root.child('profiles').child(auth.uid).child('householdId').val() == $householdId"
      }
    },
    "profiles": {
      "$uid": {
        ".read": "auth != null && auth.uid == $uid",
        ".write": "auth != null && auth.uid == $uid"
      }
    },
    "invites": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

**5. Enable GitHub Pages**
- Go to your forked repo → Settings → Pages
- Set Source to `main` branch, `/ (root)` folder
- Your app will be live at `https://yourusername.github.io/shopping-list`

---

## Roadmap

- [ ] Native iOS and Android app (React Native)
- [ ] Multiple store layouts per household
- [ ] Precise item location within a section (aisle number, shelf)
- [ ] Crowdsourced store layouts — map a store once, share it with others
- [ ] Recipe integration — add all ingredients from a recipe in one tap
- [ ] Barcode scanner for adding items

---

## Tech stack

- **Frontend** — Vanilla HTML, CSS, JavaScript (single file, no build step)
- **Backend** — Firebase Realtime Database
- **Auth** — Firebase Authentication
- **Hosting** — GitHub Pages

No frameworks, no dependencies, no monthly fees. The entire app is one HTML file.

---

## Contributing

Contributions are welcome! If you'd like to add support for more languages, improve categorization, or build new features — open an issue or submit a pull request.

If you map out the layout of a supermarket chain and want to share it, open an issue with the store name, country, and category order — we'd love to include it.

---

## License

MIT — free to use, fork, and modify.

---

