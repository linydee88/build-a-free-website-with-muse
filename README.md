# Build a Free Website with Muse

A step-by-step guide to building, hosting, and running a real website for $0/month using Muse (your AI assistant) and GitHub Pages. No Wix, no Squarespace, no Stan Store, no monthly fees.

This guide was written from a real 4-day build: a tarot reader's full business website with product pages, Stripe and PayPal checkout, custom domain, and SEO, all built by chatting with Muse.

---

## What You Need

- A GitHub account (free at github.com)
- Muse (the AI assistant; free plan works)
- A domain name (optional; ~$12/year from any registrar, or use a free `yourname.github.io` address)
- Zero coding experience (Muse writes the code; you direct the design)

## What You Get

- A fast, mobile-friendly website you fully own
- Free hosting forever via GitHub Pages (around since 2008, rock solid)
- Free HTTPS/SSL certificate
- Take payments via Stripe Payment Links and PayPal (no backend needed)
- Total monthly cost: $0

---

## Step 1: Plan Your Pages

Before touching code, tell Muse what pages you need. Example prompt:

> "I need a website with these pages: Home, About Me, a products page with 5 items, FAQ, Contact, and Terms of Service. It's a single-page site using hash routing like #/about and #/products."

Muse will scaffold the HTML structure. Iterate on it: "move the About hero image left," "make the buttons gold," etc.

## Step 2: Design Each Section

Work page by page. Useful prompts:

- "Make me a mobile menu with these links: Home, About, Products, FAQ, Contact"
- "Make a hero banner (your hero is the main banner at the top of your page, the first thing visitors see, so make it pretty) for the homepage, dark green and gold, with my tagline"
- "Generate a hero banner image, wide and short, with [describe what you want]"
- "Make product cards with a thumbnail on the left, title and description on the right, and a price badge"
- "Add two buttons under each product: Pay with Card and Pay with PayPal"

**Tip:** Keep mobile and desktop designs separate from the start. Use separate images and CSS per breakpoint so editing one never breaks the other.

## Step 3: Generate Your Images

Muse can generate images, or you can bring your own:

- "Generate a square product thumbnail for [product name], dark green and gold tarot theme"
- "Generate a wide hero banner (the main image at the top of your page), 5:1 ratio, with [description]"

Save images in an `assets/` folder in your project.

## Step 4: Push to GitHub Pages

1. Create a new public repository on GitHub (e.g. `my-website`)
2. Ask Muse to push your site files to it
3. In the repo: Settings > Pages > Deploy from branch > `main` > Save
4. Your site is live at `https://yourusername.github.io/my-website`

## Step 5: Connect Your Custom Domain (Optional)

1. In the repo: Settings > Pages > Custom domain > enter `yourdomain.com` > Save
2. At your domain registrar's DNS settings, add:
   - An `A` record pointing to GitHub's IPs, or
   - A `CNAME` record: host `www`, value `yourusername.github.io`
3. Wait for DNS to propagate (minutes to hours)
4. GitHub auto-provisions your free HTTPS certificate

## Step 6: Clean Subdomain Links (Optional but Powerful)

Instead of sharing `yourdomain.com/#/products` in your social bios, create short links like `order.yourdomain.com`:

1. Create a tiny new GitHub repo (e.g. `order.yourdomain.com`)
2. Add an `index.html` with a redirect:
```html
<!DOCTYPE html>
<html><head>
<meta http-equiv="refresh" content="0; url=https://yourdomain.com/#/products">
</head><body>
<script>window.location.replace("https://yourdomain.com/#/products");</script>
</body></html>
```
3. Add a `CNAME` file containing `order.yourdomain.com`
4. Enable GitHub Pages on the repo
5. Add a DNS `CNAME` record: host `order`, value `yourusername.github.io`

Repeat for any shortcut you want (`library.yourdomain.com`, `book.yourdomain.com`, etc.)

## Step 7: Take Payments with No Backend

### Stripe Payment Links (recommended)
1. Create a Stripe account (free; they take ~2.9% + 30c per sale)
2. Dashboard > Payment Links > Create payment link for each product
3. Add custom fields (e.g. "Your questions," "Your email") so buyers send you what you need
4. Paste the `https://buy.stripe.com/...` URLs into your site's buttons
5. For discounts: create a coupon in Stripe, then enable "allow promotion codes" on the payment link

Stripe Payment Links support cards, Apple Pay, and Google Pay automatically.

### PayPal
1. Create PayPal payment links in your PayPal Business account
2. Paste the `https://www.paypal.com/ncp/payment/...` URLs into your PayPal buttons
3. Note: PayPal's simple links don't support coupon codes; for a sale price, create a separate link at the sale amount

## Step 8: Favicon and SEO

- **Favicon:** Save your logo as `assets/favicon.png` (and `.ico`), then add to your `<head>`:
```html
<link rel="icon" type="image/png" href="assets/favicon.png">
```
- **SEO:** Add a meta description so Google can index you properly:
```html
<meta name="description" content="One sentence describing your site and what you offer.">
<meta property="og:title" content="Your Site Name">
<meta property="og:description" content="One sentence for social shares.">
```

## Step 9: Ditch the Subscriptions

Once your site handles what Wix/Squarespace/Stan Store did for you, cancel them:

- Export anything you need first (customer lists, content)
- Turn off auto-renew, then cancel
- Keep your domain registration wherever it is (you only need DNS access)
- Savings: Wix (~$20-40/mo) + Stan Store (~$29/mo) = hundreds per year back in your pocket

---

## Fine Details That Make It Feel Professional

These are the small things that separate a "homemade" site from one that feels polished:

### Hash Routing with Working Back Button
Use hash routes (`#/about`, `#/products`) and a JavaScript router. Key detail: when a visitor clicks a product, then hits the browser back button, they should land back on the listing page **at the same scroll position** they left. Save `window.scrollY` before navigating to a detail view, restore it on back.

### Detail Pages
Each product gets its own view (`#/product/widget`) with:
- A circular back button (top-left) that returns to the listing
- Full description, terms, and order buttons top AND bottom (so buyers never have to scroll up to buy)
- A currency notice if you sell internationally ("Prices are in USD...")

### Buttons That Convert
- **Order buttons first.** On mobile, put your buy button before your contact button. People scroll and buy; contact is for later.
- **Show payment logos.** Small Visa, Mastercard, Apple Pay, Google Pay badges on your pay buttons. Seeing a familiar logo is a mental shortcut to "this is easy, I'll do it."
- **Two payment options, side by side:** "Pay with Card" (Stripe) and "Pay with PayPal." Let the buyer choose.

### Mobile Menu That Doesn't Suck
- Keep it simple: 2-column grid or a clean vertical list
- Match your site colors (don't let it default to white/black)
- Include every page, including new ones you add later

### Centering and Spacing
- Center your hero text; it reads as more intentional than left-aligned on mobile
- Give buttons breathing room (min 10px gaps); cramped buttons feel cheap
- Price badges: high contrast (white badge, dark text, or vice versa) so the price pops

### The "One More Click" Rule
Every extra click between "I want this" and "I bought this" loses people. Count the clicks from your social bio to completed purchase. If it's more than 3, shorten it with subdomain redirects (Step 6).

---

## Lessons Learned

- **Verify before claiming.** When something looks broken, check the live site with a fresh fetch before changing code. Browser cache causes most "it's not working" false alarms; hard-refresh (Ctrl+F5) first.
- **Mobile and desktop stay separate.** Separate images, separate elements, separate CSS per breakpoint. Editing one should never shift the other.
- **Your repo is the source of truth.** Every change goes through git. If something breaks, you can always roll back.
- **Binary files need care.** Some push tools skip images; verify image URLs return 200 after pushing.
- **Fiddling is the job.** Expect to iterate. Each round makes it better, and it costs nothing but time.

---

## Real Example

This guide comes from [linydee.com](https://linydee.com), a tarot reader's site built in 4 days with Muse: 5 product pages with Stripe + PayPal checkout, custom subdomains (`order.linydee.com`, `library.linydee.com`), SEO, and a full About/FAQ/Books/Library section. Monthly cost went from ~$70 (Wix + Stan Store) to $0.

---

Built with Muse. If this helped you, star the repo.
