- [x] Refactor `ProductCard` and `ProductGrid` to fit better in size
- [x] Refactor `ProductBanner` to be a component that consists of title, see-all-button that renders an instance of `ProductPage`, and only shows the first 4 products in the passed `products` array. No more arrow buttons. Make sure it shows one row only, so that the 4th card doesn't jump to the next line upon scaling down. 
- [x] Make an API path, that gets all the available countries from the data (`/api/countries`) 
- [x] Refactor ProductPage so it renders the countries and categories in the filter that actually occur within the data -> use API paths for `/categories` and `/countries`
- [ ] Refactor the props type on ProductPage to be able to take a filter in the same format as in ProductBanner
- [x] Add option to the filter "Discounted products"

# BasketPage fix
- [x] BasketPage needs to reflect `BasketItem`s that reflect whoever is logged in

# Structure anonymous user storage better
- [x] If user is not logged in `if (!currentUser)` the basket is based on a key from localStorage called `"localUser"`
	- [ ] Bonus: if an anonymous registers an account, the basket of `localUser` is moved to that users basket and `localUser` is wiped.
- [x] Fix for: BasketPage
- [x] Fix for: Navbar
- [x] Fix for: ProductCard (handler functions)

## Editing cart
- [x] Refactor so adding things to and updating cart works for logged in user
- [x] Refactor so adding things to and updating cart works for `localUser`

## Basket architecture status

| |When logged in     |When NOT logged in     |
| --- | --- | --- |
|where is the data coming from?|API call based on `currentUser.customerId`|`localStorage.getItem("localUser")` which is formatted similarly|
| counter in Navbar reflects user's real data    | ✅ | ✅ |
| content on BasketPage reflects user's real data| ✅ | ✅ |
| adding smth to basket from FrontPage           | ✅ | ❌ |
| adding smth to basket from ProductsPage        | ✅ | ❌ |
| adding smth to basket from FrontPage           | ✅ | ❌ |
| adding smth to basket from ProductsDetailPage  | ✅ | ❌ |
