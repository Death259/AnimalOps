<div align="center">
  <img src="animalops-logo.png" alt="AnimalOps Logo" width="400">
</div>

# AnimalOps 🐾

A free, open-source web application designed specifically for animal rescue organizations to manage rescued animals and their information. Store animal data in Google Sheets and photos in your choice of cloud storage - all using your existing cloud solutions.

![AnimalOps Logo](https://img.shields.io/badge/AnimalOps-Animal%20Rescue%20Management-4A8F63?style=for-the-badge)

## Features

### Data Management
- 📊 **Google Sheets Integration** - Store all animal records in a spreadsheet for easy viewing, sorting, and analysis
- 🔍 **View & Edit Records** - Browse all animals, search by name/ID/species, and edit existing records
- 🖨️ **Print Function** - Generate printable packets with cover pages showing all animal info plus one page per photo
- 🆔 **Dual ID System** - User-defined Animal IDs for organization plus auto-generated internal tracking IDs

### Photo Management
- 📸 **Multiple Storage Options** - Choose between Dropbox, OneDrive, or Google Drive for photo storage
- 📷 **Camera Integration** - Take photos directly with your device camera (laptop webcam, iPad, or iPhone)
- 📁 **File Upload** - Upload existing photos from your device
- 🗂️ **Organized by Animal ID** - Photos automatically organized into folders by your Animal ID

### Animal Information Fields
- **Required Fields:**
  - Animal Name
  - Species (Dog, Cat, Rabbit, Bird, Reptile, Other)
  - Gender (Male, Female, Neutered Male, Spayed Female, Unknown)
  - Intake Date
  - Animal ID (your custom identifier)
  - Building ID (kennel/location)
  - Color
  - Body Condition Score
- **Optional Fields:**
  - Breed
  - Age/Age Estimate
  - Health Notes
  - Behavior Notes
  - Multiple Photos

### Technical Features
- 🔒 **Privacy-First** - API tokens stored only in your browser session, never on any server
- 📱 **Mobile Friendly** - Works great on phones and tablets for field use
- 💰 **Zero Cost** - Runs entirely on GitHub Pages (free) and your existing cloud storage
- 🔧 **Flexible** - Choose the photo storage provider that works best for your organization

## Why AnimalOps?

Built specifically for nonprofit animal rescue organizations that need a simple, cost-effective way to track rescued animals without expensive specialized software. If you already use Google Sheets and Dropbox, OneDrive, or Google Drive, you can start using AnimalOps immediately at no additional cost.

## Quick Start

### 1. Deploy to GitHub Pages

1. Fork or clone this repository
2. Go to your repository Settings → Pages
3. Select your branch (usually `main`) and save
4. Your app will be live at `https://yourusername.github.io/animalops`

### 2. Set Up Google Sheets

**Create a Spreadsheet:**
1. Create a new Google Sheet
2. Copy the Spreadsheet ID from the URL: `docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`

**Get an API Token:**
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project (e.g., "AnimalOps")
3. Enable the Google Sheets API
4. Create OAuth 2.0 credentials (Web application type)
5. Add `https://developers.google.com/oauthplayground` as an authorized redirect URI
6. Go to [OAuth 2.0 Playground](https://developers.google.com/oauthplayground)
7. Use your credentials and authorize `https://www.googleapis.com/auth/spreadsheets`
8. Exchange authorization code for tokens
9. Copy the Access Token

**Note:** Google Sheets access tokens expire after ~1 hour. The app will prompt you to enter a new one when needed.

### 3. Set Up Dropbox (Option 1 for Photo Storage)

**Create an App:**
1. Go to [Dropbox App Console](https://www.dropbox.com/developers/apps)
2. Click "Create app"
3. Choose "Scoped access" and "Full Dropbox" (or App folder)
4. Name your app (e.g., "AnimalOps")

**Set Permissions:**
1. Go to Permissions tab
2. Enable: `files.metadata.write`, `files.content.write`, `files.content.read`, `sharing.write`
3. Submit changes

**Generate Token:**
1. Go to Settings tab
2. Scroll to "OAuth 2" section
3. Click "Generate" under "Generated access token"
4. Copy the token (starts with "sl...")

**Note:** Dropbox tokens don't expire, but keep them secure!

### 4. Set Up OneDrive (Option 2 for Photo Storage)

**Register an Application:**
1. Go to [Azure Portal - App Registrations](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)
2. Click "New registration"
3. Name: "AnimalOps"
4. Supported account types: "Accounts in any organizational directory and personal Microsoft accounts"
5. Redirect URI: Select "Web" and enter `https://login.microsoftonline.com/common/oauth2/nativeclient`
6. Click "Register"

**Configure API Permissions:**
1. Go to "API permissions"
2. Click "Add a permission" → "Microsoft Graph" → "Delegated permissions"
3. Add: `Files.ReadWrite`, `Files.ReadWrite.All`, `User.Read`
4. Click "Add permissions"

**Enable Public Client Flow:**
1. Go to "Authentication"
2. Scroll to "Advanced settings"
3. Enable "Allow public client flows" → Yes
4. Click "Save"

**Get Access Token via Graph Explorer:**
1. Go to [Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
2. Sign in with your Microsoft account
3. Click "Modify permissions" (consent to required permissions)
4. Make any test query (e.g., GET /me)
5. Click "Access token" tab to view your token
6. Copy the token (starts with "EwB..." or similar)

**Note:** Microsoft Graph access tokens expire after ~1 hour. The app will prompt you to enter a new one when needed.

### 5. Set Up Google Drive (Option 3 for Photo Storage)

**Use Same Google Cloud Project:**
1. If you already created a project for Google Sheets, use that same project
2. Otherwise, go to [Google Cloud Console](https://console.cloud.google.com) and create a new project

**Enable Google Drive API:**
1. In your project, go to "APIs & Services" → "Library"
2. Search for "Google Drive API" and click "Enable"

**Use Existing OAuth Credentials:**
1. If you created credentials for Google Sheets, you can use the same ones
2. Go to "APIs & Services" → "Credentials"
3. You should see your existing OAuth 2.0 Client ID

**Get Access Token via OAuth Playground:**
1. Go to [OAuth 2.0 Playground](https://developers.google.com/oauthplayground)
2. Click the settings gear icon (top right)
3. Check "Use your own OAuth credentials"
4. Enter your Client ID and Client Secret
5. In Step 1, select "Drive API v3" → `https://www.googleapis.com/auth/drive.file`
6. Click "Authorize APIs" and sign in
7. In Step 2, click "Exchange authorization code for tokens"
8. Copy the **Access token** (starts with "ya29...")

**Note:** Google Drive access tokens expire after ~1 hour, just like Google Sheets tokens.

**Tip:** Using Google Drive with Google Sheets means everything stays in one Google ecosystem - perfect for organizations already using Google Workspace!

### 6. Start Using AnimalOps

1. Visit your deployed app
2. Enter your Google Sheets Spreadsheet ID and access token
3. Choose Dropbox, OneDrive, or Google Drive and enter your access token for your chosen provider
4. Click "Connect" on both services
5. Start adding animal records!

## How It Works

### Data Flow

```
User Input → AnimalOps (Browser) → Google Sheets (animal data)
                                  ↓
                    Dropbox OR OneDrive OR Google Drive (photos)
```

1. **Animal Information** is saved as a row in your Google Sheet with columns for all animal details
2. **Photos** are uploaded to your chosen cloud storage provider in organized folders (one folder per Animal ID)
3. **Photo Links** from your cloud storage are saved in the Google Sheet for easy reference

### What Gets Stored Where

**Google Sheets (one row per animal):**
- Timestamp
- Internal ID (auto-generated)
- Name, Species, Breed
- Age, Gender
- Intake Date
- Animal ID (your custom ID)
- Building ID
- Color
- Body Condition Score
- Health Notes
- Behavior Notes
- Photo Links
- Photo Count

**Dropbox, OneDrive, or Google Drive (organized by Animal ID):**
```
/AnimalOps/
  ├── DOG-2024-001/
  │   ├── DOG-2024-001_photo_1_IMG_001.jpg
  │   └── DOG-2024-001_photo_2_IMG_002.jpg
  └── CAT-2024-005/
      └── CAT-2024-005_photo_1_IMG_003.jpg
```

## Using AnimalOps

### Adding Animals

1. Click "Add New Animal" from the main screen
2. Fill in all required fields (marked with *)
3. Take photos with your device camera or upload existing photos
4. Click "Save Animal Record"
5. The app will save data to Google Sheets and upload photos to your cloud storage

### Viewing & Editing Records

1. Click "View Records" from the main form
2. Click "Refresh Records" to load all animals from Google Sheets
3. Use the search box to filter by name, species, Animal ID, breed, or building
4. Click "Edit" on any record to modify it
5. Make your changes and click "Update Animal Record"

### Printing Records

1. Go to "View Records" and load your animals
2. Click "Print All" button
3. The app will:
   - Fetch all photos from cloud storage
   - Generate a cover page for each animal with all their information
   - Create one page per photo showing the image and animal details
   - Open your browser's print dialog
4. Print to a printer or save as PDF

### Taking Photos

1. In the Add Animal form, click "Take Photo"
2. Allow camera access when prompted
3. The app will use your device's camera (back camera on mobile devices)
4. Click "Capture Photo" to take the picture
5. Take as many photos as needed
6. You can also click "Upload Photos" to select existing photos from your device

## Privacy & Security

- ✅ All API tokens are stored **only in your browser's session storage**
- ✅ Tokens are **cleared when you close the browser tab**
- ✅ **No backend server** - everything runs in your browser
- ✅ API calls go **directly from your browser** to Google/Dropbox/OneDrive/Google Drive
- ✅ Your data never touches any third-party servers

**Important:** Anyone with the API tokens can access your data. Keep them secure and only share with authorized staff.

## Contributing

We welcome contributions from the community! Whether you're adding new cloud storage providers, improving the UI, or fixing bugs, your help makes AnimalOps better for animal rescues everywhere.

### Adding a New Cloud Storage Provider

1. Add a new configuration section in the HTML (follow the Dropbox/OneDrive/Google Drive pattern)
2. Implement connection test function (`connect[Provider]()`)
3. Implement upload function for your provider
4. Update the form submission handler to use the new provider
5. Add help documentation for obtaining API tokens
6. Submit a pull request!

### Development Setup

No build process needed! Just:
1. Clone the repository
2. Open `animalops.html` in your browser
3. Make changes and test locally
4. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- 🐛 **Bug Reports:** Open an issue on GitHub
- 💡 **Feature Requests:** Open an issue with the "enhancement" label
- 📖 **Documentation:** Check the built-in help system (? button in the app)
- 🤝 **Community:** Share your success stories and help other rescues!

## Acknowledgments

Built with ❤️ for animal rescue organizations worldwide. Every animal deserves a chance, and every rescue deserves great tools.

## FAQ

**Q: Do I need to know how to code?**  
A: No! Just follow the setup instructions to get your API tokens, and you're ready to go.

**Q: How much does this cost?**  
A: Free! GitHub Pages hosting is free, and you're using your existing Google and Dropbox/OneDrive/Google Drive accounts.

**Q: What happens if my API token expires?**  
A: Just generate a new one and enter it in the Configuration section. Your data is safe in Google Sheets and your cloud storage.

**Q: Can multiple staff members use this?**  
A: Yes! Each person can generate their own tokens and use the app. All data goes to the same Google Sheet and cloud storage account.

**Q: Can I customize the fields?**  
A: Yes! The code is open source. You can modify the form fields and update the Google Sheets columns accordingly.

**Q: Is my data backed up?**  
A: Your data is in Google Sheets and your chosen cloud storage, which have their own backup systems. We recommend enabling version history in Google Sheets.

**Q: Can I use this for other types of rescues (wildlife, exotic animals, etc.)?**  
A: Absolutely! The fields are customizable, and the species dropdown includes an "Other" option.

**Q: Can I take photos directly in the app?**  
A: Yes! Click "Take Photo" to use your device's camera (laptop webcam, iPad, or iPhone camera). You can take as many photos as needed.

**Q: Can I print animal records?**  
A: Yes! Go to "View Records" and click "Print All" to generate printable packets with cover pages and photos for each animal.

**Q: How are photos organized?**  
A: Photos are automatically organized into folders by your Animal ID (e.g., DOG-2024-001, CAT-2024-005) in your cloud storage.

---

**Made for rescues, by supporters of animal welfare. Fork it, improve it, share it! 🐕 🐈 🐰**
