# Florida Contractor Registry — Static Site Deployment

**Status:** Static mockup deployment (Phase 1)
**Purpose:** Get design mockups live on floridacontractorregistry.com for stakeholder review + iterative development

---

## Kya hai yeh?

Yeh saare 33 production HTML mockups hain — homepage se leke admin pages tak. Static hai — matlab search, forms, login — kuchh actually kaam nahi karega abhi. Yeh sirf **dikhne ke liye** hai.

Aage jab hum functionality add karenge (Supabase, Stripe, etc.), tab tak yeh live rahegi taaki Jim, contractors, aur stakeholders design dekh sakein.

---

## Setup Instructions (10 minutes)

### Step 1: GitHub repo banao

1. github.com pe jao aur naya private repo banao: `floridacontractorregistry`
2. Repo banate waqt README/gitignore add mat karo — hum already provide kar rahe hain

### Step 2: Local pe extract karke Git initialize karo

```bash
# Jahan bhi zip download hai wahan extract karo
cd path/to/fcr-static-site

# Git initialize karo
git init
git add .
git commit -m "Initial deployment: 33 static mockup pages"

# GitHub repo se connect karo (URL apne repo se replace karna)
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/floridacontractorregistry.git
git push -u origin main
```

### Step 3: Vercel se connect karo

1. **vercel.com pe login karo** (GitHub account se sign in easiest hai)
2. **"Add New Project"** click karo
3. **Import** karo apna `floridacontractorregistry` repo
4. Framework detection: Vercel apne aap **"Other"** ya **"Static"** detect karega
5. **Build settings — kuchh change mat karo:**
   - Build Command: (empty rakho)
   - Output Directory: (empty rakho, ya `.` daalo)
   - Install Command: (empty rakho)
6. **"Deploy"** click karo

30-60 seconds mein site live ho jayegi. Vercel ek preview URL degi jaisi:
`floridacontractorregistry-abc123.vercel.app`

### Step 4: Custom domain connect karo

1. Vercel project mein: **Settings → Domains**
2. Add karo: `floridacontractorregistry.com`
3. Add karo: `www.floridacontractorregistry.com`
4. Vercel batayegi kya DNS records add karne hain
5. Cloudflare DNS mein jaake woh records add karo
6. 5-15 minutes mein propagation ho jayega

---

## Kya kaam karega, kya nahi

### ✅ Kaam karega
- Har page render hoga design ke saath
- Internal links kaam karengi (`/counties`, `/about`, `/contractor/aceca-construction`)
- Mobile responsive dikhega
- Google Fonts load honge
- Har page ka HTML valid hai

### ❌ Kaam nahi karega (kyunki abhi static hai)
- Search bar mein type karke koi results nahi milenge
- Contractor profiles: sirf ek dummy contractor "Aceca Construction" hai
- Contact forms submit nahi honge
- Login: koi actual auth nahi hai
- Admin pages: navigate ho jayenge but real data nahi hai
- Diagnostic flow: form fill ho jayega but data kahin save nahi hoga
- 266,312 contractors ka database: abhi nahi hai

Yeh sab **Phase 2** mein aayega — jab hum Next.js pe migrate karenge Supabase ke saath.

---

## URL Structure

Yeh URLs pe pages accessible honge:

| URL | Page |
|-----|------|
| `/` | Homepage |
| `/counties` | Counties index |
| `/cities` | Cities index |
| `/types` | License types index |
| `/county/broward` | Sample county page |
| `/contractor/aceca-construction` | Sample contractor profile |
| `/contractors` | For Contractors marketing |
| `/search` | Search results (static) |
| `/diagnostic` | Diagnostic flow |
| `/about`, `/sources`, `/verify`, `/permits`, `/complaint`, `/hiring-checklist` | Content pages |
| `/privacy`, `/terms`, `/sms-terms`, `/cookies`, `/dmca`, `/featured-terms` | Legal pages |
| `/admin/claims`, `/admin/leads`, `/admin/contractors`, `/admin/sync`, `/admin/settings` | Admin pages |
| `/login`, `/login/sent` | Auth pages |
| `/claim/aceca-construction`, `/claim/approved` | Claim flow |
| `/manage/aceca-construction` | Contractor profile management |
| `/inquiries` | Contractor inquiries inbox |

---

## Iterative Development kaise karenge (Phase 2 aur aage)

Static site live hone ke baad, hum yeh workflow follow karenge:

1. **Alag branch** banayenge har feature ke liye (jaise `feature/homepage-real-search`)
2. **Local pe develop** karenge — Vercel automatically preview URLs banata hai har branch ke liye
3. **Test karenge** preview URL pe
4. **Merge karenge main branch mein** jab tayyar ho — Vercel automatically production pe deploy karega

Iss tarah main production site kabhi nahi tootegi jab hum naye features add karenge.

---

## Agar kuchh problem aaye

**Vercel deployment fail ho jaye:**
- Check karo ki `vercel.json` file root mein hai
- Check karo ki `index.html` file root mein hai
- Vercel dashboard mein deployment logs padhne se error samajh aayega

**Custom domain kaam nahi kar raha:**
- DNS propagation mein 15-30 minutes lag sakte hain
- Cloudflare mein DNS records exactly wahi hone chahiye jo Vercel ne suggest kiye
- `dig floridacontractorregistry.com` command se check kar sakte ho DNS resolve ho raha hai ya nahi

**Koi page 404 dikha raha hai:**
- URL patterns check karo `vercel.json` mein — koi missing hai?
- File naming aur URL matching consistent hai?

---

## Next Steps

1. Yeh static site live karo (aaj)
2. Jim ko URL bhejo review ke liye
3. Ek project management doc banao Phase 2 tasks ke liye
4. Phase 2 shuru karo: Next.js migration + Supabase setup + real search

Phase 2 ke liye purani handoff zip mein Build Brief v1.3 padhna — yeh saara plan already documented hai.

Good luck!

— Documented May 24, 2026
