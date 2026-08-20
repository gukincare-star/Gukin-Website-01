# GUKIN — Shopify integration & pages still to build

## Live prices from Shopify (Storefront API)

The shop section renders from a `products` array. To go live:

1. Shopify admin → **Apps → Develop apps → Create an app** → enable **Storefront API** scopes `unauthenticated_read_product_listings`.
2. Copy the **Storefront access token**.
3. Replace the static array with this fetch (put the token in an env var, never in the repo):

```js
const SHOP = 'your-store.myshopify.com';
const TOKEN = process.env.SHOPIFY_STOREFRONT_TOKEN;

async function getProducts() {
  const res = await fetch(`https://${SHOP}/api/2024-10/graphql.json`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json', 'X-Shopify-Storefront-Access-Token': TOKEN },
    body: JSON.stringify({ query: `{
      products(first: 10) {
        edges { node {
          id handle title description
          images(first: 2) { edges { node { url altText } } }
          variants(first: 1) { edges { node { id price { amount currencyCode } availableForSale } } }
        } }
      }
    }` }),
  });
  const { data } = await res.json();
  return data.products.edges.map(({ node: n }) => ({
    slot: n.handle,
    name: n.title,
    subtitle: n.description.split('.')[0],
    price: '$' + Math.round(n.variants.edges[0].node.price.amount),
    variantId: n.variants.edges[0].node.id,
    inStock: n.variants.edges[0].node.availableForSale,
    img: n.images.edges[0]?.node.url,
  }));
}
```

Field mapping is 1:1 with the existing array, so the cards and cart drawer need no other change. For real checkout, swap the local cart for `cartCreate` / `cartLinesAdd` and redirect to `cart.checkoutUrl`.

## Pages referenced but not yet built

The homepage links to these. Create them (or repoint the links) before launch:

**Collection pages** — from the four "Shop by concern" tiles:
- `collection-gut.html`
- `collection-skin.html`
- `collection-longevity.html`
- `collection-strength.html`

Each should list the products tagged to that concern (filter the Shopify array by `goal`/tag).

**Theory pages** — from the three "Read the science" links:
- `theory-gut.html`
- `theory-age.html`
- `theory-skin.html`

**Journal articles** — from the four journal cards:
- `journal-gut-longevity-axis.html`
- `journal-nad-depletion-aging.html`
- `journal-pdrn-peptides.html`
- `journal-collagen-zinc-permeability.html`

Until these exist the links will 404. Simplest interim fix: point them all at `index.html#science`.

## Image optimisation (still outstanding)

Everything in `site/media/` should go through squoosh.app — WebP, longest edge ~1600px, quality ~80, target under 300 KB each. Several files are currently 3–7 MB.
