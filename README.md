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