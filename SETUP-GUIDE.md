# RestroFlow — Setup Guide (Roman Urdu)

RestroFlow ek free restaurant/hotel app hai jo PC aur mobile dono par chalti hai.
Har dish ki recipe (raw material) andar set hoti hai, bill banate hi stock apne aap kam hota hai,
lekin bill par sirf dish ka naam, price aur GST dikhta hai.

---------------------------------------------------------------
## 1. App kholna (sabse aasan tareeqa)

**PC par:** `index.html` file par double-click karein. Chrome mein khulegi. Bas.

**Mobile par:** `index.html` ko hosting par daalna padega (Part 6 dekhein), phir link Chrome mein kholein
aur ⋮ menu → "Add to Home screen" dabayein. App ka icon mobile par aa jayega.

---------------------------------------------------------------
## 2. Pehli baar setup

1. Restaurant ka naam, phone, address, GSTIN (agar hai) likhein.
2. Bill type chunein:
   - **Restaurant 5% GST** (normal restaurant, CGST 2.5% + SGST 2.5%)
   - **Hotel restaurant 18% GST** (jis hotel mein room 7,500 se upar ka ho)
   - **Composition scheme** (bill par GST nahi dikhta)
   - **No GST** (simple bill)
3. Owner PIN aur Cashier PIN set karein (alag alag, 4 se 6 number).
4. "Demo menu load karein" par tick rehne dein, taake app ko pehle try kar sakein.
   Baad mein Settings → "Delete menu, stock & everything" se demo hata sakte hain.

**Owner** ko sab dikhta hai (recipe, cost, stock, reports, settings).
**Cashier** ko sirf Billing aur Bills dikhte hain. Recipe aur raw material usko nazar nahi aate.

---------------------------------------------------------------
## 3. Roz ka kaam (Cashier)

1. **Billing** → table par tap karein.
2. Dish par tap karein (Half/Full ho toh size chunein). Qty + / − se badlein.
3. **KOT** dabayein, kitchen ka parcha print hoga aur **us waqt stock automatic kam ho jata hai.**
4. Customer ka bill: **Bill & Pay** → Cash / UPI / Card chunein → Confirm.
5. Bill par sirf naam, qty, rate, amount, GST aur total aata hai. Raw material kahin nahi dikhta.
6. Print ya WhatsApp se customer ko bhej sakte hain.

Takeaway, Delivery aur Room service ke liye upar ke buttons use karein.

**Security:** KOT ja chuka item hatane ya order cancel karne par Owner PIN maangta hai.
Owner ke Reports mein "Control report" dikhata hai kis ne kya hataya.

---------------------------------------------------------------
## 4. Apna menu aur recipe daalna (Owner)

**Step A: Raw material (Stock → Raw materials → Add)**
Naam (Chicken), unit (kg / litre / pieces), price per kg, abhi kitna stock hai, aur kitne par alert chahiye.

**Step B: Gravy base (Stock → Gravy bases → Add)**
Jo gravy aap pehle se bana kar rakhte hain (red gravy, makhani gravy, dal).
Ek batch ki recipe likhein (kitna pyaz, tamatar, tel...) aur ek batch se kitne kg gravy banti hai.
Jab gravy banayein: **Make a batch** dabayein, raw material kam hoga aur gravy ka stock badh jayega.

**Step C: Dish (Menu → Add dish)**
Naam, category, price likhein. Half/Full chahiye toh "Add size" dabayein.
Recipe mein ek portion ka saman likhein. Jaise Butter Chicken:
- Chicken 250 g
- Makhani Gravy 200 g
- Butter 15 g
- Cream 20 ml

Neeche app khud dikhata hai: cost, margin, food cost %.

**Step D: Khareedari (Stock → Purchases → New purchase)**
Maal aate hi quantity aur total price likhein. Stock badh jayega aur average cost khud nikal jayegi.

**Bachi cheezein:** Wastage (kharab/jala hua maal) Stock → Wastage mein likhein.
Mahine mein ek baar Stock → Stock count se asli maal gin kar system se milayein.

---------------------------------------------------------------
## 5. Reports (Owner)
Aaj, kal, 7 din, mahina: sales, GST summary, profit (andaza), dish-wise bikri aur munafa,
raw material kitna use hua, wastage, aur CSV download.

---------------------------------------------------------------
## 6. Free hosting (GitHub Pages) — taake mobile par bhi chale

1. github.com par apne account se login karein.
2. Upar "+" → **New repository** → naam `restroflow` → **Public** → Create.
3. "uploading an existing file" par click karein.
4. Is folder ki sab files drag karein: `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`.
5. **Commit changes** dabayein.
6. Repository ki **Settings → Pages** → Branch: `main`, folder: `/ (root)` → Save.
7. 1–2 minute baad link milega: `https://aapka-username.github.io/restroflow/`
8. Wo link PC aur mobile dono par kholein.

(Ya mujhe bolein, main aapke GitHub par yeh khud daal dunga.)

---------------------------------------------------------------
## 7. PC + Mobile ka data sync (free Firebase)

Bina sync ke har device ka data alag rehta hai. Sync ke liye (ek baar ka kaam):

1. console.firebase.google.com par Google account se login → **Add project** → naam `restroflow` →
   Google Analytics band kar dein → Create.
2. Left menu **Build → Firestore Database → Create database**. Location: `asia-south1 (Mumbai)`.
   **Production mode** chunein → Enable.
3. Firestore ke **Rules** tab mein yeh paste karein aur **Publish** dabayein:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

4. **Build → Authentication → Get started → Email/Password → Enable → Save.**
   Phir **Users** tab → **Add user** → ek email aur password banayein (yeh sirf sync ke liye hai, yaad rakhein).
5. Upar gear icon → **Project settings** → neeche **Your apps** → `</>` (Web) →
   naam likhein → Register. Wahan `firebaseConfig = {...}` wala block dikhega, usko copy karein.
6. RestroFlow mein **Settings → Cloud sync**: config paste karein, sync email aur password likhein, **Connect** dabayein.
7. Connect hone ke baad **Copy setup code** dabayein.
8. Dusre device (mobile) par app kholein, pehli screen par **Enter setup code** par code paste karein.
   Poora data wahan aa jayega.

Status bar mein "Cloud synced" dikhega. Internet jaye toh app chalta rehta hai, wapas aane par data khud sync ho jata hai.

Note: Firebase ki free limit ek chhote/medium restaurant ke liye kaafi hai. Agar Firebase "billing" maange
ya free option na dikhaye, toh mujhe screenshot bhejein.

---------------------------------------------------------------
## 8. Printing
- 80mm ya 58mm thermal printer PC se connected ho toh Print dabane par seedha print hota hai.
- Android mobile par Bluetooth printer ke liye free app "RawBT" ya phone ki Print service use hoti hai.

## 9. Backup
Settings → **Download backup** (har hafte karein). Cloud sync on ho toh data cloud mein bhi rehta hai.

## 10. Abhi nahi hai (agle version mein ho sakta hai)
UPI QR bill par, kitchen display screen, Zomato/Swiggy order import, loyalty/customer khata, Hindi/Urdu app screens.
