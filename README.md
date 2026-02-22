# Tawheed Center Registration Verification App

A client-side web application for verifying event registration tickets from Excel files.

## Features

- ✅ **Auto-loads Excel file** - No manual upload needed
- ✅ **Progress bar** - Visual feedback during loading
- ✅ **Smart donor search** - Case-insensitive partial matching
- ✅ **Merged cell handling** - Automatically fills down donor names
- ✅ **Ticket summary** - Shows ticket count and total amount
- ✅ **Compact layout** - All info visible without scrolling
- ✅ **Works offline** - After initial page load

### Current Status

⚠️ **Note:** The current Excel file format does not include a "Ticket Type" column needed for Adult/Child breakdown. This feature will be added in a future update. The app currently shows total ticket count and amount.

## File Structure

```
registration-checker/
├── index.html          # Main application file
├── all-tickets.xlsx    # Your data file (Excel)
└── README.md           # This file
```

## Quick Start

### Step 1: Prepare Your Files

1. **Rename your Excel file** to `all-tickets.xlsx`
2. **Ensure column headers** include:
   - `Donor` (required)
   - `Ticket Type` (for Adult/Child breakdown)
   - `Ticket Fee` (for total amount calculation)
   - `Reference` (optional, for ticket numbers)

### Step 2: Deploy

Upload both files to your web server in the same folder:

```
/public_html/
    └── registration-checker/
        ├── index.html
        └── all-tickets.xlsx
```

### Step 3: Access

Open your browser and visit:

```
https://yourdomain.com/registration-checker/
```

The app will automatically:
1. Load the Excel file
2. Show a progress bar
3. Display "✓ Loaded X records from all-tickets.xlsx"
4. Enable the search box

## How to Use

### Searching
1. **Type a donor name** in the search box (minimum 2 characters)
2. **Results appear instantly** showing:
   - Total number of tickets
   - Breakdown: Adults 👤 / Children 👶 / Other 🎫
   - Total amount paid
   - Donor details (Phone, Email, etc.)

### Refreshing Data
To load a new version of the Excel file:
1. Replace `all-tickets.xlsx` on the server
2. Click the **🔄 Refresh Data** button
3. Or refresh the browser page

## Data File Format

### Expected Excel Columns

| Column | Required | Description |
|--------|----------|-------------|
| Donor | ✅ Yes | Donor full name |
| Ticket Type | ❌ No | "Adult (10+ Years)" or "Child (5-10 Years)" - currently not in data |
| Ticket Fee | ❌ No | Ticket price (for total calculation) |
| Reference | ❌ No | Ticket reference number (e.g., SR-12345) |
| Phone Number | ❌ No | Contact phone |
| Email Address | ❌ No | Contact email |
| Event Title | ❌ No | Event name |

### Example Data Structure

```
Reference   | Donor                     | Phone Number   | Ticket Type       | Ticket Fee
-----------|---------------------------|----------------|-------------------|------------
SR-060835  | ABBAS SHARIFF ABDULMAJEED | (248) 790-5441 | Adult (10+ Years) | 30
           | ABBAS SHARIFF ABDULMAJEED |                | Adult (10+ Years) | 30
SR-061177  | ABBAS SHARIFF ABDULMAJEED | (248) 790-5441 | Adult (10+ Years) | 30
```

**Note**: The app handles merged cells (empty donor names) by filling down from the last known donor.

## Troubleshooting

### "File not found" Error
- Ensure `all-tickets.xlsx` is in the same folder as `index.html`
- Check that the filename is exactly `all-tickets.xlsx` (case-sensitive on some servers)
- Try accessing the file directly: `https://yourdomain.com/registration-checker/all-tickets.xlsx`

### "Could not find Donor column" Error
- Open your Excel file
- Ensure the first row has a column named exactly `Donor`
- No extra spaces before/after the name

### App Takes Too Long to Load
- Check your internet connection
- The file should load in 1-3 seconds
- If using a slow server, consider upgrading hosting

### Search Not Working
- Wait for the file to fully load (progress bar reaches 100%)
- Type at least 2 characters
- Try refreshing the page

## Browser Compatibility

Works on all modern browsers:
- ✅ Chrome 60+
- ✅ Firefox 60+
- ✅ Safari 14+
- ✅ Edge 79+

## Local Testing (Development)

To test locally before deploying:

### Option 1: Python
```bash
cd registration-checker
python -m http.server 8000
# Open http://localhost:8000
```

### Option 2: Node.js
```bash
cd registration-checker
npx serve
# Open http://localhost:3000
```

### Option 3: VS Code
- Install "Live Server" extension
- Right-click `index.html` → "Open with Live Server"

**Note**: You cannot open `index.html` directly by double-clicking - you need a local server.

## Updating the Application

### Change Default Filename
Edit `index.html` and find:
```javascript
const DEFAULT_DATA_FILE = 'all-tickets.xlsx';
```

Change to your preferred filename, e.g.:
```javascript
const DEFAULT_DATA_FILE = 'january-dinner.xlsx';
```

### Change Event Name
Edit the header text in `index.html`:
```html
<h1>Tawheed Center</h1>
<p>Annual Ramadan Fundraiser 2026 - Registration Verification</p>
```

## Security Notes

- All data processing happens in the browser
- No data is sent to any external server
- Excel file must be in the same domain (CORS policy)
- For production, consider adding authentication

## Support

If you encounter issues:
1. Check the browser console (F12 → Console tab) for error messages
2. Verify your Excel file format matches the expected structure
3. Ensure your web server is configured to serve `.xlsx` files

## License

Free to use for Tawheed Center events.
