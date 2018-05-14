# Helper JavaScript
Publishers who do not want a CMP (Consent Management Provider) UI to appear as a pop-up on their site still need the ability to pass a "consent" signal downstream to process bid requests appropriately. Such publishers need a way to operationalize their understanding that they have consent from their users while satisfying the technical need to pass on consent objects.

The PubMatic Helper JavaScript code generates a consent object for every bid request. Consent is provided for all the vendors listed in the IAB EU Transparency & Consent Framework Global Vendor List.

 
## The Helper JavaScript:

+ Implements all functions, such as getConsentData and getVendorConsents, which are detailed in the IAB Consent Management 
+ Provider JavaScript API.
+ Relies on IAB's vendor list to construct the string.
+ Requires that publishers install it on every page.
+ Will be available in Open Source (github).
+ Works with any client (e.g., OpenWrap) that integrates with IAB's Consent Management Framework.

## Important Notes
+ By using the Helper JavaScript, you confirm that you have obtained required consents from end users.
+ This code was forked from https://github.com/appnexus/cmp

## Download Script

+ `./build/cmp.bundle.js` - Helper Script to include on your site

## How to Include on Web Page
```js
<!-- 
	Publisher will need to add following two script tags on their web-pages.
-->
<script>
	window.__cmp = {
		config: {
			logging: 'debug'
		}
	};
</script>
<script src="<<HTTP_PATH_TO_HOSTED_cmp.bundle.js>>" async></script>
```

### Sample Web Page example
```js
<!DOCTYPE html>
<html>
    
    <head>
        <!-- 
        	Publisher will need to add following two script tags on their web-pages.
        -->
        <script>
            window.__cmp = {
                config: {
                    logging: 'debug'
                }
            };
        </script>
        <script src="<<HTTP_PATH_TO_HOSTED_cmp.bundle.js>>" async></script>
    </head>
    
    <body>
        <h3>
            Demo
        </h3>
        <!-- 
        	Sample code for accessing APIs.
        	Publishers do not need to put following code on their web-page. 
        -->
        <script>
            setTimeout(function() {
                window.__cmp('getVendorConsents', null, function(result) {
                    console.log('getVendorConsents callback result:\n' + JSON.stringify(result, null, 2));
                });

                window.__cmp('getConsentData', null, function(result) {
                    console.log(result);
                });
            }, 3000);
        </script>
    </body>

</html>
```

# Instructions to extend (Optional)
### Installation

```sh
git clone https://github.com/PubMatic/GDPR_Helper_JS.git
cd cmp
yarn install
```

## Build for Production

```sh
yarn build
```

This produces a production build of the `cmp` script and the docs application:
+ `./build/cmp.bundle.js` - CMP script to include on your site
+ `./build/docs/` - Application hosting the documentation

## Documentation

Instructions to install the CMP as well as API docs and examples are available in the `docs`
application included with the repo.

```sh
yarn start
```

The documentation can be viewed at:
`http://localhost:5000/docs/`

## Development
You can start a development server that will monitor changes to all CMP and docs files with:
```sh
yarn dev
```

Development server can be accessed at:
`http://localhost:8080/`

## Testing

```sh
yarn test
```
