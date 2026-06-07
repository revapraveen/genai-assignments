# 🧪 AI-Powered Testcase Generator

A beautiful, single-page HTML application that transforms user stories into comprehensive test cases using AI via Langflow integration.

## 📋 Features

✅ **Always-Visible Chat Icon** - Custom fallback button ensures the chat icon is always present  
✅ **Langflow Integration** - Direct API integration with Langflow AI  
✅ **Sample User Stories** - 8 pre-loaded banking domain user stories  
✅ **One-Click Copy** - Copy sample stories or generated test cases  
✅ **CSV Export** - Download test cases as CSV for import into test management tools  
✅ **Clear Chat** - Start fresh conversations easily  
✅ **Scrollable Interface** - Custom-styled scrollbars throughout  
✅ **Blue & White Theme** - Professional gradient design  
✅ **Responsive Design** - Works on desktop and mobile  
✅ **Error Handling** - Fallback mechanisms and user-friendly notifications  

## 🚀 Quick Start

### 1. Configure Langflow Credentials

Open `testcase-generator.html` and update these values in **TWO LOCATIONS**:

#### Location 1: HTML Web Component (line ~450)
```html
<langflow-chat
    host_url="YOUR_HOST_URL"
    flow_id="YOUR_FLOW_ID"
    ...
></langflow-chat>
```

#### Location 2: JavaScript Config (line ~460)
```javascript
const LANGFLOW_CONFIG = {
    hostUrl: "YOUR_HOST_URL",
    flowId: "YOUR_FLOW_ID",
    apiKey: "YOUR_API_KEY"
};
```

### 2. Open in Browser

Simply double-click `testcase-generator.html` or open it in any modern web browser.

### 3. Start Generating Test Cases

1. Look for the 💬 chat icon in the top-right corner
2. Click to open the AI chat
3. Copy sample stories or paste your own
4. Get instant test case generation!
5. **Download as CSV** using the 📥 CSV button
6. Import into your test management tool

## 🏗️ Architecture

### Hybrid Approach

This implementation uses a **hybrid approach** for maximum reliability:

```
┌─────────────────────────────────────┐
│  Custom Fallback Button (Always On) │ ← Guaranteed visibility
├─────────────────────────────────────┤
│  Langflow Web Component (Primary)   │ ← Official integration
├─────────────────────────────────────┤
│  Langflow CDN Script                │ ← External dependency
└─────────────────────────────────────┘
```

**Benefits:**
- ✅ Custom button appears immediately on page load
- ✅ Langflow integration loads asynchronously
- ✅ If Langflow loads successfully, custom button auto-hides
- ✅ If Langflow fails, custom button provides fallback functionality
- ✅ User always sees a clickable chat icon

### File Structure

```
.
├── testcase-generator.html       # Main application (single file)
├── LANGFLOW_SETUP_GUIDE.md       # Detailed configuration guide
└── README.md                      # This file
```

## 🎨 Customization

### Export Test Cases as CSV

The application includes a powerful CSV export feature:

1. **Generate test cases** using the AI chat
2. Click the **📥 CSV** button in the chat window
3. File downloads automatically as `testcases_YYYY-MM-DD-HH-MM-SS.csv`
4. **Import into test management tools** like JIRA, TestRail, Azure DevOps, qTest

**CSV Format includes:**
- Test Case ID (TC001, TC002, ...)
- Title
- Description
- Test Steps
- Expected Result
- Priority (High/Medium/Low)
- Category (Functional/Security/Performance)
- Status (Not Executed by default)
- Created Date

The export feature intelligently parses AI responses to extract structured test case information, supporting multiple formats (tables, lists, structured text).

See [CSV_EXPORT_FEATURE.md](./CSV_EXPORT_FEATURE.md) for detailed documentation.

---

## 🎨 Customization

### Change Colors

Edit the CSS gradient values in `testcase-generator.html`:

```css
.custom-chat-button {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    /* Change to your colors */
}
```

### Change Chat Icon

Update both locations:

```html
<!-- Custom button -->
<button class="custom-chat-button">
    🤖  <!-- Your emoji here -->
</button>

<!-- Langflow component -->
<langflow-chat trigger_icon="🤖" ...></langflow-chat>
```

### Change Position

```css
.custom-chat-button {
    top: 20px;    /* Adjust vertical position */
    right: 20px;  /* Adjust horizontal position */
}
```

```html
<langflow-chat chat_position="top-right" ...></langflow-chat>
```

## 🔧 Technical Details

### Dependencies

- **Langflow Embedded Chat**: CDN-loaded web component
- **No Build Tools Required**: Pure HTML/CSS/JavaScript
- **No npm/Node.js**: Works directly in browser

### Browser Support

- ✅ Chrome/Edge (Chromium-based)
- ✅ Firefox
- ✅ Safari
- ✅ Mobile browsers

### Key Components

1. **Custom Chat Button** (`custom-chat-button` class)
   - Fixed positioning at top-right
   - Pulse animation for attention
   - Always visible on load
   - Auto-hides when Langflow loads

2. **Langflow Web Component** (`<langflow-chat>`)
   - Official Langflow integration
   - Attribute-based configuration
   - Shadow DOM encapsulation
   - Event-based communication

3. **Configuration Object** (`LANGFLOW_CONFIG`)
   - Centralized credentials
   - Used by initialization script
   - Easy to update

## 🐛 Troubleshooting

### "Chat icon is missing"
- **This should never happen!** The custom fallback button is always visible
- Check if your browser blocks the page (look for shield icon in address bar)
- Try opening in incognito/private mode

### "Chat not responding"
- Verify Langflow instance is running
- Check flow is deployed in Langflow
- Test flow directly in Langflow UI first
- Check browser console (F12) for errors

### "Two chat icons appearing"
- This means Langflow loaded successfully
- The custom button should auto-hide after 1 second
- If both remain, check browser console for errors

### "CORS errors"
- Configure CORS in your Langflow instance
- Add your domain to allowed origins
- For local testing, allow `file://` protocol or use local server

## 📚 Documentation

- [Langflow Setup Guide](./LANGFLOW_SETUP_GUIDE.md) - Detailed configuration instructions
- [Langflow Official Docs](https://docs.langflow.org/)
- [Langflow Embedded Chat](https://github.com/langflow-ai/langflow-embedded-chat)

## 🔒 Security Notes

1. **API Keys**: Never commit API keys to version control
2. **HTTPS**: Use HTTPS in production for secure communication
3. **CORS**: Configure appropriate CORS policies
4. **Rate Limiting**: Implement rate limiting in Langflow
5. **Key Rotation**: Regularly rotate API keys

## ✅ Checklist Before Going Live

- [ ] Updated `host_url` in web component
- [ ] Updated `flowId` in web component
- [ ] Updated all three values in `LANGFLOW_CONFIG`
- [ ] Tested with sample user stories
- [ ] Verified chat icon appears
- [ ] Tested chat opens and responds
- [ ] Checked on mobile device
- [ ] Reviewed browser console for errors
- [ ] Configured CORS if needed
- [ ] Secured API keys appropriately

## 📝 License

This is a demonstration project. Modify and use as needed for your purposes.

## 🤝 Support

For Langflow-specific issues:
- [Langflow Discord](https://discord.gg/langflow)
- [Langflow GitHub Issues](https://github.com/langflow-ai/langflow/issues)

For this implementation:
- Check the setup guide
- Review browser console for errors
- Verify configuration values

---

**Built with ❤️ using Langflow and pure HTML/CSS/JavaScript**
