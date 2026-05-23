# Loom

[paste your Loom link here after recording]

---

## What I picked

Fixed a bug in `product-card.js` that throws 24 console errors on every collection page on xinzuo.com.au. The error is `MissingRefError: productCardLink not found`. One-line fix.

## Why it's the highest-impact thing here

Collection pages are where people browse and click through to buy. This bug fires 24 times every time someone loads one.

Three reasons it matters:

1. The feature that's broken — updating card links when a variant is selected — silently doesn't work. People click and go to the wrong URL or default product.
2. 24 errors in the console drowns out real bugs. Future devs can't see what's actually breaking.
3. The fix is literally already written in the same file, just not applied here. Lines 213 and 216 wrap `cardGalleryLink` and `productTitleLink` with safety checks. Line 210 with `productCardLink` doesn't. Someone forgot one ref out of three.

I could've rebuilt the bundle builder page. But fixing a real bug on the main shopping flow with 3 lines beats shipping 500 lines of something flashy.

## What I did

One file. Three lines added in `assets/product-card.js` at line 210.

Before:
```js
productCardLink.href = productUrl;
```

After:
```js
if (productCardLink instanceof HTMLAnchorElement) {
  productCardLink.href = productUrl;
}
```

That's it. Same pattern the next two refs already use. If the link element exists, update it. If not, don't crash.

**How I checked it:**
- before.png — xinzuo.com.au console, 24 red errors clearly visible
- after.png — my dev store with the fix, console is clean

## What I'd do next

1. Find the Liquid file that's missing the `ref="productCardLink"` attribute on its `<a>` tag and add it. My fix stops the crash, but the actual feature (link updates on variant change) still won't work until the template is fixed too. Suspect file: `snippets/xz-product-card.liquid`.
2. Check `quick-add.js` and `product-form.js` — they use the same ref pattern and probably have the same bug waiting to happen.
3. Add a basic test that loads a product card and checks for console errors. Nothing right now stops this from breaking again.