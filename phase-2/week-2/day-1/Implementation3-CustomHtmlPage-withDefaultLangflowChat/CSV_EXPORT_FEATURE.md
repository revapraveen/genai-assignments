# 📥 CSV Export Feature Documentation

## Overview
The Testcase Generator now includes a powerful **CSV Export** feature that allows you to download all generated test cases in a structured CSV format, ready for import into test management tools.

---

## 🎯 How to Use

### Step 1: Generate Test Cases
1. Open the chat window by clicking the 💬 button
2. Paste your user stories into the chat
3. Wait for the AI to generate test cases

### Step 2: Download as CSV
1. Click the **📥 CSV** button in the chat actions
2. The file will automatically download as `testcases_YYYY-MM-DD.csv`
3. Import the CSV into your test management tool (JIRA, TestRail, etc.)

---

## 📊 CSV Format

The exported CSV includes the following columns:

| Column | Description | Example |
|--------|-------------|---------|
| **Test Case ID** | Unique identifier | TC001, TC002 |
| **Title** | Test case title/summary | "Verify login with valid credentials" |
| **Description** | Detailed description | "Test the login functionality..." |
| **Test Steps** | Step-by-step procedure | "1. Navigate to login page 2. Enter username..." |
| **Expected Result** | Expected outcome | "User successfully logs in and sees dashboard" |
| **Priority** | Priority level | High, Medium, Low |
| **Category** | Test category | Functional, Security, Performance |
| **Status** | Execution status | Not Executed (default) |
| **Created Date** | Date of creation | 2026-06-06 |

---

## 🔍 Intelligent Parsing

The CSV export feature uses **intelligent parsing** to extract structured test cases from AI responses. It supports multiple formats:

### Format 1: Table Format
```
| Test Case | Description | Steps | Expected Result |
|-----------|-------------|-------|-----------------|
| TC001     | Login test  | ...   | Success         |
```

### Format 2: Structured Text
```
Test Case 1: Login with valid credentials
Description: Verify user can login
Steps: 1. Open app 2. Enter credentials 3. Click login
Expected Result: User is logged in
Priority: High
```

### Format 3: Simple List
```
1. Test Case: Verify login functionality
2. Test Case: Verify password reset
3. Test Case: Verify user registration
```

### Format 4: Free Text
If no structured format is detected, the entire AI response is captured as test case content.

---

## 📁 Example CSV Output

```csv
Test Case ID,Title,Description,Test Steps,Expected Result,Priority,Category,Status,Created Date
TC001,"Login with valid credentials","Verify user can login with correct username and password","1. Navigate to login page 2. Enter valid username 3. Enter valid password 4. Click login button","User successfully logs in and sees the dashboard",High,Functional,Not Executed,2026-06-06
TC002,"Login with invalid password","Verify appropriate error for wrong password","1. Navigate to login page 2. Enter valid username 3. Enter invalid password 4. Click login button","Error message displays: Invalid credentials",High,Security,Not Executed,2026-06-06
TC003,"Password reset functionality","Verify user can reset forgotten password","1. Click Forgot Password link 2. Enter email 3. Click Submit 4. Check email for reset link","Password reset email is received with valid link",Medium,Functional,Not Executed,2026-06-06
```

---

## 🛠️ Import into Test Management Tools

### JIRA (Xray/Zephyr)
1. Go to **Test Management** → **Import**
2. Choose **CSV Import**
3. Map CSV columns to JIRA fields
4. Import test cases

### TestRail
1. Go to **Test Cases** → **Import**
2. Select **CSV (Columns)** format
3. Map columns: 
   - Test Case ID → Case ID
   - Title → Title
   - Test Steps → Steps
   - Expected Result → Expected Result
4. Import

### Azure DevOps
1. Open **Test Plans**
2. Click **Import** → **CSV**
3. Map fields and import

### qTest
1. Navigate to **Test Design**
2. Click **Import** → **CSV**
3. Configure field mapping
4. Import test cases

### Manual Spreadsheet
Simply open the CSV in:
- Microsoft Excel
- Google Sheets
- LibreOffice Calc

---

## ✨ Features

### Auto-Numbering
- Test cases are automatically numbered (TC001, TC002, TC003...)
- Sequential numbering ensures uniqueness

### Smart Field Detection
- Automatically extracts:
  - Test case titles
  - Descriptions
  - Test steps
  - Expected results
  - Priority levels
  - Categories

### CSV Safety
- Handles special characters (commas, quotes, newlines)
- Properly escapes fields
- UTF-8 encoding for international characters

### Timestamp Naming
- Files named with timestamp: `testcases_2026-06-06T14-30-15.csv`
- Prevents overwriting previous exports
- Easy to track versions

---

## 🎨 Customization

You can customize the CSV format by modifying the `convertTestCasesToCSV()` function in the HTML file:

### Add Custom Columns
```javascript
const headers = [
    'Test Case ID',
    'Title',
    'Description',
    'Test Steps',
    'Expected Result',
    'Priority',
    'Category',
    'Status',
    'Created Date',
    'Assigned To',      // Add custom column
    'Environment'       // Add custom column
];
```

### Change Default Values
```javascript
testCase.priority = 'Critical';  // Change default priority
testCase.status = 'Ready';       // Change default status
testCase.category = 'Regression'; // Change default category
```

### Modify Test Case ID Format
```javascript
id: `TEST-${String(testCaseId).padStart(4, '0')}`  // TEST-0001 format
id: `TC_${projectCode}_${testCaseId}`              // TC_PROJ_1 format
```

---

## 🧪 Testing the Feature

### Test with Simple Input
1. Send message: "Test login functionality"
2. Wait for AI response
3. Click **📥 CSV**
4. Verify CSV downloads with test case

### Test with Multiple Test Cases
1. Paste multiple user stories
2. AI generates multiple test cases
3. Click **📥 CSV**
4. Verify all test cases are in CSV

### Test with Complex Format
1. AI returns table format
2. Click **📥 CSV**
3. Verify table data is properly extracted

---

## 🐛 Troubleshooting

### "No test cases to download"
**Cause:** No AI responses in chat history
**Fix:** Send a message and wait for AI response first

### "No structured test cases found"
**Cause:** AI response doesn't match expected format
**Fix:** The tool will still create CSV with raw content

### CSV not downloading
**Cause:** Browser blocking downloads
**Fix:** Check browser settings to allow downloads from file:// URLs

### Special characters appear wrong
**Cause:** Encoding issue
**Fix:** Open CSV with UTF-8 encoding option

### Missing test case fields
**Cause:** AI response doesn't include all fields
**Fix:** Default values are used (e.g., "Medium" priority)

---

## 📊 Sample Test Cases for CSV

Here are sample user stories that generate good CSV exports:

```
User Story 1:
As a customer, I want to transfer funds between my accounts so that I can manage my money efficiently.

User Story 2:
As a customer, I want to view my transaction history for the last 90 days so that I can track my spending.

User Story 3:
As a customer, I want to receive instant notifications for transactions above $500 so that I can detect fraud quickly.
```

The AI will generate detailed test cases that export beautifully to CSV.

---

## 🎯 Best Practices

1. **Generate multiple test cases** before exporting (better value)
2. **Review in chat** before downloading CSV
3. **Use Clear button** to start fresh test suite
4. **Download periodically** to save progress
5. **Import to test tools** immediately to avoid version conflicts

---

## 📈 Future Enhancements

Possible future features:
- Export to Excel (.xlsx) format
- Export to JSON for API tools
- Custom column selection
- Template-based export
- Batch export with filtering
- Direct integration with test management APIs

---

## 💡 Tips

- **Organize by priority**: Sort CSV by Priority column in Excel
- **Add test data**: Add a "Test Data" column for inputs
- **Track execution**: Update Status column after running tests
- **Version control**: Keep CSV files in Git for history
- **Collaborate**: Share CSV files with team via email/Slack

---

## ✅ Summary

The CSV export feature provides:
- ✅ One-click download of all test cases
- ✅ Structured format ready for import
- ✅ Intelligent parsing of AI responses
- ✅ Compatible with all major test tools
- ✅ Professional CSV formatting
- ✅ Automatic field population
- ✅ Timestamp-based file naming

**Boost your productivity by seamlessly moving from AI-generated test cases to your test management workflow!** 🚀
