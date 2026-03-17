# IEEE Pitt Student Branch — Website

The official website for the IEEE University of Pittsburgh Student Branch.  
Live site: [https://pittssoeieee.github.io/ieeepitt.github.io/](https://pittssoeieee.github.io/ieeepitt.github.io/)

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [How to Edit the Site](#how-to-edit-the-site)
    - [Editing Events](#editing-events)
    - [Editing Merch](#editing-merch)
    - [Updating the GroupMe Link](#updating-the-groupme-link)
    - [Updating the Mailing List](#updating-the-mailing-list)
    - [Updating Contact Info & Footer](#updating-contact-info--footer)
3. [How to Add a Logo](#how-to-add-a-logo)
4. [How to Add Merch Product Photos](#how-to-add-merch-product-photos)
5. [Deploying Changes](#deploying-changes)
6. [Setting Up Integrations (First-Time)](#setting-up-integrations-first-time)
    - [Stripe Payment Links](#stripe-payment-links)
    - [Google Form Mailing List](#google-form-mailing-list)
7. [Style & Branding Reference](#style--branding-reference)
8. [Troubleshooting](#troubleshooting)
9. [Future Improvements](#future-improvements)

---

## Project Structure

```
/
├── index.html       # The entire website — HTML, CSS, and JS in one file
├── README.md        # This file
└── img/             # Create this folder when you add images
    ├── logo.png     # Your branch logo (optional, see section below)
    ├── tshirt.jpg   # Product photos go here
    └── ...
```

> **Key rule:** All content editors only ever need to touch the `EDITABLE DATA` block near the bottom of `index.html`. Everything else is layout and styling code that does not need to change.

---

## How to Edit the Site

Open `index.html` in any text editor (VS Code is recommended). Scroll to the `<script>` tag near the bottom of the file. You will see a clearly marked section:

```js
/* ================================================================
 *  ✏️  EDITABLE DATA  —  The only section editors need to change.
 * ================================================================ */
```

All editable content lives between this comment and the one that reads `RENDERING LOGIC`. **Do not edit anything below the `RENDERING LOGIC` comment.**

---

### Editing Events

Find the `EVENTS` array. Each event is a JavaScript object inside the array. Add, remove, or modify objects to control what appears on the site. Events are automatically sorted by date, so order in the file does not matter.

**Adding an event:**
```js
const EVENTS = [
  // Copy and paste this block for each new event:
  {
    title:    "Your Event Title",
    date:     "2026-05-15",       // Format: YYYY-MM-DD  (required for sorting)
    time:     "6:00 PM",          // Display only — any string works
    location: "Benedum Hall 219",
    desc:     "A short description of the event shown on the card.",
    link:     "https://your-rsvp-link.com",  // Use "#" if there is no link
    linkText: "RSVP"              // The button label. Defaults to "Learn More" if omitted.
  },
  // ...other events
];
```

**Removing an event:** Delete the entire object including its surrounding `{ }` and the comma after it.

**Hiding all events temporarily:** Set the array to empty: `const EVENTS = [];`  
The site will automatically display a "No upcoming events" message.

---

### Editing Merch

Find the `MERCH` array. Each item is a JavaScript object. Add, remove, or modify objects to control what appears in the store.

**Adding a product:**
```js
const MERCH = [
  // Copy and paste this block for each new product:
  {
    name:      "Product Name",
    desc:      "Short description shown on the product card.",
    price:     "$25.00",          // Display string only — Stripe handles the real price
    stripeUrl: "https://buy.stripe.com/YOUR_LINK_HERE",  // From Stripe Dashboard
    image:     "img/product.jpg"  // Path to photo. Use "" for a placeholder box.
  },
  // ...other products
];
```

**Removing a product:** Delete the entire object including its surrounding `{ }` and the comma after it.

**Temporarily hiding a product without deleting it:** Add `//` before every line of the object to comment it out.

---

### Updating the GroupMe Link

Find this line near the top of the editable block:

```js
const GROUPME_LINK = "https://groupme.com/join_group/YOUR_GROUP_ID/YOUR_TOKEN";
```

Replace the URL with your current GroupMe join link.

**How to get the GroupMe join link:**
1. Open the GroupMe app
2. Tap your group → tap the group name at the top → **Share**
3. Copy the join link and paste it in place of the placeholder URL

> If your GroupMe group changes or gets a new invite link, just update this one line and redeploy.

---

### Updating the Mailing List

Find these three lines:

```js
const MAILING_LIST_FORM_URL   = "";
const MAILING_LIST_NAME_FIELD  = "entry.000000000";
const MAILING_LIST_EMAIL_FIELD = "entry.111111111";
```

These connect the subscribe form to your Google Form. See [Google Form Mailing List](#google-form-mailing-list) in the setup section for how to find the correct values.

> **If `MAILING_LIST_FORM_URL` is left empty (`""`), clicking Subscribe will open the user's default email client as a fallback.** This is fine as a temporary measure before the form is set up.

---

### Updating Contact Info & Footer

The footer contains the branch email address and a link to ieee.org. To change the email:

1. Search the file for `ieeepitt@pitt.edu` — it appears in two places
2. Replace both instances with your actual email address

To change the footer text (school name, year, etc.), search for `Swanson School of Engineering` or `© 2026` and update accordingly.

---

## How to Add a Logo

1. Add your logo image file to the `img/` folder in the repository (create the folder if it does not exist). Name it `logo.png` or any filename you prefer.
2. In `index.html`, find this comment in the `<nav>` section:
   ```html
   <!-- LOGO: To use your own logo image, replace the two spans below with:
        <img src="img/logo.png" alt="IEEE Pitt" style="height:36px;" /> -->
   ```
3. Delete the two `<span>` lines directly below the comment:
   ```html
   <span class="logo-badge">IEEE</span>
   <span class="logo-text">Pitt Student Branch</span>
   ```
4. Replace them with:
   ```html
   <img src="img/logo.png" alt="IEEE Pitt" style="height:36px;" />
   ```
   Adjust the filename and height as needed.

---

## How to Add Merch Product Photos

1. Create an `img/` folder in the repository if it does not already exist.
2. Upload your product photo (`.jpg` or `.png`) into that folder.
3. In the `MERCH` array, set the `image` field to the relative path:
   ```js
   image: "img/tshirt.jpg"
   ```
4. If you leave `image` as an empty string (`""`), a gray placeholder box is shown instead.

**Recommended image specs:** Square aspect ratio (1:1), at least 600×600px, under 500KB. You can use [squoosh.app](https://squoosh.app) to compress images for free.

---

## Deploying Changes

All changes go live automatically when you push or upload to the `main` branch of this repository. GitHub Pages rebuilds the site within about 60 seconds.

**Option A — Edit directly in GitHub (easiest for small changes):**
1. Open `index.html` in the repository on GitHub
2. Click the pencil **Edit** icon in the top right
3. Make your changes
4. Click **Commit changes** at the bottom

**Option B — Edit locally and push (recommended for larger changes):**
```bash
# Clone the repo (first time only)
git clone https://github.com/YOUR_ORG/ieeepitt.github.io.git

# Make your changes in index.html, then:
git add .
git commit -m "Update events for April"
git push
```

**Option C — Upload files via GitHub UI (for adding images):**
1. Navigate to the `img/` folder (or root) in the repository
2. Click **Add file → Upload files**
3. Drag in your images and commit

---

## Setting Up Integrations (First-Time)

### Stripe Payment Links

Stripe Payment Links let customers check out securely without any backend code.

1. Create a free account at [stripe.com](https://stripe.com)
2. In the Stripe Dashboard, go to **Payment Links → Create payment link**
3. Add a product, set the price, and click **Create link**
4. Copy the URL (it starts with `https://buy.stripe.com/...`)
5. Paste it into the `stripeUrl` field for the matching product in the `MERCH` array

> Repeat this for each product. Each product gets its own unique Stripe link.  
> Stripe charges a small transaction fee (~2.9% + $0.30) per sale — there is no monthly cost.

---

### Google Form Mailing List

1. Go to [forms.google.com](https://forms.google.com) and create a new form
2. Add two **Short answer** questions: one for **Name**, one for **Email**
3. Click the three-dot menu (⋮) in the top right → **Get pre-filled link**
4. Fill in dummy values for Name and Email → click **Get link** → copy the URL

   The URL will look like this:
   ```
   https://docs.google.com/forms/d/e/XXXXXXXXXXXX/viewform?usp=pp_url&entry.123456789=DummyName&entry.987654321=dummy@email.com
   ```

5. From that URL, extract:
    - **Form base URL:** everything up to and including `/formResponse`  
      Change `viewform` to `formResponse` — e.g.:  
      `https://docs.google.com/forms/d/e/XXXXXXXXXXXX/formResponse`
    - **Name entry ID:** the `entry.XXXXXXXXX` before your dummy name value
    - **Email entry ID:** the `entry.XXXXXXXXX` before your dummy email value

6. Paste all three into `index.html`:
   ```js
   const MAILING_LIST_FORM_URL   = "https://docs.google.com/forms/d/e/XXXXXXXXXXXX/formResponse";
   const MAILING_LIST_NAME_FIELD  = "entry.123456789";
   const MAILING_LIST_EMAIL_FIELD = "entry.987654321";
   ```

7. To see responses, open the form in Google Forms and click the **Responses** tab. You can also click the Google Sheets icon to export all responses to a spreadsheet.

---

## Style & Branding Reference

The site uses IEEE's official brand colors. If you ever need to regenerate or restyle any part of the site using an AI tool, include this in your prompt:

> *"Use IEEE official brand colors: Primary Blue `#006699`, Navy `#003057`, Gold `#F7A800`. Font: Inter. Clean white card layout with a navy header and footer."*

| Token | Hex | Used For |
|---|---|---|
| IEEE Blue | `#006699` | Buttons, card accents, links |
| IEEE Navy | `#003057` | Header, footer, event date badges |
| IEEE Gold | `#F7A800` | Accent color, CTA buttons, dividers |
| Light Blue | `#E8F4F8` | Alternate section backgrounds |
| White | `#ffffff` | Cards, main background |

---

## Troubleshooting

**Site shows a 404 after deploying**  
→ Make sure the file is named exactly `index.html` (lowercase). GitHub Pages requires this exact filename as the entry point.

**Changes aren't showing up on the live site**  
→ Wait 60–90 seconds after committing — GitHub Pages has a short build delay. Also try a hard refresh (`Ctrl+Shift+R` / `Cmd+Shift+R`) to clear your browser cache.

**The mailing list subscribe button does nothing**  
→ Check that `MAILING_LIST_FORM_URL` is not an empty string. Also verify the entry IDs match your form exactly — they are case-sensitive.

**Stripe "Buy Now" button links to a dead page**  
→ The placeholder URL `https://buy.stripe.com/YOUR_LINK_HERE` needs to be replaced with a real link from your Stripe Dashboard. See the Stripe setup section above.

**Images aren't showing up**  
→ Double-check that the filename and path in the `image` field exactly match the file you uploaded, including capitalization. File paths are case-sensitive on GitHub Pages (e.g. `img/Tshirt.jpg` ≠ `img/tshirt.jpg`).

**I want to ask an AI to make changes to the site**  
→ Paste the full contents of `index.html` into Claude (or another AI tool) and describe what you want changed. It can regenerate the file with your requested edits while preserving the rest of the site.

## Future Improvements

It is the constitutional responsibility of the webmaster to maintain the operation of this site throughout the duration of their elected semester. It is also imperative that the webmaster makes any necessary improvements to the site as they deem fit. Potential improvements include:

1. Adding an officer page to the website with pictures and descriptions of the current admin.
2. To add a board-created Pitt IEEE logo to the website.
3. To update and maintain the README for future site contributors.
4. Refactoring the HTML behavior / functions to improve performance.
