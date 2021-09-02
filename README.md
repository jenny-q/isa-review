# Documentation for Isagenix Codebase - Front-end

The front end for this project was made with patternlab, handlebars, bootstrap, slick, jquery validate, and matchheight.

In the project directory, run  `npm install`.

Once everything is installed, you can run a local instance of patternlab (our component library) with `gulp develop`

The page will automatically open in your browser, and will refresh if you make any changes to the `scss`,`js`, or `hbs` files. Eslint has been enabled and will show any lint errors in the console.

## :file_folder: Folder Structure

All of our front end files live within `/Isagenix-Patternlab`, specifically `/source`. 

`/_data` and `/meta` have files that create the patternlab instance.

:exclamation: **DO NOT EDIT** files under `/public`

```
+-- /public
+-- /source
|   +-- /data
|   +-- /meta
|   +-- /patterns
|   |   +-- /00-atoms
|   |   +-- /01-components
|   |   +-- /02-pages
|   +-- /assets
|   |   +-- /images
|   +-- /css
|   |   +-- /iframe
|   |   +-- /scss
|   |   |   +-- /abstracts
|   |   |   |   +-- _base.scss
|   |   |   |   +-- _variables.scss
|   |   |   +-- /bundles
|   |   |   |   +-- globalBundle.scss
|   |   |   +-- /components
|   |   |   |   +-- accordion.scss
|   |   |   |   +-- alert.scss
|   |   |   +-- /vendor
|   |   |   |   +-- slick.scss
|   |   +-- all.min.css
|   +-- /js
|   |   +-- /base
|   |   |   |   +-- baseClasses.js
|   |   +-- /bundles
|   |   |   |   +-- cartBundle.js
|   |   |   |   +-- globalBundle.js
|   |   +-- /helpers
|   |   |   |   +-- ifeq.js
|   |   |   |   +-- stripSpecialChar.js
|   |   +-- /services
|   |   |   |   +-- accountService.js
|   |   |   |   +-- cartService.js
|   |   +-- /utils
|   |   |   |   +-- historyUtil.js
|   |   |   |   +-- marketUtil.js
|   |   +-- /vendor
|   |   |   |   +-- bootstrap.min.js
|   |   |   |   +-- jquery.min.js
|   |   +-- app.js
|   |   +-- index.js
|   +-- gulpfile.js
|   +-- package.json
```

### /patterns

`/patterns` contains all of our atoms, components and pages.

`/00-atoms` is comprised of branding/system colors, buttons, and headings

`/01-components` contains the building blocks of our site, all of our components live here. Each component has its own folder, e.g. `/header`, `/footer`, `/checkout`.

`/02-pages` are mock up site pages that contain multiple components, e.g. the `cart.hbs` page is importing the `header.hbs`, `cart.hbs`,`cartSidebar.hbs`, and `footer.hbs`  

### /assets

`/assets` contains icons, images for patternlab.  

### /css 

`/css` contains site styling divided into different folders

### /scss

`/scss` contains site styling divided into different folders, `/scss`, `/iframe`, and `/webfonts`

:exclamation: Note: `/iframe` contains css for the **Add Credit Card** modal in checkout.

`/abstracts` contains base, fonts, mixins, and variables. 
	- `/base` is made up of what is considered base site styling, headings, buttons, modal, standard background colors (e.g. bg-turquoise), text colors (e.g. color-turquoise)
	- `/variables` has all of our scss variables (e.g $turquoise, $turquoiseDark)

`/bundles` are page specific scss bundles. 
	- The `globalBundle.scss` is importing scss that is used across most pages of the site:
```
@import '../abstracts/mixins';
@import '../abstracts/variables';
@import '../abstracts/base';
@import '../components/header';
@import '../components/search';
@import '../components/footer';
@import '../components/footerModal';
```
 The cartBundle.scss is importing the scss that is used in on the cart page. No need to include files like header, footer, since it is already defined in the global file.

```
@import '../components/product';
@import '../components/cart';
@import '../components/cartModal';
@import '../components/cartSidebar';
@import '../components/cartToggle';
@import '../components/cart-coupon';
@import '../components/cart-empty';
@import '../components/price';
```

 `/components` consists of component specific scss, e.g. accordion.scss, cart.scss, etc.

`/vendor` has vendor specific scss, e.g. slick.scss

Files of note:
- `all.min.css` is the css file for Font Awesome
- `app.scss` imports all the scss files insode of `/scss` and outputs it into its sister file `app.css`
- `bootstrap.min.css` is bootstraps css file.

### /js

`/js` consists of js files structured into different folders, e.g. `/base`, `/bundles`, `/helpers`, `/services`, `/utils`,
`/vendor`

### /base 

`/base` has one file called `baseClasses.js`, these are global const variables that are used mutiple times across different js files like IS_ACTIVE, IS_HIDDEN, IS_VALID

### /bundles 

Similar to the scss bundles, `/bundles` holds files that are page specific, e.g., `/cartBundle.js` holds cart related js
```
import '../../_patterns/01-components/cart/cart';
import '../../_patterns/01-components/cartModal/cartModal';
import '../../_patterns/01-components/cartToggle/cartToggle';
import '../../_patterns/01-components/cart-coupon/cart-coupon';
```

### /helpers

The files in `/helpers` are handlebars helpers.

- `ifeq.js`  determines if string is equal to json property. In the example below, we are checking if displaytype is equal to 'Range'.

```
 {{#ifeq ../DisplayType "Range" }}
 	if so, do range stuff
 {{/ifeq}}
```

- `stripSpecialChar.js`  replaces special characters with an '-'.

```
{{ stripSpecialChar Name }}
```

### /services
These are mostly calls to sitecore API for cart, inventory, country, etc.

### /vendor 

Third party js files like bootstrap, jquery, slick, and more


### :construction: /fonts, /icons, /images, /static, /styleguide 

These hold default patternlab icons, images, etc. 

## Adding a new component

Create a new folder under `/01-components`  with the name of your component. The hbs and js file should match the name of your folder
```
+-- /01-components
|   +-- /accordion
|   |   +-- accordion.hbs
|   |   +-- accordion.js
|   +-- /breadcrumbs
|   |   +-- breadcrumbs.hbs
|   |   +-- breadcrumbs.js
```
Some components will have to be broken down into [partials](https://handlebarsjs.com/guide/partials.html), in this situation, create a new partials folder inside your component folder. The product component is a great example:
```
+-- /01-components
|   +-- /product
|   |   +-- product.hbs
|   |   +-- product.js
|   |   +-- /partials
|   |   |   +-- productDescription.hbs
|   |   |   +-- productPrice.hbs
```
The scss file for your component should be saved under `/css/scss/components/componentName.scss` as well as the corresponding bundle, e.g. if its a globally used component like breadcrumb, add it to the globalBundle.scss.
```
+-- /source
|   +-- /patterns
|   |   +-- /00-atoms
|   |   +-- /01-components
|   +-- /css
|   |   +-- /scss
|   |   |   +-- /components
|   |   |   |   +-- accordion.scss
|   |   |   |   +-- breadcrumbs.scss
|   |   |   +-- /bundles
|   |   |   |   +-- globalBundle.scss
|   |   |   |   +--cartBundle.scss
```

## Using BEM in scss

Writing scss using BEM is an efficient and clean way to create styling for the site. BEM stands for **block__element--modifier**. 
A block can be many things, e.g. `header, container, footer`. It can also be something as small as a `button`.

Using the button example, the class .button and .button-primary is our block, our modifiers are --hover, --disabled, etc. In this case, we would use **block--modifier-value** syntax.

This site has four types of buttons with multiple states.

```
button button-primary
button button-secondary
button button-tertiary
button button-arrow
button button-primary button-primary--disabled 
```

Product is a great example of a large block element. The class product envelops the entire product page structure. The product page also hosts multiple partials that load depending on the page type (e.g. kit, kit as a product, pack, single facet, multi facet).

The product page is broken up into multiple elements. Some of these don't have the .`product` block name. That is because they are their own blocks, and the product page version is a modifer of that block. An example of this is the `isa-modal` component.

`.isa-modal` is its own component, and it is used globally on the site. There are only minor differences for the gallery pop-up, so instead of creating a new class `.product-gallery__modal`, we are using `.isa-modal .isa-modal--gallery` as the modifer. That way we don't have to create duplicate modal scss styling in the product-gallery scss file, we just add the changes in the `isa-modal.scss` file

```
.isa-modal {
	//global styles here

	//gallery specific styling
    &--gallery {
        position: fixed;
        top: 0;
        left: 0;
        visibility: hidden;
        z-index: 1050;
        width: 100%;
        height: 100%;
        overflow: hidden;
        outline: 0;
        background: rgba($turquoiseDark, .8);
```

There are other exceptions, but the rest of the product block is pretty straight forward.

```
.product
	.container // bootstrap class, most, if not all pages use this class to wrap content
		.product__heading // product header
		.product__details-subheader //reviews and share
		.product__row
			.product-gallery
			.product__details
				.product__dietary-restrictions			
```

## Loading Partials on Templates

Some components render data from sitecore, and don't need partials. Ask your lead and make sure you have all the requirements before starting.

Some components use json to display data. Below is an example with the product template and productHeader.hbs
The json lives in the parent component that holds the partials, product has an attribute called data-product-details.

```
<section class="product" data-product-details='{ json data }'>
```

In the `product.js`

```
import productHeader from './partials/productHeader.hbs';

// load partials
function loadHeader() {
    let $product = $('.product');
    let productData = $product.data('product-details');
    let productHeaderHtml = productHeader(productData);
    $productHeading.append(productHeaderHtml);
}
```

If the partial is being reused, you can add logic for the renderings. The product heading is used on both single product and pack pages:

```
<h1 class="product__header">
    {{#ifeq ProductType 'Bundle'}}
        {{# Products}}
            {{ Name }}
        {{/ Products}}
    {{else}}
        {{# ProductFamily}}
            {{ Name }}
        {{/ ProductFamily}}
    {{/ifeq}}
</h1>
```

:exclamation: Do not put a component in a partial if it is not being generated by javascript. 

## Javascript  - Product.js

`product.js`  has a lot of code that renders different types of products, e.g. kits, kits as a product, single facet products, multi facet products.

Most, if not all of the functions are neatly wrapped with one function `initEventHandlers`:

- `loadHeader();`
    - Loads the header for the product depending on type (pack/product)

- `createGroupByFacets();`
    - This will create an empty div based on the facets that live under the groupByFacets object in the product data. If it is empty, it is considered a product with no facets.
    This function will also create the *dietary restrictions* section based on `SecondaryFacetGroupId`, as well as load the image/default radio partial for the facets.

- `checkNullPrices();`
     - If a product has null prices, or the prices object is empty, the product will not get rendered on the page

- `checkForProducts();`
    - This is checking for products in the json, if there are no products, show description and header only, no facets.
    Will display `no products` in console.

- `checkKits();`
    - This is checking for product kits. If there are kits, the template is slightly different. The products appear in `<ul><li>kit product</li></ul>`
    This also looks for `checkRender` to be set to true/false on the json. If it is false, it will render like a kit page. If it is set to true, it will render like a product page, with facets `createGroupByFacets`. 

- `checkBundleConfiguration();`
    - Checks if this is a kit or a product pack, will load partials depending on `productData.BundleConfiguration.IsConfigurable`.

- `productShareUrl();`
    - Displays url on product share modal.

- `sortFacets();`
    - Sorts facet sections based on `"Order": 0` within `GroupByFacets`

- `checkMultiFacets();`
    - Will filter data that displayed based on whether there are multiple facets or not.

- `loadTooltip();`
    - If there is a tooltip on page, load bootstrap tooltip.

- `checkCustomerType();`
    - Looks for  `"CustomerType"` in the json. If there is a set type, e.g. `Retail`, only retail pricing will show. If it's blank, both pricing groups will display.

- `sortPrice();`
    - Sort pricing to always display Preferred Customer pricing first.

- `checkStatus();`
    - Checks to see if `IsTempUnavailable` is set to true/false. If true, it will display as error message next to the facet, and the add to cart button will be grayed out and disabled. The error message is set in the json under the `Labels` object.

    - :exclamation: Out of stock is checked on page load with function `checkProductOos()`. The message for out of stock and temporarily unavailable is the same. Check the console to see if product is marked `oos` or `not oos`.

- `checkHeight()`
    - checks the height of the product description, if it's more than 3 lines, clip the description, adds an ellipsis, and displays a Show More button.

- `checkPriceTypeOnLoad()`
    - Runs once, will check the first price type AFTER the pricing is sorted. I removed the "checked" attribute on the `hbs` templates because the PC price was not always the first one in the json.

These are all related to price quantity.

```
$productPrice.on('click', '.increase-items', increaseItems);
$productPrice.on('click', '.decrease-items', decreaseItems);
$productPrice.on('focus', '.quantity-input', storeItemQuantity);
$productPrice.on('blur', '.quantity-input', updateItemQuantity);
$productPrice.on('keyup', '.quantity-input', checkItemMaxQuantity);
```

`addToCart` adds the product to cart, but there are two types of addToCart. There is `addProductToCart()` and `addKitToCart()`.

`$body.on('click', '.addToCart', addToCart);`

`closeMsg` closes any `addToCart` error messages.

`$body.on('click', '.error__btn', closeMsg);`

This toggles the `IS_ACTIVE` class and displays the Add to Cart button and quantity. Only the active radio button will show add to cart, quantity.

`$body.on('click', '.price__block input', showInput);`

This copies the url within the product share modal.

`$copyToClipboardBtn.on('click', CopyToClipboard);`

This makes the custom input fields for product kits ada accessible.

`$productLabel.on('keypress', inputAda);`

Toggles product description if there is a Show More button.

`$body.on('click', '#show-more', toggleDescription);`

Keeps the same quantity number across multiple products instead of resetting to zero on facet click.

```
$productInput.on('click', getUpdatedQuantity);
$body.on('keyup', '.price__quantity-sign--amount', getUpdatedQuantityKey);
```

These will keep the same price type clicked on product update. If the user clicks on `Retail` and selects a different flavor, the product will show `Retail` price clicked.

```
$productInput.on('click', checkPriceType);
$body.on('click', '.price__block input', setPriceType);
```

Checks the description height on facet click. Some products have longer descriptions than others, or none at all.

`$body.on('click', '.product__input', checkHeight);`

:exclamation: Sometimes there is some sitecore code that breaks clib, I just wrap in this to check if it is in patternlab. This will only run on a sitecore environment.

```
if(!$body.hasClass('patternlab__body')) {
    initCurrencyFormatter();
}
```