# Tawheed Center Registration Verification System

A web-based application for verifying event registration tickets from Excel files.

## 📁 Files Required

| File | Purpose |
|------|---------|
| `index.html` | Main application file (runs in browser) |
| `all-tickets.xlsx` | Registration data file (Excel format) |

## 🚀 Quick Start

### Option 1: Deploy to Web Server (Recommended)

1. **Upload files** to your web server:
   ```
   /registration-checker/
   ├── index.html
   └── all-tickets.xlsx
   ```

2. **Access the app**:
   ```
   https://yourserver.com/registration-checker/
   ```

3. The app will **auto-load** the data and show a progress bar.

### Option 2: Local Testing

```bash
cd registration-checker

# Python 3
python -m http.server 8000

# OR Node.js
npx serve .

# OR PHP
php -S localhost:8000
```

Then open: `http://localhost:8000`

## 📊 Data File Format

Your Excel file should have these columns:

| Column | Required | Description |
|--------|----------|-------------|
| **Donor** | ✅ Yes | Person's full name |
| **Ticket Type** | ✅ Yes | e.g., "Adult (10+ Years)", "Child(5-10 Years)" |
| **Ticket Fee** | ✅ Yes | Price per ticket (for total calculation) |
| **Phone Number** | ❌ No | Contact number |
| **Email Address** | ❌ No | Email (shown in results) |
| **Reference** | ❌ No | Ticket reference numbers (e.g., SR-060835) |

### Example Data Structure:

```
| Reference | Donor | Phone Number | Email Address | Ticket Type | Ticket Fee |
|-----------|-------|--------------|---------------|-------------|------------|
| SR-060835 | John Doe | (248) 555-1234 | john@email.com | Adult (10+ Years) | 30 |
|           | John Doe |              |               | Adult (10+ Years) | 30 |
| SR-061177 | John Doe | (248) 555-1234 | john@email.com | Adult (10+ Years) | 30 |
```

**Note:** The app handles merged cells automatically (common in Excel exports).

## 🔄 File Naming

The app tries these filenames in order:

1. `all-tickets.xlsx` ← **Recommended**
2. `All Tickets.xlsx`
3. `tickets.xlsx`
4. `data.xlsx`
5. `registrations.xlsx`

**To use a specific file:** Rename it to `all-tickets.xlsx`

## 🖥️ How to Use

1. **Load Data** (automatic on page open)
   - Progress bar shows loading status
   - Wait for "✓ Loaded X records" message

2. **Search**
   - Type a donor name in the search box
   - Results appear instantly

3. **View Results**
   - Total tickets count
   - Adults/Children breakdown
   - Total amount ($)
   - Contact information

4. **Refresh Data**
   - Click "🔄 Refresh Data" button to reload the file
   - Useful after updating the Excel file

## 📱 Mobile Support

The app works on all devices:
- ✅ Desktop (Chrome, Firefox, Safari, Edge)
- ✅ Tablets
- ✅ Mobile phones

## 🐛 Troubleshooting

### "No data file found" Error

**Problem:** The app can't find the Excel file.

**Solution:**
1. Ensure `all-tickets.xlsx` is in the **same folder** as `index.html`
2. Check the filename is exactly `all-tickets.xlsx` (case-sensitive on Linux servers)
3. Verify the file extension is `.xlsx` (not `.xls` or `.csv`)

### "Could not find Donor column" Error

**Problem:** The Excel file doesn't have a "Donor" column.

**Solution:**
1. Open the Excel file
2. Ensure the first row has a column named exactly "Donor"
3. Save and re-upload

### Slow Loading

**Expected times:**
- 100 rows: ~1 second
- 1,000 rows: ~3 seconds
- 10,000 rows: ~10 seconds

**If slower:**
1. Check your internet connection (for remote servers)
2. Try a different browser (Chrome/Firefox recommended)
3. Reduce file size by removing unnecessary columns

### Browser Console Errors

**To check errors:**
1. Press `F12` (or `Ctrl+Shift+J` on Chrome)
2. Click the "Console" tab
3. Look for red error messages
4. Screenshot and report if needed

## 🔒 Security Notes

- The app runs entirely in the user's browser
- No data is sent to external servers
- Excel file must be publicly accessible (for auto-load)
- Consider password-protecting the folder if data is sensitive

## 📝 Updating Data

To update registration data:

1. **Replace the Excel file** on the server with the new version
2. **Keep the same filename** (`all-tickets.xlsx`)
3. **Click "Refresh Data"** button in the app
4. **Or refresh the page** (F5)

## 🎨 Customization

### Change Default Filename

Edit `index.html`, find this line:
```javascript
const DEFAULT_DATA_FILE = 'all-tickets.xlsx';
```

Change to your preferred filename.

### Change Event Name

Edit `index.html`, find this line:
```html
<p>Annual Ramadan Fundraiser 2026 - Registration Verification</p>
```

### Change Colors

Edit the CSS section in `index.html`:
```css
/* Header gradient */
.header { background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%); }

/* Success color */
.result-card.found { border-left-color: #28a745; }
```

## 💾 Browser Storage

The app temporarily stores data in browser memory (not localStorage) for:
- Faster searches
- Smoother scrolling

Data is cleared when the page is closed.

## 📞 Support

If you encounter issues:
1. Check the browser console (F12)
2. Verify file format matches examples above
3. Test with a small sample file first

---

**Version:** 1.0
**Last Updated:** February 2026
**Requirements:** Modern web browser, Excel file with registration data
