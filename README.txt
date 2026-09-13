========================================================
 SHELFCOUNT — Grocery Camera Scanner & Inventory App
========================================================

WHAT THIS IS
------------
ShelfCount is a mobile app you run in your phone's browser (a
"Progressive Web App" / PWA). It uses your phone's CAMERA to scan
product barcodes, looks up the product name automatically where
possible, lets you confirm/edit the details and quantity, and keeps
a running inventory list. Tapping "View Items" generates a report
you can browse, search, and download as an Excel (.xlsx) file.

No native Android/iOS app-store build is required, and every tool
used below is completely free with no license fees:

  - HTML / CSS / JavaScript      -> open web standards, free forever
  - BarcodeDetector API          -> built into the Chrome/Android
                                     browser itself, nothing to install
  - SheetJS ("xlsx" library)     -> Apache 2.0 open-source license,
                                     loaded automatically from a free CDN
  - Open Food Facts product API  -> free, open, no API key or sign-up
                                     (used only to auto-fill a product's
                                     name/brand when it's in their
                                     public database; if it isn't, you
                                     just type the name in yourself)


FILES IN THIS FOLDER
---------------------
  index.html      The entire app (camera scanner + inventory + report)
  manifest.json   Lets the phone install it as an app icon
  sw.js           Small "service worker" so it also works offline
  icon.svg        App icon
  README.txt      This file


------------------------------------------------------
STEP 1 — GET THE APP ONTO YOUR PHONE (pick ONE option)
------------------------------------------------------

OPTION A — Quickest: host it for free with GitHub Pages
  1. Create a free GitHub account at github.com (no license/fees).
  2. Create a new repository, upload all 5 files in this folder.
  3. In the repo, go to Settings > Pages > set source to "main"
     branch, root folder. Save.
  4. GitHub gives you a URL like:
     https://yourname.github.io/shelfcount/
  5. Open that URL on your phone in CHROME (Android is best
     supported — see "Browser Notes" below).

OPTION B — No account needed: Netlify Drop
  1. Go to https://app.netlify.com/drop in a desktop browser
     (free, no credit card, no license).
  2. Drag this whole folder onto the page.
  3. It gives you an instant free public URL — open that on your
     phone.

OPTION C — Local network only (no hosting at all)
  1. On a computer on the same Wi-Fi as your phone, open a terminal
     in this folder and run:
        python3 -m http.server 8080
     (Python is free and usually already installed on Mac/Linux;
     on Windows install it free from python.org.)
  2. Find your computer's local IP address (e.g. 192.168.1.20).
  3. On your phone's browser, go to: http://192.168.1.20:8080
  Note: camera access normally requires a secure "https://" address
  or "localhost" — a plain local http:// address may block the
  camera on some phones. Options A or B avoid this problem entirely
  and are recommended.


------------------------------------------------------
STEP 2 — "INSTALL" IT LIKE A REAL APP (OPTIONAL BUT NICE)
------------------------------------------------------
Once the page is open on your phone in Chrome:
  1. Tap the browser menu (⋮).
  2. Tap "Add to Home screen" / "Install app".
  3. It now opens full-screen with its own icon, just like a
     regular installed app — with no browser address bar.


------------------------------------------------------
STEP 3 — HOW TO USE THE APP
------------------------------------------------------

SCANNING AN ITEM
  1. Open the app — you land on the "Scan" tab.
  2. Tap "Start Scanning". Allow camera access when your phone
     browser asks for it.
  3. Point the camera at a product's barcode, holding it inside the
     bracket frame, a few inches away, in good light.
  4. When it reads the code you'll feel a short vibration and a
     "Confirm Item" panel pops up.
       - If the product is in the free Open Food Facts database,
         Name/Brand/Category are filled in for you automatically.
       - If not, just type the item's name in yourself.
       - Set the Quantity, and optionally Price and Location
         (e.g. "Aisle 3, Shelf B").
  5. Tap "Add to Inventory". The panel closes and the camera keeps
     running so you can immediately scan the next item.
  6. If you scan the SAME barcode again later, the app recognises
     it and increases that item's quantity instead of creating a
     duplicate row.

ITEMS WITHOUT A BARCODE
  Tap "+ Add item manually (no barcode)" under the Start Scanning
  button, fill in the details by hand, and tap "Add to Inventory".

VIEWING THE REPORT
  1. Tap "View Items" at the bottom of the screen.
  2. You'll see:
       - Total SKUs (distinct products), Total Units, and Total
         Value (if you entered prices).
       - A searchable list of every item — search by name, brand,
         or barcode using the search box.
       - +/- buttons to adjust quantity, or "Remove" to delete a
         line.
  3. Tap "Download Excel Report" to save a real .xlsx spreadsheet
     of the full inventory to your phone (Item Number, Category,
     Item Name, Brand, Barcode, Quantity, Price, Condition,
     Location, and timestamps).
  4. "Clear All" wipes the list if you want to start a fresh count
     (it will ask you to confirm first).


------------------------------------------------------
BROWSER / DEVICE NOTES
------------------------------------------------------
  - Best experience: CHROME on ANDROID. It has built-in native
    barcode scanning (the "BarcodeDetector" browser feature) with
    zero extra software.
  - iPhone (Safari) currently does not support live barcode
    scanning in the browser the same way. On iPhone, use
    "+ Add item manually" to type in items — everything else
    (the list, report, and Excel export) works the same.
  - If "Start Scanning" is greyed out, your browser doesn't support
    live scanning — manual entry still works fully.
  - The app needs an internet connection only to (a) look up a
    product name automatically and (b) load the Excel export tool
    the first time. Scanning and manually adding items still work
    with no connection; the product name field will just stay
    blank for you to fill in.


------------------------------------------------------
MAKING IT PERMANENT / STANDALONE (OPTIONAL)
------------------------------------------------------
As delivered, item data is kept only for your current browsing
session so this also runs safely as a live preview. Once you host
it yourself (Step 1), you can make the list persist between visits
by storing it in the phone's own browser storage. In index.html,
find the "Storage abstraction" section near the top of the
<script> block and add this to the "else" branch of loadItems()/
saveItems() — this uses the browser's standard localStorage, which
is free and built in:

    function loadItems(){
      var raw = localStorage.getItem('shelfcount-items');
      return raw ? JSON.parse(raw) : [];
    }
    function saveItems(items){
      localStorage.setItem('shelfcount-items', JSON.stringify(items));
    }

That's it — no paid database, backend, or license required.


------------------------------------------------------
WANT A REAL APP-STORE APK/IPA LATER?
------------------------------------------------------
If you eventually want this packaged as a downloadable Android/iOS
app instead of a browser app, these are the standard FREE,
open-source tools for wrapping a web app like this one — no
license fees for any of them:

  - PWABuilder (pwabuilder.com) — free tool from Microsoft that
    packages a PWA into an Android/iOS app.
  - Bubblewrap (github.com/GoogleChromeLabs/bubblewrap) — free,
    open-source (Apache 2.0) command-line tool from Google for the
    same purpose.
  - Capacitor (capacitorjs.com) — free, open-source (MIT license)
    framework for wrapping web apps as native apps.

These require installing Android/Xcode build tools on a computer
with internet access, so they're a later step, not needed to use
the app today.

========================================================
