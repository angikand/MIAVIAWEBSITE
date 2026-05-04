# Stripe Setup — Online Payment for Experiences

This is the step-by-step for getting real payments flowing on the Miavia site. No coding, no Terminal, no developer needed. About 1 hour total spread across activating your Stripe account and creating one Payment Link per experience.

```
Member books → Formspree (email + Slack) → Stripe Payment Link → Confirmation page
                                            (member pays here)
```

---

## Part 1 — Create your Stripe account (~15 min)

### 1. Sign up

1. Open **https://dashboard.stripe.com/register**.
2. Fill in:
   - **Email** — your business email
   - **Full name** — Angelica Andryushkina
   - **Country** — France (or wherever Miavia is registered)
   - **Password** — strong, save in a password manager
3. Click **Create account**. Verify your email.

### 2. Stay in **Test mode** for now

You'll see a banner at the top that says "TEST MODE". Leave it on while we set up — no real money moves. We'll switch to live mode once everything is wired and you've done test purchases yourself.

### 3. Activate the account (when you're ready for real money)

To collect real payments later you'll need to verify your business identity:
1. In the dashboard left sidebar → **Activate payments**.
2. Provide:
   - Business type (Individual / Company / Non-profit)
   - Business address
   - Tax ID (SIRET if French company)
   - Bank account (IBAN) where Stripe will deposit your earnings
   - Photo ID (passport or French ID card)
3. Stripe takes 1–2 business days to verify. You can keep testing in Test mode while you wait.

**Important:** Don't activate yet if you're just testing. Keep going in Test mode.

---

## Part 2 — Create a Payment Link for each experience (~5 min each)

A Payment Link is a checkout URL Stripe gives you for a specific product. Members click it → they're sent to a Stripe-hosted payment page → they pay → Stripe sends them back to your site.

You'll create one Payment Link per experience. Skip any experience you don't want online payment for.

### How to create one Payment Link (do this 9 times)

1. In the Stripe dashboard left sidebar, click **Payment links** → **+ Create**.
2. Click **+ Add a product**.
3. Fill in:
   - **Name:** the experience name. e.g. `Truffle Hunting`
   - **Description:** short copy. e.g. `Half-day guided truffle hunt in the Var with expert guide and trained dog. Tasting included.`
   - **Image** (optional): upload a photo of the experience.
   - **Price:** the price you want to charge. e.g. `450 EUR`. Pick **One off** (not subscription).
4. Click **Add product**.
5. Scroll down to **After payment** → choose **Don't show confirmation page** (we have our own) → set:
   - **Redirect URL:** for now `http://localhost/#confirmation` (we'll update this once you have your live Vercel URL).
6. Optional but recommended:
   - Under **Options** → enable **Collect customers' phone numbers**.
   - **Custom fields**: don't bother, we collect everything in our form first.
7. Click **Create link** at the top right.
8. Stripe gives you a **URL** that looks like: `https://buy.stripe.com/test_aBC123...` — **copy this URL**.

### Repeat for each experience

Use these as a starting point — adjust the prices to whatever Miavia charges:

| Experience | Suggested price |
|---|---|
| Yoga Class (private session) | €150 |
| Wine Tasting (Red or White) | €200 per person |
| Wine Tasting (Champagne) | €250 per person |
| Truffle Hunting | €450 per group |
| Horse Riding | €200 per rider |
| Cooking Classes | €280 per person |
| Painting Class | €150 per person |
| Paintball | €120 per group |
| Massage Wellness | €180 (60 min) |
| Private Chef | €600 per evening |
| Stay Deposit (optional, for property pages) | €500 |

You can change the price any time from the Stripe dashboard — the URL stays the same.

---

## Part 3 — Paste the URLs into the website (~5 min)

Once you have your Payment Link URLs, open `index.html` in TextEdit (or any text editor).

Near the top, find this block:

```html
<script>
  ...
  window.MIAVIA_STRIPE_LINKS = {
    yoga:      '',  // e.g. 'https://buy.stripe.com/xxx'
    wine:      '',
    truffle:   '',
    horses:    '',
    cooking:   '',
    painting:  '',
    paintball: '',
    wellness:  '',
    chef:      '',
    stay:      ''
  };
</script>
```

Paste each URL between the quotes. Example:

```html
window.MIAVIA_STRIPE_LINKS = {
  yoga:      'https://buy.stripe.com/test_aBC123yoga',
  wine:      'https://buy.stripe.com/test_aBC123wine',
  truffle:   'https://buy.stripe.com/test_aBC123truffle',
  horses:    'https://buy.stripe.com/test_aBC123horse',
  cooking:   'https://buy.stripe.com/test_aBC123cook',
  painting:  'https://buy.stripe.com/test_aBC123paint',
  paintball: 'https://buy.stripe.com/test_aBC123paintball',
  wellness:  'https://buy.stripe.com/test_aBC123wellness',
  chef:      'https://buy.stripe.com/test_aBC123chef',
  stay:      ''  // leave blank to keep manual concierge invoicing for property bookings
};
```

Save the file. Do the same for `miavia-deploy/index.html`, `miavia-github/index.html`, and `miavia-github-full/index.html` so the deployed copy stays in sync. (Or just save the main `index.html` and re-copy.)

---

## Part 4 — Test it (~5 min)

1. Open the site in your browser.
2. Sign in (or create a test account).
3. Go to any experience detail page (e.g. Truffle Hunting).
4. Scroll to the booking form, fill in your name / email / date / guests, click **Continue to Payment**.
5. The page should redirect to Stripe's hosted payment page.
6. Use Stripe's test card to pay: card number **`4242 4242 4242 4242`**, any future date for expiry, any 3-digit CVC, any postal code.
7. Click Pay. Stripe redirects you back to the site.
8. **Check Slack** — the booking inquiry from Formspree should be in `#website-contact`.
9. **Check Stripe** dashboard → **Payments** — the test payment should be there with the booking number you generated.

If both arrive, you're done.

---

## Part 5 — Switch to live mode (after deploy)

Once the site is on Vercel and you've activated your Stripe account:

1. In Stripe dashboard, top right → toggle **Test mode** OFF.
2. **Re-create each Payment Link in Live mode** (Stripe doesn't auto-port them). Same prices, same products.
3. Update each URL in `index.html` — Live URLs start with `https://buy.stripe.com/` (no `test_`).
4. Re-deploy the site.
5. Update each Payment Link's **Redirect URL** from `localhost` to your real Vercel domain, e.g. `https://miavia.vercel.app/#confirmation`.

---

## What flows where

| Action | Lands in |
|---|---|
| Member books an experience | Formspree (email + Slack) AND Stripe Payment Links page |
| Member pays | Stripe dashboard → **Payments** |
| Member completes payment | Returned to your `#confirmation` page |
| Money | Stripe → your bank account (after activation), usually 7-day delay on first payout |

The `client_reference_id` parameter we send to Stripe (the booking number, e.g. `MV123456`) is also visible in Stripe → Payments. That's how you correlate a Stripe payment with the Formspree submission of the same booking number.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Click Continue → stays on the form | The Stripe URL for that experience is missing or has a typo. Check the `MIAVIA_STRIPE_LINKS` block in `index.html`. |
| Stripe "Test mode" warning on the live site | You're using a `test_` URL on production. Re-create the link in Live mode and update the URL. |
| Member paid but you didn't get a Slack notification | The Formspree POST happens BEFORE the Stripe redirect. Check Formspree dashboard. If it's not there, the form wasn't submitted properly — check the browser console. |
| Want to change a price | In Stripe dashboard → Payment links → open the link → edit price. URL stays the same. |
| Want to disable an experience temporarily | Set its URL to `''` in `MIAVIA_STRIPE_LINKS`. Form falls back to "thank you" page without payment. Concierge handles manually. |

---

## Files

- This guide.
- `index.html` — `MIAVIA_STRIPE_LINKS` config block lives at the top (in the `<head>`).
- `CONTACT_FORM_SETUP.md` — Formspree setup (already done).
- `MIAVIA_WEBSITE.md` — full site implementation record.
