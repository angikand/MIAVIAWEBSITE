# Membership Approval Workflow

How Miavia handles new member applications: from sign-up to approval to welcome email.

```
Applicant signs up → "Application Received" page → Slack alert
   ↓
Boss/concierge reviews in Clerk dashboard
   ↓
Boss sets membershipStatus = approved
   ↓
(Automatic email to applicant — see Part 3)
   ↓
Applicant signs in at miavia.com → full member access
```

---

## Part 1 — How a new application looks to you

When someone fills out the sign-up form on miavia.com:

1. They enter the 7 fields (First Name, Last Name, Email, Password, Country Code, Phone, Birthday, Language).
2. They get a 6-digit verification code by email.
3. After they enter it correctly:
   - Their Clerk user is created with `unsafeMetadata.membershipStatus = 'pending'`.
   - They are **immediately signed out** — no member access yet.
   - They land on a dark "Application Received" page that says they'll hear back within 48 hours.
4. **Slack `#website-contact`** gets a message like:

   ```
   New Miavia membership application — Sarah Lambert
   Type: Membership application
   Name: Sarah Lambert
   Email: sarah@example.com
   Phone: +33 6 12 34 56 78
   Birthday: 1992-03-14
   Language: English
   Applied at: 2026-04-30T08:14:22Z
   Approval link: https://dashboard.clerk.com
   ```

5. **Formspree inbox** also receives the same details (search `https://formspree.io/forms/xdaybonp/submissions`).

This means even if you miss Slack, every application is preserved in Formspree forever.

---

## Part 2 — How to approve (or reject) an applicant

### Approve

1. Open https://dashboard.clerk.com → sign in → choose your Miavia application.
2. Left sidebar → **Users**. Find the applicant by email (newest first).
3. Click their row to open their profile.
4. Scroll to the **Metadata** section (often near the bottom).
5. Find the **Unsafe metadata** sub-section. You'll see something like:

   ```json
   {
     "birthday": "1992-03-14",
     "language": "English",
     "countryCode": "+33",
     "phone": "612345678",
     "phoneE164": "+33612345678",
     "membershipStatus": "pending",
     "appliedAt": "2026-04-30T08:14:22Z"
   }
   ```

6. Click **Edit** on the unsafe metadata.
7. Change `"membershipStatus": "pending"` to `"membershipStatus": "approved"` and add `"approvedAt": "2026-04-30T17:02:00Z"` (today's date in ISO format — copy-paste from `https://www.utctime.net/`).
8. Click **Save**.

That's it. The next time the user signs in at miavia.com, they have full member access — booking forms unlock, contact form unlocks, everything.

### Reject

If you don't want to approve someone:
- **Soft option:** leave their `membershipStatus` as `pending` and never email them. They can't access anything. Most concierge-graceful.
- **Hard option:** click **Delete user** at the bottom of the user's profile page. Their email becomes available to register again later.
- **Block option:** click **Lock account**. Their sign-in attempts will fail with a "your account has been locked" message.

---

## Part 3 — Automated approval email (optional setup, ~15 min)

The site already gates the booking forms based on `membershipStatus`. But for the cleanest UX you want the applicant to receive an email the moment you mark them approved. Recommended path: a Clerk webhook → Make.com workflow → Gmail.

### Option A — Make.com (easiest, no code)

1. Sign up at https://www.make.com (free tier is enough — 1,000 ops/month).
2. Click **Create a new scenario**.
3. **Trigger:** search for **"Webhooks"** → choose **"Custom webhook"** → **Add**. Make.com gives you a unique URL like `https://hook.us1.make.com/abc123xyz...`.
4. **Action:** add a step → search **"Gmail"** → choose **"Send an email"** → connect your Miavia Gmail (e.g., `info@miavia.com`).
5. In the email step:
   - **To:** `{{1.data.email_addresses[0].email_address}}` (this pulls from the webhook payload — Make's UI will let you click into the structure)
   - **Subject:** `Welcome to Miavia — your membership is approved`
   - **Body (HTML):**

     ```html
     <p>Dear {{1.data.first_name}},</p>

     <p>It is our great pleasure to welcome you to Miavia.</p>

     <p>Your membership has been approved. You may now sign in at
     <a href="https://miavia.com">miavia.com</a> to begin booking experiences
     and reserving stays at our destinations.</p>

     <p>Should anything need attention, our concierge is one message away —
     simply use the Contact page once signed in.</p>

     <p>Welcome to the family.</p>

     <p>— The Miavia Team</p>
     ```

6. Add a **Filter** between the trigger and Gmail: only run when `data.unsafe_metadata.membershipStatus = approved`. This prevents the email from firing on every metadata change (e.g., when a user updates their birthday).
7. **Save the scenario** and turn it ON.
8. Now go to Clerk: **Webhooks** (left sidebar) → **Add Endpoint**.
   - **Endpoint URL:** paste the Make.com webhook URL from step 3.
   - **Subscribe to events:** check **`user.updated`** only.
   - Click **Create**.
9. Test it: in the Clerk dashboard, find a test user with `membershipStatus: pending`, change it to `approved`, save. The Make.com scenario should fire and Gmail should send the email.

### Option B — Resend (more bespoke, requires a tiny bit of JS)

If you'd rather not use Make.com, you can use **Resend** (https://resend.com — free for 3,000 emails/month) and a Netlify Function. Email me/Slack me if you want this setup — it's 30 min of work and gives you full HTML email control.

---

## Part 4 — Existing members (who signed up before the approval flow was added)

Anyone who signed up before April 30, 2026 doesn't have `membershipStatus` set in their metadata. To grandfather them in:

1. Clerk dashboard → **Users**.
2. For each existing user (probably just you and the boss), open their profile.
3. **Edit unsafe metadata** → add `"membershipStatus": "approved"` to the JSON.
4. Save.

Without this, even existing members will see "Application under review" when they try to book.

---

## Part 5 — Quick reference

| Action | Where |
|---|---|
| Sign-up form | `miavia.com` → menu → Become a Member |
| Application alert (Slack) | `#website-contact` |
| Application alert (email) | Formspree → `xdaybonp` submissions |
| Approve / reject | https://dashboard.clerk.com → Users → Edit metadata |
| Approval email automation | Make.com (Part 3) |
| Member sign-in | `miavia.com` → menu → Sign In |

---

## Part 6 — What status values mean in code

The site reads `unsafeMetadata.membershipStatus` from each Clerk user. Possible values:

- **`pending`** — applied but not approved. Booking + Contact forms show a "Application under review" panel.
- **`approved`** — full member. All features unlock.
- **(no value)** — treated as `pending` (defensive default).

Set as `publicMetadata.membershipStatus` instead of `unsafeMetadata` if you want it visible to other users — but for Miavia's purposes `unsafeMetadata` is the right place (only the user themselves and Clerk admins can see it).
