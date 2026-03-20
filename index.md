---
layout: page
title:
secondary_content: |

  [Edit this page at github.com/owen-kellie-smith/static-websites](https://github.com/owen-kellie-smith/static-websites)

---

# Static websites hostable on github pages

<!-- Table -->
<table id="repo-table">
<thead>
<tr>
  <th>Original</th>
  <th>Copy</th>
  <th>Features of the copy</th>
  <th>Forks</th>
  <th>Last push</th>
</tr>
</thead>
<tbody>
<tr>
  <td data-label="Original"><a href="https://www.exmusicsummerschool.co.uk/">exmusicsummerschool.co.uk</a></td>
  <td data-label="Copy"><a href="https://owen-kellie-smith.github.io/ex-static/">ex-static</a></td>
  <td data-label="Features" >Uses plain markdown</td>
  <td  data-label="Forks" data-repo="owen-kellie-smith/ex-static" data-field="forks">...</td>
  <td  data-label="Last push" data-repo="owen-kellie-smith/ex-static" data-field="pushed" data-repo-link="https://github.com/owen-kellie-smith/ex-static">...</td>
</tr>
<!-- Repeat rows for other repos, following the same structure -->
<tr>
  <td data-label="Original"><a href="https://www.thornburyswingband.com/">thornburyswingband.com</a></td>
  <td data-label="Copy"><a href="https://owen-kellie-smith.github.io/tsb-static/">tsb-static</a></td>
  <td data-label="Features" >Uses plain markdown</td>
  <td  data-label="Forks" data-repo="owen-kellie-smith/tsb-static" data-field="forks">...</td>
  <td  data-label="Last push" data-repo="owen-kellie-smith/tsb-static" data-field="pushed" data-repo-link="https://github.com/owen-kellie-smith/tsb-static">...</td>
</tr>
<tr>
  <td data-label="Original"> offline -- replaced by the copy</td>
  <td data-label="Copy"><a href="https://owen-kellie-smith.github.io/etcb-website/">etcb-website</a></td>
  <td data-label="Features" >Single web-page</td>
  <td  data-label="Forks" data-repo="owen-kellie-smith/etcb-website" data-field="forks">...</td>
  <td  data-label="Last push" data-repo="owen-kellie-smith/etcb-website" data-field="pushed" data-repo-link="https://github.com/owen-kellie-smith/etcb-website">...</td>
</tr>
<tr>
  <td data-label="Original"><a href="https://www.axevaleorchestra.co.uk/">axevaleorchestra.co.uk</a></td>
  <td data-label="Copy"><a href="https://owen-kellie-smith.github.io/avo-website/">avo-website</a></td>
  <td data-label="Features" >Single web-page</td>
  <td  data-label="Forks" data-repo="owen-kellie-smith/avo-website" data-field="forks">...</td>
  <td  data-label="Last push" data-repo="owen-kellie-smith/avo-website" data-field="pushed" data-repo-link="https://github.com/owen-kellie-smith/avo-website">...</td>
</tr>
</tbody>
</table>


<!-- Scripts -->
<script>
// Format dates as YYYY-MM-DD
function formatDate(dateString) {
  const date = new Date(dateString);
  return date.toLocaleString("en-GB", {
  day: "2-digit",
  month: "2-digit",
  year: "numeric",
  hour: "2-digit",
  minute: "2-digit",
  hour12: false
  });
}

// Load data from forks.json
fetch("forks.json")
  .then(res => res.json())
  .then(data => {
    document.querySelectorAll("[data-repo]").forEach(el => {
      const repo = el.dataset.repo;
      const field = el.dataset.field;

      if (!data[repo]) return;

      if (field === "forks") el.textContent = data[repo].forks;
      else if (field === "pushed") {
        const dateText = formatDate(data[repo].pushed_at);
        const link = el.dataset.repoLink;
        el.innerHTML = `<a href="${link}" target="_blank">${dateText}</a>`;
      }
    });
  });

// Make table sortable
document.querySelectorAll("#repo-table th").forEach((header, colIndex) => {
  let ascending = true;
  header.addEventListener("click", () => {
    const table = header.closest("table");
    const tbody = table.querySelector("tbody");
    const rows = Array.from(tbody.querySelectorAll("tr"));

    rows.sort((a, b) => {
      let A = a.children[colIndex].innerText.trim();
      let B = b.children[colIndex].innerText.trim();

      const numA = parseFloat(A);
      const numB = parseFloat(B);
      if (!isNaN(numA) && !isNaN(numB)) return ascending ? numA - numB : numB - numA;

      const dateA = Date.parse(A);
      const dateB = Date.parse(B);
      if (!isNaN(dateA) && !isNaN(dateB)) return ascending ? dateA - dateB : dateB - dateA;

      return ascending ? A.localeCompare(B) : B.localeCompare(A);
    });

    rows.forEach(row => tbody.appendChild(row));
    ascending = !ascending;
  });
});
</script>



# How to host your website for free and control it 

By following steps 1-8 below you can:
1. **Keep full control of your website content** – Your website files live in your own free GitHub account. Other people can suggest changes, but only you can **accept** them. All changes are  reversible. You can make changes directly on the GitHub website or via a local copy on your own machine, which you then push to GitHub.
2. **Host your website for free** – GitHub Pages hosts your site for free and implements your changes within a couple of minutes.
3. **Keep full control of your domain name** – you decide what it points to and how it’s managed. Via your own free Cloudflare account, Cloudflare connects your domain to your Github site.
4. **Leave your website readers in peace** – your readers see a similar website at the usual address.

> As an interim step if you are happy for me to update your website content then you can ignore steps 1-7 and just do (reversible) [step 8](#step-8-change-nameservers-for-your-domain) (with the nameservers from my Cloudflare account -- ask me for them). 

> If you have any trouble, [create a new issue](https://github.com/owen-kellie-smith/static-websites/issues) or ask me the next time we meet etc.


---

## Step 1: Fork the repository

1. Go to the repository: `https://github.com/owen-kellie-smith/\<repo-name-for-your-website\>`
2. Click **Fork** (top right: Pin Watch **Fork** Star).

> Now you have your own copy of the website content under your GitHub account and so the website content is **fully under your control**.

---

## Step 2: Enable GitHub Pages

1. Go to your fork → **Settings → Pages**
2. Under **Source**, select:
    Branch: main 
    Folder: /(root) or /docs depending on where the index.md or index.html file is.
3. Click **Save**

> Your Github site will be visible at: 
`https://<your-username>.github.io/<repo-name>/`

---

## Step 3: Check you can edit your new website content

Edit your new repo (i.e. the fork) on the github website or clone it to a local copy on your machine.  Make some changes, commit them and push them to github and check that after a few minutes (and page refreshes in your browser) you see your changes implemented at:
`https://<your-username>.github.io/<repo-name>/`
 

---

## Step 4: Set up Cloudflare

1. Create an account at [Cloudflare](https://www.cloudflare.com/).
2. In Cloudflare, click **Add a site**, enter your domain and (in the next screen) choose the **Free plan**
3. Cloudflare will scan your DNS and give you two nameservers, e.g.:
```
abby.ns.cloudflare.com
john.ns.cloudflare.com
```
> The first names will almost certainly not be abby and john but will be unique to you.
4. **Write down** the Cloudflare nameservers.

---

## Step 5: Point Cloudflare DNS to GitHub Pages

In Cloudflare DNS Records create 4 A records, and 1 CNAME record.  Suppose your domain is `yourdomain.com`


Add **A records** pointing to GitHub Pages:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

> Why four IPs? 
> GitHub Pages uses multiple IPs for redundancy. If one IP fails, the others still serve your site.


Add a **CNAME record** pointing to your GitHub Pages site:
```
www → <your-username>.github.io
```

If you want email forwarding from say info@yourdomain.com to some other email address then also go to Cloudflare > Email > Email Routing > Routing rules (which adds other MX and TXT DNS records automatically).

Example Cloudflare DNS records for 'seatonsite.co.uk' showing 4 A records and 1 CNAME record:
<div class="gallery">
{% include gallery.html size="xxl" href="assets/cloudflare_dns_records.png" %}
</div>


---

## Step 6: Enforce HTTPS

1. In Cloudflare: 
   - Go to **SSL/TLS** → Overview → set mode **Full**  (maybe nothing to do as it may already be set to Full)
   - Go to **SSL/TLS** → Edge Certificates → Always use HTTPS (slide to on)

2. In GitHub Pages: 
   - Go to **Settings → Pages** → enable **Enforce HTTPS**

---
## Step 7: Add your custom domain

1. In Github **Settings → Pages**, under **Custom domain**, enter your domain: 
`www.yourdomain.com` 
2. Click **Save**.  

> Your Github site will no longer be visible but keep going to the end (about 10 mins).

---

## Step 8: Change nameservers for your domain

Go to your domain registrar (where you bought your domain) and 
- **write down on paper** / take a screenshot of the existing nameservers
- delete all the existing nameservers and add just the two xyz.ns.cloudflare.com nameservers from your Cloudflare account in [step 4](#step-4-set-up-cloudflare). 
- wait 10 minutes
> Your Github site will be visible at:  `https://yourdomain.com/`
> So you will be free at your leisure to stop renewing your hosting plan for the old copy of the site.


---

## Result

✅ Your website will be:

- [Fully controlled by you](#step-3-check-you-can-edit-your-new-website-content) (via your GitHub account) 
- Hosted for free (GitHub Pages) 
- [Connected to your domain](#step-8-change-nameservers-for-your-domain) (via Cloudflare) 

---

## Updating your website

To make changes to the website:

1. Edit files in your GitHub repository. Commit and push changes.
3. Wait 5 minutes.
4. Refresh your browser page (to get the new page, not a cached copy).

---

