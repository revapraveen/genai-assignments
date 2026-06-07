# 🔧 Troubleshooting Langflow 403 Error

## Problem
Getting error: `HTTP error! status: 403` when sending messages to Langflow

## Root Cause
The 403 Forbidden error typically means one of the following:
1. **API Key is invalid or expired**
2. **API Key doesn't have permission for this flow**
3. **CORS is blocking the request**
4. **Flow ID is incorrect**

---

## ✅ Solution Steps

### Step 1: Verify Langflow is Running

Open your browser and visit:
```
http://localhost:7860
```

You should see the Langflow UI. If not, start Langflow:
```bash
langflow run
```

---

### Step 2: Get the Correct API Key

1. Open Langflow UI: http://localhost:7860
2. Click on your profile icon (top-right)
3. Go to **Settings** → **API Keys**
4. Click **"Create New API Key"**
5. Copy the generated key (starts with `sk-`)
6. **Save it immediately** - you won't see it again!

---

### Step 3: Get the Correct Flow ID

1. In Langflow UI, open your testcase generator flow
2. Look at the browser URL:
   ```
   http://localhost:7860/flow/YOUR-FLOW-ID-HERE
   ```
3. Copy the Flow ID from the URL

---

### Step 4: Update Configuration in HTML File

Open `testcase-generator.html` and find this section (around line 625):

```javascript
const LANGFLOW_CONFIG = {
    hostUrl: "http://localhost:7860",
    flowId: "YOUR-FLOW-ID-HERE",        // ✏️ PASTE YOUR FLOW ID
    apiKey: "YOUR-API-KEY-HERE"         // ✏️ PASTE YOUR API KEY
};
```

**Replace:**
- `YOUR-FLOW-ID-HERE` with your actual Flow ID
- `YOUR-API-KEY-HERE` with your actual API key

---

### Step 5: Test the API Directly

Open your browser's Developer Tools (F12) and run in Console:

```javascript
const testLangflow = async () => {
    const response = await fetch('http://localhost:7860/api/v1/run/YOUR-FLOW-ID', {
        method: 'POST',
        headers: {
            'accept': 'application/json',
            'Content-Type': 'application/json',
            'x-api-key': 'YOUR-API-KEY'
        },
        body: JSON.stringify({
            input_value: "Test message",
            output_type: "chat",
            input_type: "chat"
        })
    });
    console.log('Status:', response.status);
    console.log('Response:', await response.json());
};
testLangflow();
```

**Expected result:** Status 200 with a response

---

### Step 6: Check Langflow API Documentation

Visit Langflow's built-in API docs:
```
http://localhost:7860/docs
```

Here you can:
1. See all available endpoints
2. Test the `/api/v1/run/{flow_id}` endpoint directly
3. Verify your API key works
4. See the exact request format required

---

## 🔍 Common Issues & Fixes

### Issue 1: "API Key is invalid"
**Fix:** Generate a new API key in Langflow settings

### Issue 2: "Flow not found"
**Fix:** 
- Make sure the flow is saved in Langflow
- Verify the Flow ID is correct
- Check the flow is not deleted

### Issue 3: "CORS error"
**Fix:** Langflow usually allows localhost by default. If you get CORS errors:
1. Check Langflow is running on `http://localhost:7860`
2. Make sure you're accessing the HTML file via `file://` or a local server
3. Add CORS headers in Langflow config if needed

### Issue 4: "Cannot reach Langflow"
**Fix:**
- Start Langflow: `langflow run`
- Check it's running on port 7860
- Try `http://127.0.0.1:7860` instead of `localhost`

### Issue 5: "Request timeout"
**Fix:**
- Your flow might be taking too long to process
- Check Langflow console for errors
- Simplify your flow to test

---

## 🧪 Testing Checklist

Before using the HTML chat:

- [ ] Langflow is running (visit http://localhost:7860)
- [ ] You can see your flow in Langflow UI
- [ ] You've created a new API key in Settings
- [ ] You've updated `LANGFLOW_CONFIG` in the HTML file
- [ ] Flow ID matches the URL in Langflow
- [ ] API key starts with `sk-`
- [ ] Tested the endpoint in http://localhost:7860/docs
- [ ] No CORS errors in browser console

---

## 📝 Correct API Format

The HTML file now uses the **correct Langflow API format**:

```javascript
// ✅ CORRECT (Updated)
fetch(`${hostUrl}/api/v1/run/${flowId}`, {
    method: 'POST',
    headers: {
        'accept': 'application/json',
        'Content-Type': 'application/json',
        'x-api-key': apiKey  // ✅ Uses x-api-key header
    },
    body: JSON.stringify({
        input_value: message,
        output_type: "chat",
        input_type: "chat",
        tweaks: {}
    })
});

// ❌ INCORRECT (Old)
headers: {
    'Authorization': `Bearer ${apiKey}`  // ❌ Wrong header
}
```

---

## 🎯 Quick Fix Summary

1. **Get NEW API key** from Langflow Settings
2. **Get Flow ID** from browser URL when viewing your flow
3. **Update both values** in `testcase-generator.html`
4. **Refresh the page** (hard refresh: Cmd+Shift+R)
5. **Try sending a message** again

---

## 💡 Still Not Working?

### Check Browser Console

1. Press **F12** to open Developer Tools
2. Go to **Console** tab
3. Look for error messages
4. Share the error details for more help

### Check Langflow Logs

In the terminal where Langflow is running, look for:
- Connection errors
- Authentication errors
- Flow execution errors

### Verify Flow Works in Langflow UI

1. Open your flow in Langflow
2. Test it directly in the Langflow playground
3. Make sure it returns a response
4. Only then try the HTML chat

---

## ✅ Success Indicators

When everything is working correctly, you should see:

**In Browser Console:**
```
✅ Langflow connection successful!
Langflow response: {...}
```

**In Chat Window:**
- Your message appears in blue (right side)
- Loading dots appear briefly
- AI response appears in white (left side)

---

**Need more help?** Check:
- Langflow documentation: https://docs.langflow.org
- Langflow API reference: http://localhost:7860/docs
- Browser console for detailed error messages
