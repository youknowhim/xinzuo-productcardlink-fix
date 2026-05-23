# Bug Fix: `productCardLink` MissingRefError — `product-card.js`

## What I picked
Fixed a bug causing 24 `MissingRefError: productCardLink not found` console errors on every collection page on xinzuo.com.au.

## Why it matters
Collection pages are the main shopping funnel. This fires 24 times on every load.

1. The broken feature — updating card links on variant selection — silently fails. Users click through to the wrong URL or default product.
2. 24 errors drown out real bugs. Future devs can't see what's actually breaking.
3. The fix was already written in the same file. Lines 213 and 216 wrap `cardGalleryLink` and `productTitleLink` in safety checks. Line 210 didn't. One ref missed out of three.

## What I did
One file. Three lines in `assets/product-card.js` at line 210.

**Before:**
```js
productCardLink.href = productUrl;
```

**After:**
```js
if (productCardLink instanceof HTMLAnchorElement) {
  productCardLink.href = productUrl;
}
```

Same pattern the other two refs already use.

**Verified with:**
- `before.png` — xinzuo.com.au console, 24 red errors visible
- `after.png` — dev store with fix applied, console clean

## What I'd do next
1. Find the Liquid template missing `ref="productCardLink"` on its `<a>` tag. The crash is fixed, but variant link updates still won't work until the template is corrected. Suspect: `snippets/xz-product-card.liquid`.
2. Audit `quick-add.js` and `product-form.js` — same ref pattern, likely same latent bug.
3. Add a smoke test that loads a product card and asserts no console errors. Nothing currently prevents this from regressing.
