# Mkanga-Ulimi Farm Website — Final Deployment & Content Guide

This website is a static HTML, CSS and JavaScript site. It does **not** have a website admin dashboard or database-backed content manager. To change website content, edit the files below, test locally, then upload/push the changed files to the hosting provider (for GitHub Pages, commit and push to the published repository).

## 1. Important files and folders

- `index.html` — homepage content, homepage product teaser cards, hero sections and homepage calls to action.
- `market.html` — Market page layout, cart overlay, and market page text.
- `assets/js/products.js` — **the product catalogue** shown automatically on Market. Add, edit, or remove products here.
- `assets/images/` — product photos, homepage images, logos and other website images.
- `gallery.html` — gallery layout and the list of photos shown in the gallery.
- `assets/images/gallery-watermarked/` — the watermarked gallery photos currently used by `gallery.html`.
- `assets/css/style.css`, `assets/css/responsive.css` and page-specific inline CSS — website styling and mobile layout.
- `assets/js/market.js` — market search, category filters, quantity controls, cart and WhatsApp checkout. Do not edit unless changing market behaviour.
- `assets/js/main.js` — shared navigation and general website interactions.
- `contact.html` — contact-page details and contact links.
- `README.md` — short project overview.

## 2. How to add or change a Market product

1. Open `assets/js/products.js` in VS Code or another text editor.
2. Find `const MARKET_PRODUCTS = [` and copy an existing product object as a template.
3. Add the new object inside the array, separated from neighbouring objects by commas. Each product needs a unique `id`.
4. Put the product photo in `assets/images/`, then set `image` to the exact relative path and filename. Filenames are case-sensitive on many hosts: `Pigeons.jpg` is not the same as `pigeons.jpg`.
5. Set the name, category, category label, description, price display, unit and availability.
6. Save, refresh `market.html`, and test search, category filters, quantity plus/minus, Add, cart removal and WhatsApp checkout.

Example product entry (change the sample details and ensure the image exists):

```js
{
  id: "new-product",
  name: "New Product",
  category: "livestock",
  categoryName: "Livestock",
  description: "Short product description.",
  image: "assets/images/new-product.jpg",
  price: null,
  priceDisplay: "Price on Enquiry",
  unit: "per item",
  available: true
},
```

Categories used by the site include `livestock`, `poultry`, `horticulture` and `apiculture`. The category filter buttons are generated automatically from product data.

### Prices and availability

- For a product whose price is not fixed, use `price: null` and `priceDisplay: "Price on Enquiry"`.
- For a fixed price, `price` must be a number and `priceDisplay` must show the same price in readable form, e.g. `price: 7000` and `priceDisplay: "MWK 7,000"`.
- Use `available: true` to enable Add, or `available: false` to mark it out of stock.
- Verify all prices, units and availability with the farm before publishing. Market orders are requests via WhatsApp; the website does not process payments or confirm stock automatically.
- The Farm Eggs item has been removed from the Market catalogue as requested.

## 3. How to add or change product photos

1. Prepare a clear, appropriately cropped JPG, PNG or WebP image.
2. Give it a short filename without spaces, e.g. `new-product.jpg`.
3. Upload/copy it into `assets/images/`.
4. Update the relevant `image` value in `assets/js/products.js` to match the filename exactly.
5. Preview the Market page at desktop and mobile sizes before publishing.

Do not overwrite a photo that is used by another section unless you intend to change that section too.

## 4. How to add photos to the Gallery

The gallery is manually listed in `gallery.html`; placing a file in the image folder alone will not make it appear.

1. Copy the new photo into `assets/images/gallery-watermarked/` if it has been approved/watermarked for public display. Otherwise use the appropriate existing gallery image folder and follow the same path pattern used by the page.
2. Open `gallery.html`.
3. Find the `gallery-grid` section and copy an existing image line, for example:

   ```html
   <img class="gallery-img" src="assets/images/gallery-watermarked/1.jpg" alt="Farm photo" />
   ```

4. Change `src` to the exact new path and write a useful description in `alt`, such as `alt="Harvesting tomatoes at Mkanga-Ulimi Farm"`.
5. Save and check that the image loads, looks good on a phone and opens correctly with the gallery viewer if enabled.
6. Publish both `gallery.html` and the new image file.

Use unique filenames rather than replacing `1.jpg`, `2.jpg`, etc. Keep a backup of original photos. Avoid uploading very large originals; resize/compress them for faster mobile loading.

## 5. Homepage buttons and sections

- Homepage content and buttons live in `index.html`.
- The homepage product/explore calls to action now lead to `market.html`, not the legacy `products.html` page.
- To change homepage wording, edit the relevant heading, paragraph or link in `index.html`.
- When adding a new button, use a relative link such as `href="market.html"` so it works on the hosted site.

## 6. Contact and WhatsApp ordering

- The Market checkout is implemented in `assets/js/market.js`.
- The current WhatsApp destination is `+265 999 826 757`, represented in links as `https://wa.me/265999826757`.
- If the farm changes its number, update the WhatsApp links in the relevant HTML files and `assets/js/market.js`, then test checkout on a phone.
- The Market cart is a client-side cart for building an order message. It is not a payment gateway, and cart contents are not a server-side order record.

## 7. Publish the final changes

### If the website is published with GitHub Pages

1. Keep a backup copy of the current live repository before replacing files.
2. Extract the final ZIP and open the project folder.
3. Test `index.html` and `market.html` locally in a browser. Check mobile layout and all links/images.
4. Open the correct GitHub repository and upload the changed files/folders, or commit and push the project with Git.
5. Ensure the repository's GitHub Pages publishing source still points to the correct branch/folder.
6. Wait for the Pages deployment to finish, then hard-refresh the live site (`Ctrl+F5`) or test in a private window.
7. Test the homepage product button, Market filters, pigeon photo, quantity controls, continue-shopping button, remove-from-cart, and WhatsApp checkout.

### If uploading through a hosting file manager or FTP

1. Download a backup of the current live site first.
2. Upload the updated project files while preserving the directory structure.
3. Ensure `index.html` is at the website's document root and the `assets/` directory remains alongside it.
4. Open the live site and run the same tests listed above.

## 8. Final launch checklist

- [ ] Homepage product links go to Market.
- [ ] No Farm Eggs card appears in Market.
- [ ] Pigeons display the `assets/images/Pigeons.jpg` image.
- [ ] Mobile cart has a clear “Continue shopping” back-arrow action.
- [ ] Product photos and gallery images load without 404 errors.
- [ ] All product prices and availability have been confirmed by the farm.
- [ ] WhatsApp order opens the correct farm number and includes product names and quantities.
- [ ] Navigation and footer links work.
- [ ] Website has been checked on both desktop and mobile.
- [ ] A copy of the previous live version is saved for rollback.

## 9. Troubleshooting

- **A photo is missing:** check the filename, letter case, extension and relative path.
- **A product does not appear:** check commas/braces in `products.js`, `available` value, and browser console errors.
- **A new gallery photo does not show:** confirm you added an `<img>` entry to `gallery.html` as well as uploading the image.
- **The live site still looks old:** confirm you uploaded to the correct repository/hosting folder, wait for deployment, then hard-refresh or use a private window.
- **Cart quantity looks wrong:** each product card's number is the quantity added when its Add button is clicked; the cart count shows the total number of units, not the number of different product types.
