# UPEI SMCSS Website — Competition Handoff

This repository contains the static SMCSS website prepared for the UPEI School of Mathematical and Computational Sciences Society website competition.

The project is intentionally simple to hand off: the site is a static HTML/CSS/JavaScript website with a small editable content layer (`content.js`). There is no database, server-side application, PHP, SQL, or build system required.

---

## 1. What is included

```text
SMCSS-FINAL-HANDOFF/
├── index.html      # Complete website: structure, styling, interaction
├── content.js      # Editable content layer, especially event data
└── README.md       # This handoff and maintenance guide
```

### Main sections

The website contains the seven required competition sections:

1. **Home** — what SMCSS is, who it serves, location, signup and event access
2. **About SMCS** — community, learning, fun and society information
3. **Events** — current-event Linktree hub plus optional direct event cards
4. **Executives** — executive-role cards ready for the confirmed roster
5. **Services** — locker rental information and rules
6. **Resources** — academic help, student policies, SMCS information and UPEI calendar
7. **Contact** — email, Instagram, signup link and contact form

The competition brief requires these sections and specifically asks for an extendable codebase where adding and deleting events is straightforward. This project keeps event data separate from the page layout so completed events can be removed without rewriting the page structure.

---

# 2. Important: how the website should be deployed

## Recommended production architecture

**Do not try to upload this entire `index.html` file into Squarespace as if Squarespace were a normal file host.**

The recommended architecture for this competition is:

```text
Visitor
   │
   ▼
smcss domain
   │
   ▼
Squarespace DNS
   │
   ▼
Vercel
   │
   ▼
This static website
```

This matches the competition brief, which allows any tech stack, asks that the website remain compatible with the existing Squarespace-hosted domain, suggests Vercel for deployment, and lists transfer of the Vercel project plus connection of the domain through Squarespace DNS as part of the winner handoff.

### What Squarespace is doing here

Squarespace can remain the place where the SMCSS domain/DNS is managed.

Vercel hosts the actual website files.

The domain is then connected from Squarespace to the Vercel deployment.

This means the final public website can still use the official SMCSS domain even though the website itself is hosted by Vercel.

---

# 3. Does this website work with Squarespace?

## Yes — for the competition's intended setup.

The website is a static HTML/CSS/JavaScript site, so it does not require a server-side runtime. It can be deployed to Vercel and the Squarespace-managed domain can point to that deployment through DNS.

Squarespace's current documentation also confirms that a third-party domain can be connected to a Squarespace site through DNS, and that Squarespace provides the CNAME/A records required for the connection.

### Important distinction

There are two different meanings of "Squarespace compatible":

### A. Squarespace domain + external hosting — RECOMMENDED

```text
Squarespace DNS → Vercel → SMCSS website
```

**Recommended for this project.**

Advantages:

- Preserves the custom design exactly.
- Keeps the full HTML/CSS/JavaScript implementation.
- Keeps the code in GitHub.
- Works naturally with Vercel deployment.
- Fits the competition's winner-handoff instructions.
- Squarespace remains responsible for the domain/DNS connection.

### B. Rebuilding/embedding the website inside Squarespace — POSSIBLE, but not recommended

Squarespace supports custom HTML/CSS and, on eligible plans, JavaScript through code blocks/code injection. However, Squarespace does not provide a normal "upload this static website ZIP and import it" workflow for this type of custom project.

Rebuilding the whole site inside Squarespace would require placing/reworking the markup and scripts into Squarespace pages/code blocks and potentially adapting CSS and JavaScript to Squarespace's page structure.

That could change the visual behaviour and make future maintenance more complicated.

**For the competition, use Vercel + Squarespace DNS instead.**

---

# 4. Local development

Open Terminal and enter:

```bash
cd ~/Downloads/SMCSS-V23
```

Start the local server:

```bash
python3 -m http.server 8000
```

Open:

```text
http://localhost:8000
```

For iPhone testing on the same Wi-Fi network:

```bash
ipconfig getifaddr en0
```

If the Mac reports `192.168.2.35`, for example, open:

```text
http://192.168.2.35:8000
```

If port 8000 is already being used:

```bash
pkill -f "python3 -m http.server" 2>/dev/null || true
python3 -m http.server 8000
```

---

# 5. How to manage events

## Recommended source of truth

SMCSS currently publishes upcoming events through the official Linktree:

```text
https://linktr.ee/upeismcss
```

The website therefore sends visitors to Linktree instead of hard-coding dates that can become outdated.

## Optional direct event cards

The project also supports direct event cards through `content.js`.

Open:

```text
content.js
```

Find:

```js
window.EVENTS = [
  // {
  //   title: "Math & Coding Night",
  //   date: "2026-10-20",
  //   time: "6:00 PM",
  //   href: "https://example.com/register"
  // }
];
```

To add an event, uncomment/copy the object and edit it:

```js
window.EVENTS = [
  {
    title: "Math & Coding Night",
    date: "2026-10-20",
    time: "6:00 PM",
    href: "https://example.com/register"
  }
];
```

To add another event, add another object separated by a comma:

```js
window.EVENTS = [
  {
    title: "Math & Coding Night",
    date: "2026-10-20",
    time: "6:00 PM",
    href: "https://example.com/register"
  },
  {
    title: "Study Session",
    date: "2026-10-24",
    time: "5:00 PM",
    href: "https://example.com/study"
  }
];
```

To remove a completed event, delete its object.

### What happens when EVENTS is empty?

Nothing extra is shown. The normal Linktree event hub remains the main event destination.

### What happens when EVENTS has events?

The direct event cards appear automatically. No HTML or CSS editing is required.

This is intentional: future maintainers should be able to add/remove event objects without modifying the page layout.

---

# 6. Executive roster management

The current competition build intentionally does **not** invent or hard-code executive names because the official current roster/photos were not supplied in the competition information available for this build.

The executive cards are therefore prepared with roles such as:

- President
- Vice-President
- Treasurer
- Secretary
- Activities Director
- Faculty Adviser

When the official roster is supplied, update the corresponding executive card in `index.html` with the confirmed:

- name
- role
- program
- email, if appropriate
- photograph

Do not publish a student's name, photo, program or contact information without the society's confirmation/permission.

The modal/photo placeholder is deliberately there so the visual structure is ready before official photos are inserted.

---

# 7. Locker information

The website currently reflects the supplied SMCSS competition information:

- **Price:** $10 per semester
- **Deposit:** $10 refundable deposit when the locker rules are followed
- **Rental period:** one semester
- **Location:** bottom floor of Cass Science Hall
- **How to rent:** email `smcss@upeisu.ca`
- **Food rule:** no food in lockers for extended periods because food can cause mold, bad smells and bugs
- **End-of-semester rule:** lockers must be cleaned out and locks removed by the last day of classes or the $10 deposit is not refunded

Eligibility was not specified in the supplied SMCSS information, so the website does not invent an eligibility rule.

---

# 8. Contact information

Current supplied SMCSS contact information:

- Email: `smcss@upeisu.ca`
- Instagram: `@upeismcss`
- Instagram URL: `https://www.instagram.com/upeismcss/`

The contact form uses a `mailto:` workflow. It opens the visitor's email application and prepares a message addressed to `smcss@upeisu.ca`.

### Important limitation

This is not a server-side form/database. It does not store submissions in a backend.

If SMCSS later wants a true web form with stored submissions, spam protection, staff notifications, or a dashboard, replace the mailto workflow with a form service or backend.

---

# 9. SMCSS signup

The Join SMCSS buttons use the supplied Google Form.

If the society changes its signup form in the future, search `index.html` for the Google Forms URL and replace it in each occurrence.

---

# 10. Resources

The resource cards currently point to official UPEI sources:

### Help Centres

UPEI SMCS Help Centres:

```text
https://www.upei.ca/school-of-mathematical-and-computational-sciences/help-centres
```

### Student Policies

```text
https://www.upei.ca/school-of-mathematical-and-computational-sciences/student-policies
```

### SMCS

```text
https://www.upei.ca/school-of-mathematical-and-computational-sciences
```

### UPEI Calendar

```text
https://calendar.upei.ca/current/chapter/school-of-mathematical-computational-sciences/
```

These should be periodically checked because university URLs/content can change.

---

# 11. Accessibility and responsive behaviour

The site includes:

- semantic HTML sections
- a skip-to-content link
- visible keyboard focus styles
- responsive layouts for desktop/tablet/mobile
- reduced-motion handling for major motion effects
- external-link `rel="noopener"` protection
- form labels and required fields
- `aria-label`/ARIA attributes where useful
- horizontal mobile navigation
- no dependency on a JavaScript framework

Before production launch, test the final deployed version on:

- desktop Chrome
- desktop Safari
- iPhone Safari
- Android Chrome
- keyboard navigation
- reduced-motion browser settings

---

# 12. Browser favicon / π mark

The browser tab uses a minimal white π favicon so the SMCSS identity remains recognizable without adding a large square graphic.

The main hero also contains the π mathematical mark as part of the site's visual identity.

---

# 13. Deployment to GitHub + Vercel

## GitHub

Create a repository such as:

```text
smcss-website
```

Put these files at the repository root:

```text
index.html
content.js
README.md
```

Then commit and push.

Example:

```bash
git init
git add index.html content.js README.md
git commit -m "Initial SMCSS website"
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY_URL
git push -u origin main
```

Replace `YOUR_GITHUB_REPOSITORY_URL` with the real GitHub repository URL.

## Vercel

1. Sign in to Vercel.
2. Import the GitHub repository.
3. Because this is a static site, no framework is required.
4. Deploy.
5. Confirm the Vercel URL works.
6. Test all sections and external links.
7. Add the official SMCSS domain in Vercel's Domains settings when the society is ready.

There is no `npm install`, build command, database, or server process required for this static version.

---

# 14. Connecting the Squarespace-managed domain

The competition brief says the existing domain is hosted through Squarespace.

The clean production setup is:

```text
GitHub
   ↓
Vercel deployment
   ↓
Custom domain configured in Vercel
   ↓
Squarespace DNS records
   ↓
Official SMCSS domain
```

In Squarespace:

1. Open the domain settings.
2. Start the process to connect/use a domain.
3. Use the DNS records shown by the relevant Vercel/custom-domain setup.
4. Do **not** delete existing MX records if the domain has email attached.
5. Wait for DNS propagation.
6. Verify HTTPS and the final domain.

The exact DNS values should be taken from the live Vercel/Squarespace setup rather than copied from this README because DNS values and verification records are specific to the deployment.

Squarespace's current documentation explains that third-party domain connections use DNS records, including a verification CNAME and the `www` CNAME, plus A records for the root domain when using Squarespace's DNS connection flow.

---

# 15. If the team wants to use Squarespace's page editor instead

Squarespace supports custom code through code blocks and code injection. JavaScript support depends on the Squarespace plan, and custom code is considered an advanced modification.

However, **do not use this as the primary deployment method for this project** unless the society specifically decides to rebuild the site inside Squarespace.

Why:

- the current design is a complete custom static document
- the navigation and scroll interactions depend on the page's own HTML structure
- the CSS is extensive
- the JavaScript expects the existing DOM structure
- Squarespace can alter/wrap page markup
- custom-code behaviour can require plan-specific features
- Squarespace warns that custom code may affect responsive/mobile behaviour

The cleaner handoff is therefore **Vercel hosting + Squarespace DNS**.

---

# 16. How to make a content change safely

Use this order:

1. Make a backup.
2. Change only the content you need.
3. Test locally.
4. Test desktop.
5. Test mobile.
6. Commit the change to GitHub.
7. Let Vercel deploy the updated commit.
8. Test the production URL.

For event changes, edit `content.js` first.

For contact information or permanent page copy, edit `index.html`.

Avoid changing CSS unless you are intentionally changing the visual design.

---

# 17. What NOT to change casually

Avoid changing:

- section IDs (`home`, `about`, `events`, `executives`, `services`, `resources`, `contact`)
- navigation hrefs
- the contact form ID
- JavaScript element IDs used by the site
- the `content.js` filename
- the external resource URLs unless they have been verified
- the Vercel deployment settings after production handoff

Changing section IDs can break navigation and active-section behaviour.

---

# 18. Production launch checklist

Before handing the site to SMCSS:

### Content

- [ ] Current executive names confirmed
- [ ] Executive photos confirmed/approved
- [ ] Executive programs confirmed
- [ ] Executive emails confirmed where appropriate
- [ ] Current event Linktree verified
- [ ] Signup Google Form verified
- [ ] Locker information verified
- [ ] SMCSS email verified
- [ ] Instagram verified

### Website

- [ ] Home works
- [ ] About works
- [ ] Events works
- [ ] Executives works
- [ ] Services/Locker works
- [ ] Resources work
- [ ] Contact works
- [ ] Contact form opens email correctly
- [ ] All external links open correctly
- [ ] No placeholder executive information remains

### Responsive testing

- [ ] Desktop
- [ ] Laptop
- [ ] Tablet
- [ ] iPhone Safari
- [ ] Android Chrome
- [ ] Keyboard navigation
- [ ] Reduced-motion setting

### Deployment

- [ ] GitHub repository transferred/owned by SMCSS
- [ ] Vercel project transferred to the SMCSS team/account
- [ ] Production domain connected
- [ ] Squarespace DNS verified
- [ ] HTTPS verified
- [ ] Final production test completed

These items align with the competition's stated winner-handoff requirements.

---

# 19. Architecture summary for future developers

This project deliberately avoids unnecessary complexity.

```text
index.html
├── page structure
├── visual design / CSS
├── navigation
├── interaction scripts
├── contact form mailto workflow
└── optional direct event renderer

content.js
├── EVENTS
└── EVENT_SOURCE
```

There is currently no:

- React build pipeline
- Node backend
- PHP
- SQL database
- server-side API
- authentication system

That makes the project easy to transfer and deploy.

If SMCSS eventually needs an admin dashboard, event registration database, protected executive management, or persistent contact submissions, that would be a separate future backend project rather than something to bolt onto the current static site casually.

---

# 20. Final handoff principle

**Keep the design stable. Keep content editable. Keep external information linked to official sources. Keep deployment simple.**

For normal maintenance, a future SMCSS member should be able to update an event in `content.js`, test the site locally, commit the change, and let Vercel deploy it without rebuilding the website from scratch.
