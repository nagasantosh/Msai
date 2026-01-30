# Mother Sai Construction Technologies Website

A modern, responsive website built with HTML, CSS, and JavaScript for Mother Sai Construction Technologies.

## 🌟 Features

- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- **Modern UI**: Bold Contemporary theme with vibrant colors and dynamic layouts
- **6 Pages**: Home, About, Services, Products, Projects, Contact
- **SEO Friendly**: Optimized meta tags and semantic HTML
- **Fast Loading**: Optimized images and efficient code
- **Contact Form**: Ready for Google Sheets integration

## 📁 Project Structure

```
mothersai-website/
├── index.html              # Home page
├── about.html              # About page
├── services.html           # Services page
├── products.html           # Products (Graphene) page
├── projects.html           # Projects portfolio page
├── contact.html            # Contact page with form
├── assets/
│   ├── css/
│   │   └── style.css      # Main stylesheet
│   ├── js/
│   │   └── main.js        # Main JavaScript file
│   └── images/            # Images folder (add your images here)
└── README.md              # This file
```

## 🚀 Deployment to GitHub Pages

### Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the "+" icon in the top right and select "New repository"
3. Name it: `mothersai-website` (or any name you prefer)
4. Make it **Public**
5. Don't initialize with README (we already have one)
6. Click "Create repository"

### Step 2: Upload Files

**Option A: Using GitHub Web Interface**
1. On your repository page, click "uploading an existing file"
2. Drag and drop all files and folders
3. Add commit message: "Initial website upload"
4. Click "Commit changes"

**Option B: Using Git Command Line**
```bash
cd mothersai-website
git init
git add .
git commit -m "Initial website upload"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mothersai-website.git
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on "Settings" tab
3. Scroll down to "Pages" in the left sidebar
4. Under "Source", select "main" branch
5. Click "Save"
6. Your site will be published at: `https://YOUR_USERNAME.github.io/mothersai-website/`

**Note**: It may take a few minutes for the site to go live.

## 📧 Google Sheets Integration for Contact Form

### Step 1: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "Mother Sai Contact Form Submissions"
4. Add these column headers in Row 1:
   - A1: Timestamp
   - B1: First Name
   - C1: Last Name
   - D1: Email
   - E1: Phone
   - F1: Company
   - G1: Service of Interest
   - H1: Project Type
   - I1: Location
   - J1: Message

### Step 2: Create Google Apps Script

1. In your Google Sheet, go to **Extensions** > **Apps Script**
2. Delete any existing code
3. Paste the following code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // Append row with form data
    sheet.appendRow([
      new Date(),
      data.firstName,
      data.lastName,
      data.email,
      data.phone,
      data.company,
      data.serviceInterest,
      data.projectType,
      data.location,
      data.message
    ]);
    
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'success'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'error',
      'error': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click "Save" (disk icon)
5. Name the project: "Contact Form Handler"

### Step 3: Deploy Apps Script

1. Click **Deploy** > **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Fill in the details:
   - Description: "Contact Form Submission Handler"
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Click **Deploy**
6. Review permissions and click **Authorize access**
7. Choose your Google account
8. Click **Advanced** > **Go to Contact Form Handler (unsafe)**
9. Click **Allow**
10. **Copy the Web App URL** (it should look like: `https://script.google.com/macros/s/...`)

### Step 4: Update Contact Form

1. Open `contact.html` in a text editor
2. Find the comment: `/* GOOGLE SHEETS INTEGRATION INSTRUCTIONS */`
3. Uncomment the fetch code and replace `YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL` with the URL you copied
4. The code should look like this:

```javascript
fetch('https://script.google.com/macros/s/YOUR_ACTUAL_URL_HERE/exec', {
    method: 'POST',
    mode: 'no-cors',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(data)
})
.then(() => {
    document.getElementById('successMessage').style.display = 'block';
    this.reset();
})
.catch(error => {
    console.error('Error:', error);
    alert('There was an error sending your message. Please try again or email us directly.');
});
```

5. Save the file and re-upload to GitHub

### Testing the Form

1. Visit your website's contact page
2. Fill out the form completely
3. Click "Send Message"
4. Check your Google Sheet - a new row should appear with the submission data!

## 🖼️ Adding Your Images

The website currently uses placeholder images from Unsplash. To add your own images:

1. Place your images in the `assets/images/` folder
2. Update image sources in HTML files:
   - Replace `https://images.unsplash.com/...` with `assets/images/your-image.jpg`
3. Recommended images needed:
   - Hero/banner images for each page
   - RMC plant/concrete production photos
   - Plumbing installation photos
   - Firefighting system photos
   - Graphene/technology images
   - Project photos
   - Team photo for Vikram Akoju
   - Client logos (optional - currently using placeholders)

### Image Optimization Tips

- **Format**: Use JPG for photos, PNG for logos with transparency
- **Size**: Maximum 1920px width for hero images, 800px for content images
- **Compression**: Use tools like TinyPNG or Squoosh to reduce file size
- **File naming**: Use descriptive names like `rmc-plant-production.jpg`

## 🎨 Customization

### Colors

The website uses CSS variables. To change colors, edit `assets/css/style.css`:

```css
:root {
    --primary: #FF6B35;      /* Orange */
    --secondary: #004E89;    /* Blue */
    --accent: #F7B801;       /* Yellow */
    --text: #1a1a1a;         /* Dark gray */
    --light: #fafafa;        /* Light background */
}
```

### Fonts

Current fonts are loaded from Google Fonts:
- **Crimson Pro** (headings)
- **DM Sans** (body text)

To change fonts, update the Google Fonts link in each HTML file's `<head>`.

## 📱 Responsive Breakpoints

- **Desktop**: > 1024px
- **Tablet**: 768px - 1024px
- **Mobile**: < 768px

## 🔧 Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## 📞 Support

For questions or issues:
- Email: vikram@mothersaigroup.com

## 📝 License

© 2026 Mother Sai Construction Technologies. All rights reserved.

---

## Quick Checklist Before Going Live

- [ ] Replace all placeholder images with actual photos
- [ ] Update team photo for Vikram Akoju
- [ ] Set up Google Sheets integration for contact form
- [ ] Test contact form submission
- [ ] Verify all links work correctly
- [ ] Test on mobile devices
- [ ] Review all content for accuracy
- [ ] Add Google Analytics (optional)
- [ ] Set up custom domain (optional)
- [ ] Add favicon (optional)

---

**Built with ❤️ for Mother Sai Construction Technologies**
