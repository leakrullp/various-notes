```
cd ~
cd documents/github/personal/candy-webshop-react
npm install
npm run dev
```

## Demonstration of the system functionality (3 min)

[http://localhost:5173/](http://localhost:5173/)
- Users enter our website and can immediately shop without registration
- On the frontpage you can see a curation of products (e.g. "Danish products" or "On Sale")

[http://localhost:5173/register](http://localhost:5173/register)
- You can register an account to use the site
	- Name, lastname, email, password
- After registration your name is visible on the frontpage and in the basket page

[http://localhost:5173/ProductsPage](http://localhost:5173/ProductsPage)
- The products page shows the full scope of products in the store
- You can browse based on country, category or whether it's on sale
- *Quickly add a product to cart*
- If you click on a products you see the detailed information about it on a page.
- *Add products to cart from detail page*

[http://localhost:5173/cart](http://localhost:5173/cart)
- We can see all the products we just added to our cart.
- We can remove the wrong product and adjust the amount for the other product.

## Explanation of the web UI design (2 min)
Our site follows a pattern of a **linear sequence with supporting digressions**. It follows many webshop conventions. There's a list of the full product catalog ready to browse and a cart page you can review. 

We followed the principles of:
- Visibility of System Status – name when logged in, amount in cart, fedback when no products match
- Recognization rather than recall – the user knows where to find their items

RESPONSIVE DESIGN


## Explanation of the system software architecture (5 min)
- Monorepo structure – one `npm install` command

![[Pasted image 20260614151555.png]]

- Our backend
	- All data lives in data.json
- Our API
	- Runs on `localhost:3000` separate from client
	- Routes and controllers are separated for better structure
	- The routes are indexed so `server.js` only uses one router in the end.
	- `serverUtil.js` has a `cache` variable, that makes sure the data is fetched once at startup and again when saveData has run.
- Our frontend
	- React+Typescript ordered as a typical React project
	- Indexing inside of `components`, `pages`, `hooks`, and `types` for easy import
	- Highlights:
		- Prop drilling inside `ProductsPage` passing the props between `FilterBox` and `ProductGrid`

![[Pasted image 20260614135521.png]]