# EmailJS Setup — Shringara Mehandi Booking Form

The booking form now sends bookings via **EmailJS**. Follow these steps once to
get 3 keys, paste them into `index.html`, and you're live.

> Free plan = 200 emails/month, which is plenty for a booking form.

---

## Step 1 — Create an EmailJS account
1. Go to **https://www.emailjs.com** → **Sign Up** (free).
2. Use whichever email should *own/manage* this client's form.
   - You can reuse your existing EmailJS account and just make a **new template**
     for this client — that's totally fine and keeps it free.

## Step 2 — Add an Email Service (the account that SENDS the mail)
1. Dashboard → **Email Services** → **Add New Service**.
2. Pick **Gmail** (easiest) → **Connect Account** → sign in with the Gmail you
   want to send *from* (this can be your own Gmail; the client still RECEIVES it).
3. After connecting, copy the **Service ID** (looks like `service_xxxxxxx`).

## Step 3 — Create an Email Template
1. Dashboard → **Email Templates** → **Create New Template**.
2. In the **Settings / To Email** field put:  `{{to_email}}`
3. In the **Cc** field put:  `{{cc_email}}`
4. In the **Reply To** field put:  `{{reply_to}}`
5. **Subject:**  `New Mehandi Booking — {{from_name}}`
6. **Content** (paste this):

   ```
   New booking request from the Shringara Mehandi website 🌿

   Name:     {{from_name}}
   Phone:    {{phone}}
   Email:    {{email}}
   Occasion: {{occasion}}

   Message:
   {{message}}

   ---
   Sent from: {{page_url}}
   ```
7. **Save**, then copy the **Template ID** (looks like `template_xxxxxxx`).

## Step 4 — Get your Public Key
1. Dashboard → **Account** → **General**.
2. Copy the **Public Key** (looks like `xxxxxxxxxxxxxx`).

## Step 5 — Paste the 3 keys into the website
Open `index.html`, find `EMAILJS_CONFIG` near the bottom, and fill in:

```js
const EMAILJS_CONFIG = {
  publicKey:  'PASTE_PUBLIC_KEY_HERE',
  serviceId:  'PASTE_SERVICE_ID_HERE',
  templateId: 'PASTE_TEMPLATE_ID_HERE',
  toEmail:    'sanjkaremani01@gmail.com',   // client gets bookings here
  ccEmail:    'anandsullad777@gmail.com'    // your copy (set to '' to disable)
};
```

## Step 6 — Test
1. Open the site, fill the booking form, and submit.
2. You should land on `thank-you.html` and the booking email should arrive at
   `sanjkaremani01@gmail.com` (and CC `anandsullad777@gmail.com`).
3. If it fails, open the browser console (F12) — EmailJS logs the exact error.

---

## Notes
- The variable names in the template (`{{from_name}}`, `{{phone}}`, etc.) must
  match the keys sent from `index.html`. They already do — don't rename them.
- "Service" = the Gmail that SENDS the notification.
  "To Email" (`{{to_email}}`) = who RECEIVES it (the client). They can be different.
- For a fully separate client account, repeat Step 1 with the client's own email
  and connect their Gmail as the service — otherwise reusing your account is fine.
