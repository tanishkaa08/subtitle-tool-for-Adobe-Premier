# Mac Installation Guide - Subtitle Tool for Adobe Premiere Pro

## 📱 Quick Installation Steps for Mac

### Step 1: Enable CEP Extensions

Before installing, you need to enable unsigned extensions in Adobe Premiere Pro:

1. Open **Terminal** (Applications → Utilities → Terminal)

2. Run one of these commands depending on your Premiere Pro version:

   ```bash
   # For Premiere Pro 2023 (CEP 12)
   defaults write com.adobe.CSXS.12 PlayerDebugMode 1
   
   # For Premiere Pro 2022 (CEP 11)
   defaults write com.adobe.CSXS.11 PlayerDebugMode 1
   
   # For Premiere Pro 2021 (CEP 10)
   defaults write com.adobe.CSXS.10 PlayerDebugMode 1
   
   # For older versions (CEP 9)
   defaults write com.adobe.CSXS.9 PlayerDebugMode 1
   ```

3. **Important**: You only need to run ONE of these commands based on your Premiere Pro version.

### Step 2: Find Your Extensions Folder

You have two options:

**Option A - System-wide installation** (recommended):
```bash
/Library/Application Support/Adobe/CEP/extensions/
```

**Option B - User-specific installation**:
```bash
~/Library/Application Support/Adobe/CEP/extensions/
```

**Tip**: To access these folders in Finder:
1. Open Finder
2. Press **Cmd + Shift + G**
3. Paste the path above
4. Click **Go**

### Step 3: Copy the Extension

1. Download or clone this repository
2. Find the `subtitle-tool-for-Adobe-Premier` folder
3. Copy the entire folder to your chosen extensions directory
4. The final path should look like:
   ```
   /Library/Application Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier/
   ```

### Step 4: Set Permissions

Open Terminal and run:

```bash
# For system-wide installation
sudo chmod -R 755 "/Library/Application Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier"

# For user-specific installation
chmod -R 755 ~/Library/Application\ Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier
```

### Step 5: Restart Premiere Pro

1. Quit Adobe Premiere Pro completely (Cmd + Q)
2. Relaunch Adobe Premiere Pro
3. Go to **Window → Extensions → Subtitle Tool**

## 🔧 Troubleshooting Mac Installation

### Extension Not Appearing

**Check 1**: Verify Debug Mode is Enabled
```bash
# Check if debug mode is set
defaults read com.adobe.CSXS.12 PlayerDebugMode
# Should return: 1
```

**Check 2**: Verify Folder Structure
```bash
# List the extension folder
ls -la "/Library/Application Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier/"
# You should see: index.html, main.js, CSXS folder, jsx folder, etc.
```

**Check 3**: Check Permissions
```bash
# View permissions
ls -la "/Library/Application Support/Adobe/CEP/extensions/"
# The subtitle tool folder should be readable (r) and executable (x)
```

### "Library" Folder is Hidden

To show hidden folders in Finder:
```bash
# Temporarily show hidden files
defaults write com.apple.finder AppleShowAllFiles YES
killall Finder

# To hide them again later
defaults write com.apple.finder AppleShowAllFiles NO
killall Finder
```

Or use this shortcut in Finder: **Cmd + Shift + . (period)**

### Extension Shows But Doesn't Work

**Grant File Access Permissions**:
1. Open **System Preferences**
2. Go to **Security & Privacy**
3. Click **Privacy** tab
4. Select **Files and Folders** or **Full Disk Access**
5. Find **Adobe Premiere Pro** and enable access

### CEP Version Mismatch

To find your CEP version:
1. Open Premiere Pro
2. Go to **Help → About Premiere Pro**
3. Note your Premiere Pro version:
   - 2024: CEP 12
   - 2023: CEP 12
   - 2022: CEP 11
   - 2021: CEP 10
   - 2020: CEP 9

## 🧪 Testing the Installation

After installation, test these features:

1. **Open the Extension**:
   - Window → Extensions → Subtitle Tool
   - Extension panel should appear

2. **Test File Selection**:
   - Create a new project
   - Try selecting a text file
   - File picker dialog should appear

3. **Test Basic Functionality**:
   - Select Feature 1: Static Subtitles
   - Click "Select Text File"
   - Choose any .txt file
   - File name should display in the UI

## 📋 Mac-Specific Notes

### File Paths
- Mac uses forward slashes (`/`) in file paths
- Windows uses backslashes (`\`)
- This extension automatically handles both!

### File Selection Dialog
- The native Mac file picker will be used
- You can navigate with keyboard shortcuts:
  - **Cmd + Shift + G**: Go to folder
  - **Cmd + Up**: Go to parent folder
  - **Cmd + Down**: Open selected folder

### Keyboard Shortcuts
All standard Mac shortcuts work:
- **Cmd + C**: Copy
- **Cmd + V**: Paste
- **Cmd + Z**: Undo
- **Cmd + Option + I**: Open DevTools (for debugging)

## 🔍 Viewing Debug Logs

### Method 1: Console.app
1. Open **Console.app** (Applications → Utilities → Console)
2. In the search bar, type: `CSXS` or `Premiere`
3. Look for extension-related messages

### Method 2: Chrome DevTools
1. With the extension panel open in Premiere Pro
2. Press **Cmd + Option + I**
3. DevTools will open
4. Check the **Console** tab for JavaScript errors

### Method 3: Log Files
```bash
# View CEP logs
cat ~/Library/Logs/CSXS/*.log

# Or open in TextEdit
open ~/Library/Logs/CSXS/
```

## 🎯 Quick Command Reference

```bash
# Enable debug mode
defaults write com.adobe.CSXS.12 PlayerDebugMode 1

# Create extensions folder if it doesn't exist
mkdir -p ~/Library/Application\ Support/Adobe/CEP/extensions/

# Copy extension (adjust source path as needed)
cp -R ~/Downloads/subtitle-tool-for-Adobe-Premier ~/Library/Application\ Support/Adobe/CEP/extensions/

# Set permissions
chmod -R 755 ~/Library/Application\ Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier

# Open extensions folder in Finder
open ~/Library/Application\ Support/Adobe/CEP/extensions/

# Check if extension is there
ls -la ~/Library/Application\ Support/Adobe/CEP/extensions/subtitle-tool-for-Adobe-Premier
```

## 🚨 Common Mac Issues

### Issue: "Library folder doesn't exist"
**Solution**:
```bash
# Create the folder structure
mkdir -p ~/Library/Application\ Support/Adobe/CEP/extensions/
```

### Issue: "Permission denied"
**Solution**:
```bash
# Use sudo for system-wide installation
sudo cp -R subtitle-tool-for-Adobe-Premier /Library/Application\ Support/Adobe/CEP/extensions/

# Or use user folder without sudo
cp -R subtitle-tool-for-Adobe-Premier ~/Library/Application\ Support/Adobe/CEP/extensions/
```

### Issue: "Extension not loading after restart"
**Solutions**:
1. Verify CEP version matches (see CEP Version section above)
2. Check folder name is exactly `subtitle-tool-for-Adobe-Premier`
3. Ensure all files copied correctly (should have index.html, etc.)
4. Try system-wide installation if user-specific didn't work

### Issue: "File picker shows but files won't select"
**Solution**: Grant Premiere Pro file access:
```bash
# Reset permissions for Adobe apps
sudo tccutil reset FileProviderPresence com.adobe.PremierePro
```
Then restart Premiere Pro and grant access when prompted.

## ✅ Installation Verification Checklist

- [ ] Debug mode enabled in Terminal
- [ ] Extension folder copied to correct location
- [ ] Permissions set (755)
- [ ] Premiere Pro restarted
- [ ] Extension appears in Window → Extensions menu
- [ ] Extension panel opens without errors
- [ ] File selection dialog opens
- [ ] Files can be selected and displayed

## 📞 Still Having Issues?

1. **Check the README.md** for general troubleshooting
2. **Review the CHANGELOG.md** for recent updates
3. **Press Cmd + Option + I** in the extension panel to see JavaScript errors
4. **Check Console.app** for system-level errors

---

**Mac Compatibility**: ✅ Fully Supported (v1.1+)
**Tested on**: macOS Monterey, Ventura, Sonoma
**Premiere Pro**: 2021 and later

