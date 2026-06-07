# 🚀 Langflow Chat Configuration Guide

## 📋 Overview
This guide will help you configure the Langflow chat widget in your Testcase Generator HTML file.

## ⚙️ Configuration Steps

### Step 1: Locate the Configuration Section
Open `testcase-generator.html` and find this section (around line 460):

```javascript
// Configuration
const LANGFLOW_CONFIG = {
    hostUrl: "http://localhost:7860",
    flowId: "fc2ff262-f703-4f56-844d-2a5b62e909ca",
    apiKey: "sk-d5SFgV3-bWpdJtXuR1_sg__-t_9xX2Td5i0U0k22lDI"
};
```

And also update the web component attributes (around line 450):

```html
<langflow-chat
    id="langflowChat"
    host_url="http://localhost:7860"
    flow_id="fc2ff262-f703-4f56-844d-2a5b62e909ca"
    ...
></langflow-chat>
```

### Step 2: Get Your Langflow Credentials

#### **A. Host URL**
- This is your Langflow instance URL
- Examples:
  - Cloud: `https://your-workspace.langflow.cloud`
  - Self-hosted: `https://langflow.yourdomain.com`
  - Local development: `http://localhost:7860`

#### **B. Flow ID**
- Login to your Langflow instance
- Open your testcase generator flow
- The Flow ID is in the URL: `https://langflow.cloud/flow/{FLOW_ID}`
- Or find it in Flow Settings → Flow ID

#### **C. API Key**
- In Langflow, go to Settings → API Keys
- Click "Create New API Key"
- Copy the generated key
- **Important:** Save this key securely - you won't be able to see it again!

### Step 3: Update the Configuration

Replace the placeholder values in **TWO PLACES** in `testcase-generator.html`:

#### **Location 1: Web Component Attributes (around line 450)**
```html
<langflow-chat
    id="langflowChat"
    host_url="https://your-workspace.langflow.cloud"  <!-- ✅ Your actual URL -->
    flow_id="abc123-def456-ghi789"                    <!-- ✅ Your flow ID -->
    chat_position="top-right"
    chat_trigger="icon"
    window_title="Testcase Generator AI"
    ...
></langflow-chat>
```

**Note:** The `api_key` is set programmatically for security. Update it in Location 2.

#### **Location 2: JavaScript Configuration (around line 460)**
```javascript
const LANGFLOW_CONFIG = {
    hostUrl: "https://your-workspace.langflow.cloud",  // ✅ Your actual URL
    flowId: "abc123-def456-ghi789",                     // ✅ Your flow ID
    apiKey: "lf_abc123def456ghi789"                    // ✅ Your API key
};
```

### Step 4: Test the Integration

1. Save the `testcase-generator.html` file
2. Open it in a web browser
3. **You will ALWAYS see a 💬 chat icon in the top-right corner** (this is the fallback button)
4. Click the icon to open the chat
5. Try pasting a sample user story

**Note:** The custom chat button ensures the icon is always visible, even if Langflow takes time to load or has configuration issues.

## 🎨 Customization Options

### Change Chat Icon
Update both the custom button and Langflow component:

```html
<!-- Custom button -->
<button id="customChatButton" class="custom-chat-button" ...>
    🤖  <!-- Change this emoji -->
</button>

<!-- Langflow component -->
<langflow-chat
    trigger_icon="🤖"  <!-- Change this too -->
    ...
></langflow-chat>
```

### Change Chat Position
```html
<langflow-chat
    chat_position="top-right"  <!-- Options: top-right, top-left, bottom-right, bottom-left -->
    ...
></langflow-chat>
```

Also update the custom button CSS:
```css
.custom-chat-button {
    top: 20px;     /* Change these values */
    right: 20px;   /* to move the button */
}
```

### Customize Chat Colors
```html
<langflow-chat
    icon_bg_color="#667eea"
    input_container_background_color="#ffffff"
    ...
></langflow-chat>
```

### Change Window Title
```html
<langflow-chat
    window_title="Your Custom Title"
    ...
></langflow-chat>
```

## 🔒 Security Best Practices

1. **Never commit API keys to version control**
   - Add `testcase-generator.html` to `.gitignore` if it contains keys
   - Or use environment variables/config files

2. **Use separate API keys for development and production**

3. **Rotate API keys regularly**

4. **Set appropriate CORS policies in Langflow**

## 🐛 Troubleshooting

### Chat icon not appearing?
- ✅ **The custom fallback button should ALWAYS be visible** at the top-right corner
- ✅ Check browser console (F12) for errors
- ✅ If you see the 💬 icon, the fallback is working correctly
- ✅ If Langflow loads successfully, the custom button will be hidden automatically

### Langflow not loading?
- ✅ Check the browser console for script loading errors
- ✅ Verify internet connection (CDN script needs to download)
- ✅ Try hard refresh: Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)
- ✅ The fallback button will remain visible if Langflow doesn't load

### Chat not responding?
- ✅ Verify your Langflow flow is deployed and running
- ✅ Check API key permissions in Langflow settings
- ✅ Test the flow directly in Langflow interface first
- ✅ Check browser console for API errors

### CORS errors?
- ✅ Configure CORS settings in your Langflow instance
- ✅ Add your domain to allowed origins
- ✅ For localhost testing, ensure Langflow accepts local connections

### Two chat icons appearing?
- ✅ This means Langflow loaded successfully!
- ✅ The custom button should auto-hide when Langflow is detected
- ✅ If both remain visible, check browser console for JavaScript errors

### Styling issues?
- ✅ Check for CSS conflicts with other stylesheets
- ✅ Verify z-index values (custom button: 10000, Langflow: 9999)
- ✅ Try inspecting the element with browser dev tools

## 📚 Additional Resources

- [Langflow Documentation](https://docs.langflow.org/)
- [Langflow Embedded Chat GitHub](https://github.com/langflow-ai/langflow-embedded-chat)
- [Langflow Community](https://discord.gg/langflow)

## ✅ Quick Checklist

Before going live, ensure:
- [ ] Host URL is correct and accessible
- [ ] Flow ID matches your testcase generator flow
- [ ] API key is valid and has proper permissions
- [ ] Chat icon appears in top-right corner
- [ ] Chat opens when clicking the icon
- [ ] Test with sample user stories
- [ ] Copy and clear buttons work
- [ ] Responsive on mobile devices

---

**Need help?** Check the Langflow documentation or reach out to the Langflow community!
