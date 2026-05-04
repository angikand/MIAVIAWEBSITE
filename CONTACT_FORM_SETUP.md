# Contact Form — Setup Guide (no-code, ~10 min)

This is the simple path. You sign up for **Formspree**, copy one URL, paste it into the website, and submissions start arriving in your email (and optionally in Slack). No terminal, no code, no deploy.

```
Website visitor
      │
      ▼
[Contact form on miavia] ──POST──▶ [Formspree] ──▶ [Your email]
                                         │
                                         └──▶ [Slack channel]   (optional)
```

---

## Part 1 — Create a Formspree form (5 min)

1. Go to **https://formspree.io** and click **Sign up**. Use your Miavia email (e.g. `angelica@miavia.com` or your Gmail). Free plan is fine — 50 submissions per month.
2. After you confirm your email, click **+ New Form** in the dashboard.
3. Name the form `Miavia Contact`. Leave everything else default and click **Create Form**.
4. On the next screen, Formspree shows your form's endpoint — a URL that looks like:

   ```
   https://formspree.io/f/xnnnabcd
   ```

   (the `xnnnabcd` part is unique to your form). **Copy this URL.**

5. In the dashboard, open the form you just created and check the **Settings** tab:
   - **Form emails:** confirm your email address is listed here. Every submission is forwarded to this email.
   - **Submission storage:** on. Every submission is archived in the Formspree dashboard.
   - **Reply-to:** set to `email` so when you hit Reply in your inbox, it goes back to the visitor.

That's it — your form is live.

---

## Part 2 — Paste the URL into the website (2 min)

1. Open `index.html` in your editor (VS Code, Sublime, or even TextEdit).
2. Near the top, find this block (it's in the `<head>` section):

   ```html
   <script>
     window.MIAVIA_CONTACT_ENDPOINT = ''; // e.g. 'https://formspree.io/f/xnnnabcd'
     window.MIAVIA_API_BASE = '';         // advanced: custom Node backend URL
   </script>
   ```

3. Paste your Formspree URL into the quotes on the first line:

   ```html
   <script>
     window.MIAVIA_CONTACT_ENDPOINT = 'https://formspree.io/f/xnnnabcd';
     window.MIAVIA_API_BASE = '';
   </script>
   ```

4. Save the file.
5. Do the same in `miavia-github/index.html` and `miavia-github-full/index.html` so the deployed versions match.

---

## Part 3 — Test it (2 min)

1. Open `index.html` in your browser (double-click the file, or on the deployed site go to the Contact page).
2. Fill in the form with a fake name / email / message.
3. Click **Send**. The button should say "Sending…" for a second, then the "Thank you" screen appears.
4. **Check your inbox** — you should have a Formspree email with the submission.
5. **Check the Formspree dashboard** — the submission appears under your form.

If the first submission works, you're done. Formspree asks you to confirm the email address the first time, so follow the link in their confirmation email.

---

## Part 4 — (Optional) Forward submissions to Slack

You have two options:

### Option A — Free, via Zapier

Zapier's free plan gives you 100 automations per month. More than enough for a luxury brand's contact volume.

1. Go to **https://zapier.com** and sign up (free).
2. Click **Create Zap**.
3. **Trigger**: search for **Formspree** → pick **New Submission**. Connect your Formspree account, pick the Miavia Contact form.
4. **Action**: search for **Slack** → pick **Send Channel Message**. Connect your Slack workspace, pick the `#website-contact` channel, and write the message template — something like:

   ```
   :sparkles: New Miavia contact

   *Name:* {{name}}
   *Email:* {{email}}
   *Phone:* {{phone}}
   *Topic:* {{topic}}

   {{message}}
   ```

5. Click **Publish**. Every Formspree submission now also posts to Slack.

You can ignore the Slack Incoming Webhook you made earlier — Zapier uses its own connection. (But no harm in leaving the webhook there.)

### Option B — Paid, via Formspree's native Slack integration

Formspree has Slack built in on the **Plus plan ($20/month)**. In the Formspree form settings, go to **Integrations → Slack**, authorize, pick the channel, done. Cleaner than Zapier but costs money.

---

## Part 5 — (Optional) Use the Slack webhook you already created

If you'd rather use the webhook you made in your Slack app directly (free, no Zapier), you'll need the small Node backend that's included in the `backend/` folder. That path requires a developer — it's covered at the bottom of this doc under **Advanced option**.

---

## Summary of what you need to do

**Minimum (email only):**
- [ ] Sign up at formspree.io
- [ ] Create a form, copy the endpoint URL
- [ ] Paste it into `window.MIAVIA_CONTACT_ENDPOINT` in `index.html`
- [ ] Test from your live site

**With Slack:**
- [ ] Do the above
- [ ] Either: sign up at zapier.com and wire Formspree → Slack (free), or
- [ ] Upgrade Formspree to Plus ($20/mo) and enable the Slack integration in form settings

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| First submission didn't go through | Formspree requires email confirmation before the form goes live. Check your inbox for a Formspree email and click the confirmation link. |
| "Thank you" screen doesn't appear, error banner instead | The endpoint URL is probably wrong. Copy it again from the Formspree dashboard and re-paste. |
| "Form not enabled" error | The form is paused or over the free-tier limit (50/month). Upgrade or wait for the monthly reset. |
| Spam submissions | Formspree has built-in spam filtering. The site also has a hidden honeypot field. If you still see spam, enable reCAPTCHA in the Formspree form settings. |
| No Slack message (Zapier option) | Open the Zap in Zapier → **Zap Runs** → check the last run for an error. Most common: the Slack channel is private and Zapier isn't a member. Invite it. |

---

## Advanced option — self-hosted backend

If you'd rather run everything on your own infrastructure (no Formspree, full ownership of the database), the `backend/` folder contains a Node/Express service that does exactly that — stores submissions in SQLite and forwards them to your Slack webhook.

That path requires a developer comfortable with Terminal, Node.js, and deploying to a host like Render. See `backend/README.md` for the technical details. For most luxury-brand contact volumes (< 50/month), Formspree is the sensible choice — simpler, cheaper in developer time, and just as reliable.
