# AnimalOps 🐾

A free, open-source web application designed specifically for animal rescue organizations to manage rescued animals and their information. Store animal data in Google Sheets and photos in Dropbox - all using your existing cloud storage solutions.

![AnimalOps Logo](https://img.shields.io/badge/AnimalOps-Animal%20Rescue%20Management-4A8F63?style=for-the-badge)

## Features

- 📊 **Google Sheets Integration** - Store all animal records in a spreadsheet for easy viewing, sorting, and analysis
- 📦 **Dropbox Photo Storage** - Upload and organize animal photos with shareable links
- ☁️ **OneDrive Photo Storage** - Alternative option for Microsoft users to store photos
- 🆔 **Unique Animal IDs** - Automatically generated tracking IDs for each rescue
- 🔒 **Privacy-First** - API tokens stored only in your browser session, never on any server
- 📱 **Mobile Friendly** - Works great on phones and tablets for field use
- 💰 **Zero Cost** - Runs entirely on GitHub Pages (free) and your existing cloud storage
- 🔧 **Flexible** - Choose the photo storage provider that works best for your organization

## Why AnimalOps?

Built specifically for nonprofit animal rescue organizations that need a simple, cost-effective way to track rescued animals without expensive specialized software. If you already use Google Sheets and either Dropbox or OneDrive, you can start using AnimalOps immediately at no additional cost.

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

### 5. Start Using AnimalOps

1. Visit your deployed app
2. Enter your Google Sheets Spreadsheet ID and access token
3. Choose either Dropbox or OneDrive and enter your access token for your chosen provider
4. Click "Connect" on both services
5. Start adding animal records!

## How It Works

### Data Flow

```
User Input → AnimalOps (Browser) → Google Sheets (animal data)
                                  ↓
                            Dropbox OR OneDrive (photos)
```

1. **Animal Information** is saved as a row in your Google Sheet with columns for name, species, breed, age, intake date, health notes, and more
2. **Photos** are uploaded to Dropbox in organized folders (one folder per animal ID)
3. **Photo Links** from Dropbox are saved in the Google Sheet for easy reference

### What Gets Stored Where

**Google Sheets (one row per animal):**
- Timestamp
- Animal ID (auto-generated)
- Name, Species, Breed
- Age, Gender
- Intake Date
- Health Notes
- Behavior Notes
- Photo Links (from Dropbox)
- Photo Count

**Dropbox or OneDrive (organized by animal ID):**
```
/AnimalOps/
  ├── A1234567890/
  │   ├── A1234567890_photo_1_IMG_001.jpg
  │   └── A1234567890_photo_2_IMG_002.jpg
  └── A1234567891/
      └── A1234567891_photo_1_IMG_003.jpg
```

## Privacy & Security

- ✅ All API tokens are stored **only in your browser's session storage**
- ✅ Tokens are **cleared when you close the browser tab**
- ✅ **No backend server** - everything runs in your browser
- ✅ API calls go **directly from your browser** to Google/Dropbox
- ✅ Your data never touches any third-party servers

**Important:** Anyone with the API tokens can access your data. Keep them secure and only share with authorized staff.

## Future Enhancements

The application is designed with a modular architecture to easily support additional cloud storage providers:

- [ ] Additional cloud storage providers (Box, AWS S3, etc.)
- [ ] Office 365 / Excel Online integration (as alternative to Google Sheets)
- [ ] Search and filter animals
- [ ] Export reports
- [ ] Medical record tracking
- [ ] Adoption status tracking

## Contributing

We welcome contributions from the community! Whether you're adding new cloud storage providers, improving the UI, or fixing bugs, your help makes AnimalOps better for animal rescues everywhere.

### Adding a New Cloud Storage Provider

1. Add a new configuration section in the HTML (follow the Dropbox/Sheets pattern)
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
A: Free! GitHub Pages hosting is free, and you're using your existing Google and Dropbox accounts.

**Q: What happens if my API token expires?**  
A: Just generate a new one and enter it in the Configuration section. Your data is safe in Google Sheets and Dropbox.

**Q: Can multiple staff members use this?**  
A: Yes! Each person can generate their own tokens and use the app. All data goes to the same Google Sheet and Dropbox account.

**Q: Can I customize the fields?**  
A: Yes! The code is open source. You can modify the form fields and update the Google Sheets columns accordingly.

**Q: Is my data backed up?**  
A: Your data is in Google Sheets and Dropbox, which have their own backup systems. We recommend enabling version history in Google Sheets.

**Q: Can I use this for other types of rescues (wildlife, exotic animals, etc.)?**  
A: Absolutely! The fields are customizable, and the species dropdown includes an "Other" option.

---

**Made for rescues, by supporters of animal welfare. Fork it, improve it, share it! 🐕 🐈 🐰**
