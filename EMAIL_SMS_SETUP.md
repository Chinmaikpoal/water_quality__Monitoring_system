# Email & SMS Alert Configuration Guide

This guide explains how to set up email and SMS alerts for the Water Quality Monitoring System.

## Table of Contents
1. [Email Setup (Gmail)](#email-setup-gmail)
2. [SMS Setup (Twilio)](#sms-setup-twilio)
3. [Environment Variables](#environment-variables)
4. [Testing Alerts](#testing-alerts)

---

## Email Setup (Gmail)

### Step 1: Enable 2-Factor Authentication
1. Go to [Google Account](https://myaccount.google.com/)
2. Click **Security** in the left sidebar
3. Scroll down to **2-Step Verification** and enable it
4. Follow the verification steps

### Step 2: Create App Password
1. Go back to [Google Account Security](https://myaccount.google.com/security)
2. Click **App passwords** (appears after 2FA is enabled)
3. Select:
   - App: **Mail**
   - Device: **Other (custom name)** → type "Water Quality System"
4. Click **Generate**
5. Copy the 16-character password (remove spaces)

### Step 3: Add to Environment Variables

**Windows (PowerShell):**
```powershell
$env:EMAIL_HOST = "smtp.gmail.com"
$env:EMAIL_PORT = "587"
$env:EMAIL_USER = "your-email@gmail.com"
$env:EMAIL_PASS = "your-16-char-app-password"
$env:EMAIL_FROM = "your-email@gmail.com"
```

**Windows (.env file):**
Create a `.env` file in the `backend/` folder:
```
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-16-char-app-password
EMAIL_FROM=your-email@gmail.com
```

**Alternative Providers:**
- **Outlook/Hotmail**: host=`smtp-mail.outlook.com`, port=`587`
- **Yahoo**: host=`smtp.mail.yahoo.com`, port=`587`
- **Custom SMTP**: Configure with your provider's host and port

---

## SMS Setup (Twilio)

### Step 1: Create Twilio Account
1. Go to [Twilio Console](https://www.twilio.com/console)
2. Sign up for a free account
3. Verify your phone number

### Step 2: Get Credentials
1. In Twilio Console, go to **Account** → **API Keys & Tokens**
2. Copy your **Account SID** and **Auth Token**
3. Go to **Phone Numbers** → **Manage Numbers** → **Active Numbers**
4. Note your **Twilio Phone Number** (format: +1XXXXXXXXXX)

### Step 3: Add to Environment Variables

**Windows (PowerShell):**
```powershell
$env:TWILIO_SID = "your-account-sid"
$env:TWILIO_AUTH = "your-auth-token"
$env:TWILIO_FROM = "+1234567890"
```

**Windows (.env file):**
```
TWILIO_SID=your-account-sid
TWILIO_AUTH=your-auth-token
TWILIO_FROM=+1234567890
```

### Step 4: Verify Recipients
During free trial, SMS only works to **verified phone numbers**:
1. In Twilio Console, go to **Phone Numbers** → **Verified Caller IDs**
2. Add each recipient phone number and verify

---

## Environment Variables

### Complete .env Example

Create `backend/.env`:
```
# Email Configuration
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-16-char-app-password
EMAIL_FROM=your-email@gmail.com

# SMS Configuration (Twilio)
TWILIO_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH=your-auth-token
TWILIO_FROM=+1234567890

# JWT Secret
JWT_SECRET=your-super-secret-key-change-this

# Alert Recipients (Optional - can be set in UI)
ALERT_EMAILS=recipient1@example.com,recipient2@example.com
ALERT_PHONES=+1111111111,+2222222222
```

### Loading .env in Python

The backend automatically loads `.env` using environment variables. You can also manually load it:

```python
from dotenv import load_dotenv
import os

load_dotenv('backend/.env')
email_host = os.environ.get('EMAIL_HOST')
```

---

## Testing Alerts

### Method 1: Using the Alert Test Button (Easiest)
1. Start the backend server
2. Open the dashboard in browser
3. Login
4. Click **🚨 Alerts** button
5. Go to **Recipients** tab
6. Add test email/phone numbers
7. Click **Send Test Alert**
8. Check email/phone for test message

### Method 2: Manual Test (Python)
```python
import requests
import json

# Test email & SMS
response = requests.post(
    'http://localhost:5000/admin/test-alert',
    headers={'Authorization': 'Bearer YOUR_JWT_TOKEN'},
    json={
        'subject': 'Test Alert',
        'body': 'This is a test message'
    }
)

print(response.json())
# Output: {"email_sent": true, "sms_sent": true}
```

### Method 3: Using Simulator
1. Go to **Sensor Controls** tab
2. Manually set readings to unsafe values:
   - pH < 6.5 or > 8.5
   - Turbidity > 5
   - Temperature > 30
3. Click **Update Readings**
4. Backend automatically sends alerts to configured recipients

---

## Troubleshooting

### Emails Not Sending
- ❌ **Gmail 2FA not enabled**: Enable 2-Step Verification first
- ❌ **Wrong app password**: Gmail app passwords are 16 characters (remove spaces)
- ❌ **Allow less secure apps**: Some providers block third-party apps
- ✅ **Solution**: Check backend console for error messages (`python -u app.py`)

### SMS Not Sending
- ❌ **Twilio trial account**: Only verified numbers receive SMS (add in Verified Caller IDs)
- ❌ **Wrong phone format**: Use international format: +1234567890
- ❌ **Credentials not set**: Check `TWILIO_SID`, `TWILIO_AUTH`, `TWILIO_FROM`
- ✅ **Check Twilio logs**: Go to Twilio Console → **Logs** → **Message Logs**

### Recipients List Empty
- ❌ **Not logged in**: JWT token required to add recipients
- ❌ **alerts.json not created**: First, add a recipient via UI to create file
- ✅ **Verify via**: Go to **Alerts** → **Recipients** tab → see current list

### Alerts Not Triggering
- Alerts only send for **RED** (unsafe) readings
- Safe/Yellow readings don't trigger alerts
- Check **Alerts** → **Unsafe Readings** tab to see current unsafe readings
- Use **Send Test Alert** button to manually test

---

## Alert Rules

Alerts are triggered when ANY of these conditions are met:
- **pH < 6.5** or **pH > 8.5** (acidic or alkaline)
- **Turbidity > 5** (high cloudiness)
- **Temperature > 30°C** (too warm)

Alert recipients receive:
- **Email**: Formatted message with all parameters
- **SMS**: Text message with alert status and timestamp
- **WhatsApp**: (coming soon) Direct message via WhatsApp Business API

---

## Email Template Customization

The email sent contains:
```
Subject: Water Quality Alert: [Status] at [Timestamp]

Body:
Alert: Water Quality status is [Status]
Timestamp: [2024-12-07T10:30:45]
pH: 5.2
Turbidity: 8.5
Temperature: 32.1
WQI: 15.3

This is an automated alert from the Water Quality Monitoring System.
```

To customize, edit the `send_alert_if_needed()` function in `backend/app.py`.

---

## SMS Message Format

Default SMS message:
```
Alert: Water Quality status is Unsafe
Timestamp: 2024-12-07 10:30:45
pH: 5.2 | Turbidity: 8.5 | Temp: 32°C | WQI: 15.3
```

---

## Security Notes

⚠️ **Important:**
- Never commit `.env` file to version control (add to `.gitignore`)
- Rotate credentials periodically
- Use app-specific passwords (not your actual password)
- Don't share your Twilio credentials
- Keep JWT_SECRET strong and unique

---

## Support

If alerts aren't working:
1. Check backend console for error messages
2. Verify environment variables are set: `echo $env:EMAIL_HOST` (PowerShell)
3. Test credentials manually using the test alert button
4. Check email spam folder
5. For Twilio: check [Twilio Console Logs](https://www.twilio.com/console/logs)

