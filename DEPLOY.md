# Deployment Guide

## Free Hosting Options

### Option 1: GitHub Pages (Recommended - Free Forever)

**Step 1: Create GitHub Repository**
1. Go to https://github.com/new
2. Name your repo (e.g., `tawheed-registration`)
3. Make it Public
4. Click "Create repository"

**Step 2: Upload Files**
```bash
# In your registration-checker folder
git init
git add index.html README.md all-tickets.xlsx
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/tawheed-registration.git
git push -u origin main
```

**Step 3: Enable GitHub Pages**
1. Go to your repo on GitHub
2. Click Settings → Pages
3. Under "Source", select "Deploy from a branch"
4. Select "main" branch and "/ (root)" folder
5. Click Save
6. Wait 2-3 minutes for deployment

**Your URL:** `https://YOUR_USERNAME.github.io/tawheed-registration/`

---

### Option 2: Netlify (Free, Simple Drag & Drop)

**Step 1: Prepare Files**
1. Select these files:
   - `index.html`
   - `all-tickets.xlsx`
   - `README.md` (optional)
2. Zip them into `registration-app.zip`

**Step 2: Deploy**
1. Go to https://www.netlify.com/
2. Sign up (free) with email or GitHub
3. Drag and drop your ZIP file onto the dashboard
4. Netlify automatically deploys and gives you a URL

**Your URL:** `https://random-name-123.netlify.app`

**To Update:** Just drag a new ZIP file

---

### Option 3: Vercel (Free, Good Performance)

**Step 1: Install Vercel CLI**
```bash
npm i -g vercel
```

**Step 2: Deploy**
```bash
cd registration-checker
vercel
```

**Or use GitHub:**
1. Push code to GitHub (see Option 1)
2. Go to https://vercel.com/
3. Sign up with GitHub
4. Click "New Project"
5. Import your repository
6. Deploy!

---

### Option 4: 000webhost (Free PHP Hosting)

1. Go to https://www.000webhost.com/
2. Sign up for free account
3. Create new website
4. Go to File Manager
5. Upload `index.html` and `all-tickets.xlsx` to `public_html/` folder
6. Access via: `https://YOUR_SITE.000webhostapp.com`

---

## Post-Deployment Steps

### 1. Update the Excel File

When you have new registration data:

**GitHub Pages:**
```bash
git add all-tickets.xlsx
git commit -m "Update registration data"
git push
```

**Netlify/Vercel:**
- Upload new ZIP file with updated Excel

**000webhost:**
- Use File Manager to replace `all-tickets.xlsx`

### 2. Test the App

1. Open your deployed URL
2. Wait for "✓ Loaded X records" message
3. Search for a donor name
4. Verify ticket counts display correctly

### 3. Share the Link

Send this URL to your check-in volunteers:
```
https://your-deployment-url.com
```

---

## Files Required for Deployment

Only these 2 files are needed:

```
registration-checker/
├── index.html          # The web application (REQUIRED)
├── all-tickets.xlsx    # Your data file (REQUIRED)
└── README.md           # Instructions (optional)
```

**Do NOT upload:**
- Python scripts (`check_*.py`)
- Test files (`debug.html`, `test-*.html`)
- Fix scripts (`fix.py`)
- Old versions of files

---

## Troubleshooting

### "File not found" Error

**Problem:** `all-tickets.xlsx` is not accessible

**Solutions:**
1. Ensure file is uploaded to same folder as `index.html`
2. Check filename is exactly `all-tickets.xlsx` (case-sensitive)
3. On some hosts, Excel files may need special MIME type

**For Apache (.htaccess):**
Create `.htaccess` file with:
```
AddType application/vnd.openxmlformats-officedocument.spreadsheetml.sheet .xlsx
```

### Excel File Won't Download

Some hosts block `.xlsx` files. Try:

1. Rename to `.dat` extension
2. Update `index.html` line:
```javascript
const filename = 'all-tickets.dat';  // Changed from .xlsx
```

### CORS Error

If you see "CORS policy" error, the server needs configuration.

**For Apache (.htaccess):**
```
Header set Access-Control-Allow-Origin "*"
```

**For Nginx:**
Add to server block:
```nginx
location ~* \.(xlsx)$ {
    add_header Access-Control-Allow-Origin *;
}
```

---

## Recommended: GitHub Pages

**Why GitHub Pages?**
- ✅ Completely free
- ✅ Reliable uptime
- ✅ Easy updates (just git push)
- ✅ Custom domain support
- ✅ HTTPS included
- ✅ No ads

**Custom Domain (Optional):**
1. Buy domain from Namecheap/GoDaddy
2. In GitHub repo: Settings → Pages → Custom domain
3. Add CNAME file with your domain
4. Configure DNS records

---

## Need Help?

If deployment fails:
1. Check browser console (F12) for errors
2. Verify `all-tickets.xlsx` is in the same folder as `index.html`
3. Test locally first: `python -m http.server 8080`
4. Try a different hosting option

**Quick Test:**
- Does `https://your-url.com/all-tickets.xlsx` download the file?
- If yes: App should work
- If no: File not deployed correctly
