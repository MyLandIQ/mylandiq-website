# MyLandIQ Website Setup Guide

## Overview
This guide will help you deploy your MyLandIQ website on GitHub Pages with your custom domain (mylandiq.com).

---

## Step 1: Create GitHub Repository

### 1.1 Create the Repository
1. Go to https://github.com/new
2. Repository name: `mylandiq.github.io` (or just `mylandiq-website`)
3. Make it **Public**
4. Click "Create repository"

### 1.2 Upload Website Files
Upload all files from this folder to the repository:
```
mylandiq-website/
├── index.html                    (Main landing page)
├── CNAME                         (Custom domain config)
├── privacy-policy/
│   └── index.html               (Privacy Policy)
├── terms/
│   └── index.html               (Terms of Service)
└── refund-policy/
    └── index.html               (Refund Policy)
```

**How to upload:**
- Option A: Use GitHub web interface (drag and drop)
- Option B: Use Git commands:
```bash
git init
git add .
git commit -m "Initial website setup"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mylandiq.github.io.git
git push -u origin main
```

### 1.3 Enable GitHub Pages
1. Go to your repository → Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main` / `root`
4. Click Save
5. Wait 1-2 minutes for deployment

---

## Step 2: Configure DNS in Namecheap

### 2.1 Access DNS Settings
1. Log in to Namecheap (https://www.namecheap.com)
2. Go to Dashboard → Domain List
3. Click "Manage" next to mylandiq.com
4. Go to "Advanced DNS" tab

### 2.2 Delete Existing Records
Remove any existing A, AAAA, or CNAME records for @ and www (keep MX records if you have email)

### 2.3 Add GitHub Pages DNS Records

Add these records EXACTLY:

#### A Records (for apex domain - mylandiq.com)
| Type | Host | Value | TTL |
|------|------|-------|-----|
| A Record | @ | 185.199.108.153 | Automatic |
| A Record | @ | 185.199.109.153 | Automatic |
| A Record | @ | 185.199.110.153 | Automatic |
| A Record | @ | 185.199.111.153 | Automatic |

#### CNAME Record (for www subdomain)
| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME Record | www | YOUR_USERNAME.github.io. | Automatic |

**Note:** Replace `YOUR_USERNAME` with your actual GitHub username.

#### Optional: AAAA Records (IPv6)
| Type | Host | Value | TTL |
|------|------|-------|-----|
| AAAA Record | @ | 2606:50c0:8000::153 | Automatic |
| AAAA Record | @ | 2606:50c0:8001::153 | Automatic |
| AAAA Record | @ | 2606:50c0:8002::153 | Automatic |
| AAAA Record | @ | 2606:50c0:8003::153 | Automatic |

### 2.4 Final DNS Configuration Should Look Like:
```
Type    | Host | Value                      | TTL
--------|------|----------------------------|----------
A       | @    | 185.199.108.153           | Automatic
A       | @    | 185.199.109.153           | Automatic
A       | @    | 185.199.110.153           | Automatic
A       | @    | 185.199.111.153           | Automatic
CNAME   | www  | YOUR_USERNAME.github.io.   | Automatic
```

### 2.5 Remove the Existing Redirect
In your Namecheap screenshot, there's a redirect from mylandiq.com → www.mylandiq.com.
**REMOVE THIS** after setting up DNS, as GitHub Pages handles redirects automatically.

---

## Step 3: Configure Custom Domain in GitHub

### 3.1 Add Custom Domain
1. Go to your repository → Settings → Pages
2. Under "Custom domain", enter: `www.mylandiq.com`
3. Click Save
4. Wait for DNS check (may take a few minutes)

### 3.2 Enable HTTPS
1. Once DNS is verified, check "Enforce HTTPS"
2. This enables free SSL certificate

### 3.3 Verify Setup
After 10-30 minutes, your site should be live at:
- https://www.mylandiq.com
- https://mylandiq.com (redirects to www)

---

## Step 4: Verify Everything Works

### Test These URLs:
- [ ] https://www.mylandiq.com (main page)
- [ ] https://mylandiq.com (should redirect to www)
- [ ] https://www.mylandiq.com/privacy-policy/ (Privacy Policy)
- [ ] https://www.mylandiq.com/terms/ (Terms of Service)
- [ ] https://www.mylandiq.com/refund-policy/ (Refund Policy)

### Common Issues:

**DNS Not Propagated Yet**
- DNS changes can take up to 48 hours
- Use https://dnschecker.org to check propagation
- Try clearing browser cache or use incognito mode

**404 Error**
- Ensure CNAME file exists in repository root
- Check that index.html files are in correct folders
- Wait a few minutes after pushing changes

**HTTPS Not Working**
- Wait 24 hours for SSL certificate to be issued
- Ensure "Enforce HTTPS" is checked in GitHub Pages settings

**Certificate Error**
- Usually resolves within 24 hours
- Make sure CNAME file contains exact domain

---

## Step 5: Set Up Email Addresses (Optional)

To use email like support@mylandiq.com:

### Option A: Namecheap Email (Paid)
1. Purchase Namecheap email hosting
2. Add MX records as instructed

### Option B: Gmail Forwarding (Free)
1. Use ImprovMX (free tier: https://improvmx.com)
2. Add their MX records
3. Forward to your existing Gmail

### Option C: Zoho Mail (Free for 1 user)
1. Sign up at https://www.zoho.com/mail/
2. Add MX records as instructed
3. Get free professional email

---

## File Structure Summary

Your GitHub repository should have this structure:
```
mylandiq.github.io/
│
├── index.html                 # Landing page
├── CNAME                      # Contains: www.mylandiq.com
│
├── privacy-policy/
│   └── index.html            # Privacy Policy page
│
├── terms/
│   └── index.html            # Terms of Service page
│
└── refund-policy/
    └── index.html            # Refund Policy page
```

---

## URLs After Setup

| Page | URL |
|------|-----|
| Home | https://www.mylandiq.com |
| Privacy Policy | https://www.mylandiq.com/privacy-policy/ |
| Terms of Service | https://www.mylandiq.com/terms/ |
| Refund Policy | https://www.mylandiq.com/refund-policy/ |

---

## Update Your Android App

After website is live, update these URLs in your app:

### In strings.xml or Constants:
```kotlin
const val PRIVACY_POLICY_URL = "https://www.mylandiq.com/privacy-policy/"
const val TERMS_URL = "https://www.mylandiq.com/terms/"
const val REFUND_POLICY_URL = "https://www.mylandiq.com/refund-policy/"
```

### For Google Play Store listing:
- Privacy Policy URL: https://www.mylandiq.com/privacy-policy/

---

## Future Additions

### For Web Admin Panel (Later):
You can add an admin section at:
- https://www.mylandiq.com/admin/

This can be a React/Vue app deployed to the same repository or a separate subdomain (admin.mylandiq.com).

### For API Documentation (Later):
- https://www.mylandiq.com/docs/

---

## Support

If you encounter issues:
1. Check GitHub Pages documentation: https://docs.github.com/pages
2. Check Namecheap DNS help: https://www.namecheap.com/support/knowledgebase/
3. Use DNS lookup tools: https://dnschecker.org

---

**Created:** February 15, 2026
**Last Updated:** February 15, 2026
