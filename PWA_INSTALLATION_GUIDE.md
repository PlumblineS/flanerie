# 📱 PWA Installation Guide for Flânerie

## What You're Getting

Your website can now be installed as an app! Users can add it to their home screen and use it like a native app.

---

## Files Created

1. ✅ **manifest.json** - Tells browsers this is an installable app
2. ✅ **service-worker.js** - Enables caching and offline functionality
3. ✅ **index.html** (UPDATED) - Added PWA meta tags and service worker registration
4. 📋 **ICON_INSTRUCTIONS.md** - How to create app icons

---

## Step-by-Step Installation

### Step 1: Get Your Icons Ready (Required!)

**Quick Option (5 minutes):**
1. Go to https://www.pwabuilder.com/imageGenerator
2. Upload any square logo/image (512x512 or larger)
3. Download the generated icons
4. Extract the ZIP file

You'll get all the icon sizes you need!

### Step 2: Upload Files to Your Server

Upload these files to your website root:

```
yourwebsite.com/
├── index.html          (UPDATED - replace your current one)
├── manifest.json       (NEW)
├── service-worker.js   (NEW)
└── icons/              (NEW FOLDER)
    ├── icon-72x72.png
    ├── icon-96x96.png
    ├── icon-128x128.png
    ├── icon-144x144.png
    ├── icon-152x152.png
    ├── icon-192x192.png
    ├── icon-384x384.png
    └── icon-512x512.png
```

**File structure should look like:**
```
public_html/
├── index.html
├── manifest.json
├── service-worker.js
├── privacy.html
├── terms.html
└── icons/
    └── [all icon files here]
```

### Step 3: Test It!

**On iPhone (Safari):**
1. Visit your website
2. Tap the Share button (box with arrow)
3. Scroll down and tap "Add to Home Screen"
4. Tap "Add"
5. App icon appears on home screen! 🎉

**On Android (Chrome):**
1. Visit your website
2. Look for "Install" button in address bar OR
3. Tap menu (3 dots) → "Install app" or "Add to Home Screen"
4. Tap "Install"
5. App icon appears in app drawer! 🎉

---

## Verifying It Works

### Check in Browser Console (F12):

**After uploading, visit your site and check console:**

✅ **You should see:**
```
PWA: Service Worker registered successfully: http://yoursite.com/
```

❌ **If you see errors:**
```
PWA: Service Worker registration failed: [error]
```
→ Make sure `service-worker.js` is in your root directory

### Check manifest.json:

Visit: `yourwebsite.com/manifest.json`

You should see JSON text with your app info. If you get 404, the file isn't uploaded correctly.

---

## How Users Will Install

### iPhone Users:
1. Open Safari (must use Safari, not Chrome!)
2. Visit your website
3. Tap Share → Add to Home Screen
4. Name the app (default: "Flânerie")
5. Tap Add

### Android Users:
1. Open Chrome (recommended)
2. Visit your website
3. Popup appears: "Install Flânerie?"
4. Tap Install
5. Done!

---

## Features You Now Have

✅ **Install to home screen** - Like a real app
✅ **Full screen mode** - No browser UI
✅ **Offline caching** - Basic pages work offline
✅ **App-like experience** - Splash screen, smooth navigation
✅ **Works on iOS and Android**

---

## Optional: Add Install Button to Your Site

Want a prominent "Install App" button on your website?

**Add this HTML anywhere on your homepage:**

```html
<button id="pwa-install-btn" style="display: none; position: fixed; bottom: 20px; right: 20px; background: var(--accent-color); color: white; border: none; padding: 1rem 2rem; border-radius: 50px; font-weight: 600; cursor: pointer; box-shadow: 0 4px 12px rgba(0,0,0,0.3); z-index: 9999;">
    📱 Install App
</button>

<script>
    // Show install button when PWA is installable
    let installPrompt;
    window.addEventListener('beforeinstallprompt', (e) => {
        e.preventDefault();
        installPrompt = e;
        document.getElementById('pwa-install-btn').style.display = 'block';
    });
    
    // Handle install button click
    document.getElementById('pwa-install-btn').addEventListener('click', async () => {
        if (!installPrompt) return;
        installPrompt.prompt();
        const { outcome } = await installPrompt.userChoice;
        if (outcome === 'accepted') {
            document.getElementById('pwa-install-btn').style.display = 'none';
        }
        installPrompt = null;
    });
    
    // Hide button after install
    window.addEventListener('appinstalled', () => {
        document.getElementById('pwa-install-btn').style.display = 'none';
    });
</script>
```

This button:
- Only appears when app is installable
- Triggers the install prompt when clicked
- Hides after installation
- Floats in bottom-right corner

---

## Troubleshooting

### "Install" option doesn't appear

**Checklist:**
- ✅ Website is HTTPS (required for PWA) - works on localhost too
- ✅ manifest.json is accessible at yoursite.com/manifest.json
- ✅ Icons exist at yoursite.com/icons/icon-XXX.png
- ✅ Service worker registered successfully (check console)

### Icons don't show up

**Fix:**
- Make sure icons are uploaded to `/icons/` folder
- Check file names match exactly (icon-72x72.png, etc.)
- Icons must be PNG format
- Try clearing browser cache and revisiting

### Service Worker errors

**Common issues:**
- File path wrong (must be in root: `/service-worker.js`)
- HTTPS required (except localhost)
- Browser cache (hard refresh: Ctrl+Shift+R)

### Works on Android but not iPhone

**iPhone requirements:**
- Must use Safari browser
- Must manually Add to Home Screen (no popup)
- iOS 11.3+ required
- Private browsing won't show option

---

## What Changed in Your Code

**Added to index.html:**
- PWA meta tags (theme color, app name, etc.)
- Link to manifest.json
- Apple touch icons
- Service worker registration script

**Does NOT change:**
- Your existing functionality
- Desktop experience
- Mobile responsive design
- Any of your routes/swarms/events features

**It literally just adds:**
- Ability to install to home screen
- Full-screen mode when installed
- Basic offline caching

---

## Next Steps After Testing

1. **Test on your phone** (both iPhone and Android if possible)
2. **Ask friends to test install**
3. **Promote it:** Add a banner "📱 Install our app!"
4. **Consider App Store version** in 1-2 months for corporate users

---

## Need Help?

**Common questions:**

**Q: Can I delete these files later?**
A: Yes! Just remove manifest.json, service-worker.js, and the PWA script from index.html. Your site will work normally.

**Q: Will this break my website?**
A: No. Desktop users won't notice any difference. It just adds install capability for mobile.

**Q: Do I need app store approval?**
A: No! PWA bypasses app stores entirely.

**Q: Can I update the app later?**
A: Yes! Just upload new files. Users get updates automatically when they visit.

---

## Summary

**Upload these files:**
1. index.html (replace current)
2. manifest.json (new)
3. service-worker.js (new)
4. icons/ folder with 8 PNG files (new)

**Test:**
1. Visit site on phone
2. Add to home screen
3. Open from home screen
4. Should look like a real app!

**That's it!** 🎉

Your website is now a PWA and can be installed like an app, with zero changes to your existing functionality.
