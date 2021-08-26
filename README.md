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
