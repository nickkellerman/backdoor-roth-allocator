# Backdoor Roth Allocator

A single-page tool that shows how to invest this year's backdoor Roth conversion so your Roth IRA moves closer to your target allocation, without selling anything.

Everything is in `index.html`. There's no build step, no server and no dependencies to install.

## Use it locally

Double-click `index.html` to open it in a browser. Manual entry, CSV import and pasted text all work offline. Screenshot import needs an internet connection the first time, to download the open-source text reader (Tesseract.js).

## Share it for free with GitHub Pages

1. Create a free GitHub account and a new **public** repository (e.g. `roth-allocator`).
2. Upload `index.html` (and this README) to the repository: **Add file → Upload files**.
3. Go to **Settings → Pages**. Under "Build and deployment", pick **Deploy from a branch**, branch `main`, folder `/ (root)`, then **Save**.
4. After a minute your link appears there, e.g. `https://<your-username>.github.io/roth-allocator/`. Share that link.

Cloudflare Pages and Netlify also work: drag the folder into their "deploy" page.

## Privacy design

- No backend, accounts, analytics or cookies. All math happens in the browser.
- A Content-Security-Policy in the page blocks it from sending data anywhere. The only outside requests allowed are downloads of the Tesseract.js reader from jsDelivr and its language file, and only when a screenshot is imported.
- Screenshots are read on the device, then discarded. The extracted text is filtered so that only tickers, fund names and dollar values are kept. Emails, long digit runs and masked or dashed account numbers are removed first, and the raw text is never shown or stored.
- CSV imports read only the Symbol/Ticker, Description and value columns. Other columns, such as account number, are ignored.
- "Remember my tickers and targets" is off by default. When it's on, it saves tickers, fund names, classes, targets and the amount to the browser's localStorage, but never dollar balances.

## How the allocation works

For each fund (or asset class) *i* with current value *vᵢ* and target weight *wᵢ*, the ideal value after investing *C* is *wᵢ(T + C)*. The tool buys *max(0, gapᵢ − λ·wᵢ)*, choosing λ so the buys add up to *C*. In other words, money goes to whatever is furthest below its target (relative to that target) until those funds are equally short, and nothing is ever sold. If nothing is overweight, the result lands exactly on target.

## Not advice

This is a calculator for targets you choose. It isn't financial, tax or investment advice.
