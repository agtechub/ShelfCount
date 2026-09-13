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


