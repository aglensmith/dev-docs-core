<h1> Products Overview </h1>
<div class="otp" id="no-index">
	<h3>On This Page</h3>
	<ul>
        <li><a href="#products-overview_introduction">Introduction</a></li>
        <li><a href="#products-overview_products">Products</a></li>
        <li><a href="#products-overview_pricing-precision">Pricing Precision </a></li>
        <li><a href="#products-overview_product-images">Product Images</a></li>
        <li><a href="#products-overview_product-videos">Product Videos</a></li>
        <li><a href="#products-overview_custom_fields">Custom Fields</a></li>
        <li><a href="#products-overview_bulk-pricing-rules">Bulk Pricing Rules</a></li>
        <li><a href="#products-overview_metafields">Product Metafields</a></li>
        <li><a href="#products-overview_reviews">Product Reviews</a></li>
        <li><a href="#products-overview_brands">Brands</a></li>
        <li><a href="#products-overview_variant-options">Variant Options</a></li>
        <li><a href="#products-overview_variants">Variants</a></li>
        <li><a href="#products-overview_modifier-options">Modifier Options</a></li>
        <li><a href="#products-overview_complex-rules">Complex Rules</a></li>
        <li><a href="#products-overview_categories">Categories</a></li>
	</ul>
</div>

<a href='#products-overview_introduction' aria-hidden='true' class='block-anchor'  id='products-overview_introduction'></a>

## Introduction

The Catalog refers to a store’s collection of physical and digital products. The Catalog includes all the information about a product such as MPN, warranty, price, and images. 

### Prerequisites
Scopes

The following [OAuth](/api-docs/getting-started/authentication#authentication_oauth-scopes) scopes are required:
* Modify Catalog



<a href='#products-overview_products' aria-hidden='true' class='block-anchor'  id='products-overview_products'></a>

## Products

[Products](/api-reference/catalog/catalog-api/products/getproducts) are the primary catalog entity, and the primary function of the e-commerce platform is to sell products on the storefront and other selling channels.

Products can either be Simple or Complex. 

Products can also be Physical or Digital. 

* Physical products are typically products that exist in a physical form, have a weight, and are being sold by retailers with the intent of shipping them to customers. 

* Digital products, on the other hand, may not have a physical representation in the real world; this includes downloadable products such as computer software, ebooks, music, images, and other digital media. Alternatively, a digital product may be used to sell services such as spa treatments, consulting, and so forth - which also do not require shipping.

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Product Creation
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

### Create a Simple Product

Simple products do not have any options, modifiers, or variants, and therefore cannot be configured or modified before they are added to cart. A simple product is its own variant. 

{'headers': {'Accepts': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{{CLIENT ID}}', 'X-Auth-Token': '{{ACCESS TOKEN}}'}, 'method': 'post', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products', 'body': '{\n  "name": "BigCommerce Coffee Mug",\n  "price": "10.00",\n  "categories": [\n    23,\n    21\n  ],\n  "weight": 4,\n  "type": "physical"\n}'}

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Creating Options
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>



### Create a Complex Product

Complex products have at least one option and may have modifiers or variants.

The [Create Products](/api-reference/catalog/catalog-api/products/getproducts) endpoint supports the creation of multiple variants along with the base product in a single call.

{'headers': {'Accepts': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{{CLIENT ID}}', 'X-Auth-Token': '{{ACCESS TOKEN}}'}, 'method': 'post', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products', 'body': '{\n  "name": "BigCommerce Coffee Mug",\n  "price": "10.00",\n  "categories": [\n    23,\n    21\n  ],\n  "weight": 4,\n  "type": "physical",\n  "variants": [\n    {\n      "sku": "SKU-BLU",\n      "option_values": [\n        {\n          "option_display_name": "Mug Color",\n          "label": "Blue"\n        }\n      ]\n    },\n    {\n      "sku": "SKU-GRAY",\n      "option_values": [\n        {\n          "option_display_name": "Mug Color",\n          "label": "Gray"\n        }\n      ]\n    }\n  ]\n}'}

The [Create a Product](/api-reference/catalog/catalog-api/products/createproduct) endpoint supports the creation of multiple variants along with the base product in a single call.

### Digital Products

Digital products are purchaseable items that don't have a physical representation and are not shipped to the customer; for example, manuals, ebooks, or music. A downloadable product file can be associated with a digital product.

Downloadable product files are intended for products of the “digital” type, typically for selling some kind of media file or software. Product dimensions are not required because the item is not shipped.

Files must be added to digital products using the [Control Panel or WebDav](https://support.bigcommerce.com/articles/Public/Creating-Downloadable-Products/#adding-downloadable-product) (attaching via the API is not supported). Additional settings such as a description of the file and maximum downloads can be set in the Control Panel.

{'headers': {'Accepts': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{{CLIENT ID}}', 'X-Auth-Token': '{{ACCESS TOKEN}}'}, 'method': 'post', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products', 'body': '{\n  "name": "ebook: A Guide to Coffee",\n  "price": "10.00",\n  "categories": [\n    23,\n    21\n  ],\n  "type": "digital",\n  "images": [\n    {\n      "is_thumbnail": true,\n      "image_url": "https://your-custom-image/image_name.png"\n    }\n  ]\n}'}



<a href='#products-overview_pricing-precision' aria-hidden='true' class='block-anchor'  id='products-overview_pricing-precision'></a>

## Pricing Precision

Price can be input using up to 4 decimal places.

Depending on the price, it can round up or down. We allow up to 4 decimal places and use the 5th decimal place to either roundup or down. This holds true for all pricing options available on a product.

Example:

* “price”: 10.99999 - rounds up to 11
* “price”: 10.99994 - rounds down to 10.9999

### Display
Currency settings allows for inputting a large number of decimal places for display. Since pricing precision cuts off at 4, the rest are displayed as zero’s.

<!--
    title: #### Currency Decimal Places

    data: //s3.amazonaws.com/user-content.stoplight.io/6012/1553018091114
-->

#### Currency Decimal Places
![#### Currency Decimal Places
](//s3.amazonaws.com/user-content.stoplight.io/6012/1553018091114 "#### Currency Decimal Places
")



<a href='#products-overview_product-images' aria-hidden='true' class='block-anchor'  id='products-overview_product-images'></a>

## Product Images

[Product images](/api-reference/catalog/catalog-api/product-images/getproductimages) are used to show shoppers what they’re buying and merchandise products. When creating an image, `image_url` or an `image_file` can be passed in. 

If using `image_file` Content-Type needs to be set to 
Content-Type: multipart/form-data. Any other updates using the /POST or /PUT will be rejected with the form-data.

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/images', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}, 'body': '{\n  "is_thumbnail": true,\n  "sort_order": 1,\n  "description": "Yellow Large Bath Towel",\n  "image_url": "https://your-custom-image/image_name.png"\n}'}

### Product Thumbnails

Only one image can be the [product thumbnail](/api-reference/catalog/catalog-api/models/productimage). The product thumbnail is the image that shows on the product listing page, in search results and any other location that features the product. If only one image is on the product it becomes both the thumbnail and the main product image. Images can also be added to [variants](/api-reference/catalog/catalog-api/product-variants/getvariantsbyproductid). 

<!--
title: "Product Thumbnails"
subtitle: "GET https://api.bigcommerce.com/stores/{{store_hash}}/v3/catalog/products/{{product_id}}/images/{{images_id}}"
lineNumbers: true
-->

```json
{
  "data": {
    "id": 382,
    "product_id": 158,
    "is_thumbnail": true,
    "sort_order": 0,
    "description": "",
    "image_file": "a/521/foglinenbeigestripetowel1b_1024x1024__83011__60806.jpg",
    "url_zoom": "https://cdn8.bigcommerce.com/s-{{store_hash}}/products/158/images/382/foglinenbeigestripetowel1b_1024x1024__83011__60806.1534344511.1280.1280.jpg?c=2",
    "url_standard": "https://cdn8.bigcommerce.com/s-{{store_hash}}/products/158/images/382/foglinenbeigestripetowel1b_1024x1024__83011__60806.1534344511.560.850.jpg?c=2",
    "url_thumbnail": "https://cdn8.bigcommerce.com/s-{{store_hash}}/products/158/images/382/foglinenbeigestripetowel1b_1024x1024__83011__60806.1534344511.330.500.jpg?c=2",
    "url_tiny": "https://cdn8.bigcommerce.com/s-{{store_hash}}/products/158/images/382/foglinenbeigestripetowel1b_1024x1024__83011__60806.1534344511.66.100.jpg?c=2",
    "date_modified": "2018-08-15T14:48:31+00:00"
  },
  "meta": {}
}
```



<a href='#products-overview_product-videos' aria-hidden='true' class='block-anchor'  id='products-overview_product-videos'></a>

## Product Videos
[Product Videos](/api-reference/catalog/catalog-api/product-videos/getproductvideos), in addition to images, can help shoppers understand what they’re buying and help sell the product. A product can have more than one video.

* Product videos must be hosted on YouTube. The video_id corresponds to the “v” parameter in a video url. 

Example: <span class=”fp”>https://www.youtube.com/watch?v=<b>R12345677</b></span>

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/videos', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}, 'body': '{\n  "title": "BigCommerce Mug Video",\n  "description": "Video Describing the Mug",\n  "sort_order": 1,\n  "type": "youtube",\n  "video_id": "123345AA"\n}'}



<a href='#products-overview_custom_fields' aria-hidden='true' class='block-anchor'  id='products-overview_custom_fields'></a>

## Custom Fields

[Custom fields](/api-reference/catalog/catalog-api/product-custom-fields/getcustomfields) are a feature intended for product specifications, in a key: value arrangement. As an example, there might be fields indicating technical specifications about an LED TV  such as screen size, maximum resolution, HDR support, etc. Alternatively, if selling wine, I might use Custom Fields for specifications such as vintage, region, grape, etc. Custom fields can not be used to add rules such as changing the weight or price of a product. 

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

Custom Fields are intended to be used in a couple of contexts:

* Displaying specifications on the product detail page and on the product listing pages such as category and brand pages.
* Powering faceted search (searching/filtering by custom field values)

{'method': 'put', 'body': '{\n  "name": "Release Year",\n  "value": "2018"\n}', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/custom-fields', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



<a href='#products-overview_bulk-pricing-rules' aria-hidden='true' class='block-anchor'  id='products-overview_bulk-pricing-rules'></a>

## Bulk Pricing Rules

[Bulk Pricing Rules](/api-reference/catalog/catalog-api/product-bulk-pricing-rules/getbulkpricingrules) are intended for merchants who want to offer wholesale discounts for buying in bulk. They apply once products are added to cart, but they are displayed as a callout on the storefront to let shoppers know how they can save.

Bulk Pricing rules in the catalog are on the product, meaning that they’ll trigger even if several different variants of the product are in the cart, as long as the total quantity of those variants meets one of the quantity breaks. [Price List bulk pricing](/api-reference/catalog/pricelists-api/price-lists-records/setpricelistrecordcollection) works differently.

{'method': 'put', 'body': '{\n  "bulk_pricing_rules": [\n    {\n      "quantity_min": 10,\n      "quantity_max": 15,\n      "type": "price",\n      "amount": 3\n    },\n    {\n      "quantity_min": 16,\n      "quantity_max": 25,\n      "type": "price",\n      "amount": 5\n    }\n  ]\n}', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/bulk-pricing-rules', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



<a href='#products-overview_metafields' aria-hidden='true' class='block-anchor'  id='products-overview_metafields'></a>

## Product Metafields

[Metafields](/api-reference/catalog/catalog-api/product-metafields/createproductmetafield) allow a developer to set up key and namespace pairs to store data against a resource, like a product. The data does not appear in the storefront or the control panel. This is useful for when information needs to be passed back and forth between an app and the store. 

Metafields can be added to variants, products, categories, and brands.

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/metafields', 'body': '{\n  "permission_set": "read",\n  "namespace": "Location",\n  "key": "bin_number",\n  "value": "#4456",\n  "description": "location of the product",\n  "resource_type": "product",\n  "resource_id": 131\n}', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



<a href='#products-overview_reviews' aria-hidden='true' class='block-anchor'  id='products-overview_reviews'></a>

## Product Reviews
[Product reviews ](/api-reference/catalog/catalog-api/product-reviews/getproductreviews)contains ratings and feedback from shoppers who have purchased a product. Reviews are displayed on product pages. 

Reviews cannot be created in the control panel, but they can be created via API. Creating them via API is useful if you are migrating to BigCommerce from another platform and do not want to lose existing reviews. 

Product Reviews are a native platform feature, but they can be turned off in favor of a custom setup.

{'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/reviews', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}, 'method': 'post', 'body': '{\n  "title": "Great Coffee Mug",\n  "text": "This coffee mug kept my liquids hot for several hours.",\n  "status": "pending",\n  "rating": 5,\n  "email": "testing@bigcommerce.com",\n  "name": "BigCommerce",\n  "date_reviewed": "2018-07-20T17:45:13+00:00"\n}'}



<a href='#products-overview_brands' aria-hidden='true' class='block-anchor'  id='products-overview_brands'></a>

## Brands

[Brands](/api-reference/catalog/catalog-api/brands/getbrands) are another form of catalog taxonomy, similar to Categories. However, there are a few differences:

* Exist as a single “list” on the store, with no tree structure
* Can only have a single assignment to a product; a product may have at most one brand, but a brand can have many products.
 
They’re primarily used to tag products so that consumers can find Brands they’re interested in (such as Nike shoes). Brands have their own page on the storefront which shows all the products in that Brand. They’re also used as part of faceted search navigation.

{'method': 'post', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/brands', 'body': '{\n  "name": "BigCommerce",\n  "page_title": "BigCommerce",\n  "meta_keywords": [\n    "ecommerce",\n    "best in class",\n    "grow your business"\n  ],\n  "image_url": "https://your-custom-image.png"\n}', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



<a href='#products-overview_variant-options' aria-hidden='true' class='block-anchor'  id='products-overview_variant-options'></a>

## Variant Options

[Variant options](/api-reference/catalog/catalog-api/product-variant-options/getoptions) are any choices that the shopper needs to make that will result in the selection of a variant. Color and Size are typical examples of Variant Options.  A t-shirt can have different combinations of sizes and colors.  

Example:
* Color is a Variant Option; Red, Orange, and Green are Variant Option Values
* Size is a Variant Option; Small, Medium, and Large are Variant Option Values

The combination of Small & Red is what is selected on the storefront and correlates to a product variation, also called a SKU. 
 
**Variant options:**

* Require the shopper to select a value
* Only support “multiple choice” option types
* Rectangle
* Radio button
* Color swatch
* Product pick list
* Product pick list with images
* Will automatically generate variants when created in the CP
* Are auto-generated from variants when a product is created with variants via V3 API Product /POST


### Variant Options Example:

| If the product is | Variant Option |
| -- | -- |
| T-Shirt | Blue</br>----------</br> Small<br> Medium</br> Large|
| Backpack | Black</br>Yellow<br>----------<br>2L <br> 3L<br> 8L |


### Options created on V2 and V3

* Variant options created on V3 cannot be accessed from the Control Panel. They can only be accessed via the API.
* If a product has options that were created using the V2 API, additional options cannot be added using the V3 API.
* SKUs in V2 map to variants in V3.
* Base variants are not SKUs in V2.

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

### Create Variant Options
The following request will create options that will show on the storefront as choices that can be selected by the customer. In a separate request, you could build out SKUs based on these variant
option values or a combination of variant option
values. A request like this could also be used to
add new choices to a variant that has already been created.

<!--
title: "Create Size Variant Option"
subtitle: "/POST https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/options"
lineNumbers: true
-->

```
{
  "product_id": 134,
  "name": "Size Rectangle",
  "display_name": "Size",
  "type": "rectangles",
  "option_values": [
    {
      "label": "S",
      "sort_order": 0,
      "is_default": false
    },
    {
      "label": "M",
      "sort_order": 1,
      "is_default": true
    },
    {
      "label": "L",
      "sort_order": 2,
      "is_default": false
    }
  ]
}
```



<a href='#products-overview_variants' aria-hidden='true' class='block-anchor'  id='products-overview_variants'></a>

## Variant
[Variants](/api-reference/catalog/catalog-api/product-variants/getvariantsbyproductid) represent an item as it sits on the shelf in the warehouse or a particular saleable product. A product might be a t-shirt, while the variant would be “a small, red t-shirt”. Variants are selected by shoppers on the storefront via Product Options. In the case where a product is simple, meaning it does not have any options, the product is its own variant - called a base variant. Everything you can buy should be a variant.

* Options build out variants. 
* Variants are usually what inventory is tracked against 
* Can have their own price, weight, dimensions, image, etc - or they can inherit these values from the product if they have not been specified
* Must have a SKU code (unless they’re a base variant)
* In the case of non-base variants, variants will relate to a particular combination of variant option values - such as “small” and “red”

### Variants:

| If the product is | Variant Option | Variant |
| -- | -- | -- |
| T-Shirt | Blue</br>----------</br> Small<br> Medium</br> Large| SM-BLU<br> SM-MED <br> SM-LARG
| Backpack | Black</br>Yellow<br>----------<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L</br>----------<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L|


## Create a Variant
Variants can be created in two ways:
* From existing variant options using the variant options endpoint. [v3/catalog/products/{product_id}/options](/api-reference/catalog/catalog-api/product-variants/createvariant)
* By adding the variants with variant options and skus when creating the product. See [Create a Complex Product](/api-reference/catalog/catalog-api/products/createproduct).

This will go over using existing variant options to create the variants.

Use the `https://api.bigcommerce.com/stores/{{store_hash}}/v3/catalog/products/131/options` endpoint to get the option information.

<!--
title: "Example Response"
subtitle: "/GET https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/options"
lineNumbers: true
-->

```json
{
  "data": [
    {
      "id": 193,
      "product_id": 134,
      "name": "Size1533313432-134",
      "display_name": "Size",
      "type": "rectangles",
      "sort_order": 0,
      "option_values": [
        {
          "id": 163,
          "label": "S",
          "sort_order": 0,
          "value_data": null,
          "is_default": false
        },
        {
          "id": 164,
          "label": "M",
          "sort_order": 1,
          "value_data": null,
          "is_default": true
        },
        {
          "id": 165,
          "label": "L",
          "sort_order": 2,
          "value_data": null,
          "is_default": false
        }
      ],
      "config": []
    },
    {
      "id": 194,
      "product_id": 134,
      "name": "Color1533313946-134",
      "display_name": "Color",
      "type": "swatch",
      "sort_order": 1,
      "option_values": [
        {
          "id": 166,
          "label": "Blue",
          "sort_order": 1,
          "value_data": {
            "colors": [
              "#123C91"
            ]
          },
          "is_default": false
        },
        {
          "id": 167,
          "label": "Green",
          "sort_order": 2,
          "value_data": {
            "colors": [
              "#0F961E"
            ]
          },
          "is_default": false
        },
        {
          "id": 168,
          "label": "Red",
          "sort_order": 3,
          "value_data": {
            "colors": [
              "#E60C0C"
            ]
          },
          "is_default": false
        }
      ],
      "config": []
    }
  ],
  "meta": {
    "pagination": {
      "total": 2,
      "count": 2,
      "per_page": 50,
      "current_page": 1,
      "total_pages": 1,
      "links": {
        "current": "?page=1&limit=50"
      }
    }
  }
}
```

{'method': 'get', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/options', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

In the above response, there are two variant options of size and color with three values each. 

To combine the variant option values into variants and build out SKUs use the following endpoint:

`https://api.bigcommerce.com/stores/{{store_hash}}/v3/catalog/products/131/variants`

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/variants', 'body': '{\n  "cost_price": 3,\n  "price": 12.99,\n  "retail_price": 15.99,\n  "weight": 1,\n  "width": 4,\n  "height": 14.6,\n  "depth": 22,\n  "is_free_shipping": true,\n  "purchasing_disabled": true,\n  "purchasing_disabled_message": "This item not available at this time.",\n  "product_id": 134,\n  "sku": "SMALL-BLUE",\n  "option_values": [\n    {\n      "id": 163,\n      "option_id": 193\n    },\n    {\n      "id": 166,\n      "option_id": 194\n    }\n  ]\n}', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

The `option_values` array combines the options Small and Blue to create the SKU SMALL-BLUE. The id in the option_values array is the id from the variant option response option_values > id. The option_id is the id of the option.

<!--
title: ""
subtitle: ""
lineNumbers: true
-->

```json
 {
            "id": 193, //option_id
            "product_id": 134,
            "name": "Size1533313432-134",
            "display_name": "Size",
            "type": "rectangles",
            "sort_order": 0,
            "option_values": [
                {
                    "id": 163, //id
                    "label": "S",
                    "sort_order": 0,
                    "value_data": null,
                    "is_default": false
                }
								...
```

### Create a Variant Using the Products Endpoint

The following example creates a base product, variant options, and variants in a single call to the /products endpoint. You can use this method to create a product and its variants in a single call without creating variant options first, but the option display type will default to radio button.

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Supported Types
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

{'method': 'post', 'body': '{\n  "name": "BigCommerce Coffee Mug",\n  "price": "10.00",\n  "categories": [\n    23,\n    21\n  ],\n  "weight": 4,\n  "type": "physical",\n  "variants": [\n    {\n      "sku": "SKU-BLU",\n      "option_values": [\n        {\n          "option_display_name": "Mug Color",\n          "label": "Blue"\n        }\n      ]\n    },\n    {\n      "sku": "SKU-GRAY",\n      "option_values": [\n        {\n          "option_display_name": "Mug Color",\n          "label": "Gray"\n        }\n      ]\n    }\n  ]\n}', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



<a href='#products-overview_modifier-options' aria-hidden='true' class='block-anchor'  id='products-overview_modifier-options'></a>

## Modifier Options

[Modifier options](/api-reference/catalog/catalog-api/product-modifiers/getmodifiers) are any choices that the shopper can make that will change the way the merchant fulfills the product. Examples include:
* A checkbox to add shipping insurance
* Text to be engraved on the product
* A color that an unfinished product is to be painted before it’s shipped
 
Critically, the modifier will not change the SKU/variant being fulfilled, and you cannot track inventory against combinations of modifier values. Modifiers typically would not change which product is “picked off the shelf” in the warehouse, but they change what happens to that product before it’s sent to the shopper, or how it’s sent.
 
Modifier options:
* May be required or non-required
* Support all option types
* Cannot be used as part of a variant


An adjuster can be added to a modifier option to change things such as increasing the price, changing the weight, or shipping rules.  Adjusters cannot be applied to all modifier types.

### Modifier Options Example:

| If the product is | Variant Option | Variant |Modifier |
| -- | -- | -- | -- |
| T-Shirt | Blue</br>----------</br> Small<br> Medium</br> Large| SM-BLU<br> SM-MED <br> SM-LARG| Checkbox<br>Donate to Charity|
| Backpack | Black</br>Yellow<br>----------<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L</br>----------<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L| Text Field<br> Add Embroidery|

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Modifiers that support Adjusters
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

### Add a modifier with price adjuster to an existing product

The following example shows how to add a modifier, a checkbox with a price adjuster, that will increase the product's price by five dollars. 

Creating a checkbox with an adjuster requires two separate calls: one to create the checkbox and a second to add the adjuster. Adjusters are defined within the `option_values` array, but `option_values` are not allowed in the request to create a checkbox modifier because creating a checkbox automatically generates two mandatory option values: a Yes and a No. Once the checkbox has been created along with its option values, you can update the modifier to add an adjuster. 

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Modifiers that require a second step to add an adjuster
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

First, a POST to create the modifier. 

{'method': 'put', 'body': '{\n  "type": "checkbox",\n  "required": false,\n  "config": {\n    "default_value": "Yes",\n    "checked_by_default": false,\n    "checkbox_label": "Check for Donation"\n  },\n  "display_name": "Add a $5 Donation"\n}', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/modifiers', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

Since this is a checkbox which has two states, checked/unchecked or yes/no, two option values are created. The default adjuster values are null. 

<!--
title: "Response"
subtitle: "Create Modifier Option"
lineNumbers: true
-->

```
{
  "data": [
    {
      "id": 160,
      "product_id": 131,
      "name": "Add-a-$5-Donation1535039590-191",
      "display_name": "Add a $5 Donation",
      "type": "checkbox",
      "required": false,
      "config": {
        "checkbox_label": "Check for Donation",
        "checked_by_default": false
      },
      "option_values": [
        {
          "id": 149,
          "option_id": 160,
          "label": "Yes",
          "sort_order": 0,
          "value_data": {
            "checked_value": true
          },
          "is_default": false,
          "adjusters": {
            "price": {
              "adjuster": null,
              "adjuster_value": null
            },
            "weight": null,
            "image_url": "",
            "purchasing_disabled": {
              "status": false,
              "message": ""
            }
          }
        },
        {
          "id": 150,
          "option_id": 160,
          "label": "No",
          "sort_order": 1,
          "value_data": {
            "checked_value": false
          },
          "is_default": true,
          "adjusters": {
            "price": null,
            "weight": null,
            "image_url": "",
            "purchasing_disabled": {
              "status": false,
              "message": ""
            }
          }
        }
      ]
    }
  ],
  "meta": {
    "pagination": {
      "total": 1,
      "count": 1,
      "per_page": 50,
      "current_page": 1,
      "total_pages": 1,
      "links": {
        "current": "?page=1&limit=50"
      }
    }
  }
}
```

Next send a PUT request to update the modifier value. This increases the price by $5 when the Yes option value is selected.

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/modifiers/{modifier_id}/values', 'body': '{\n  "is_default": false,\n  "adjusters": {\n    "price": {\n      "adjuster": "relative",\n      "adjuster_value": 5\n    }\n  }\n}', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

### Troubleshooting: 422 Error

<!--
title: ""
subtitle: ""
lineNumbers: true
-->

```json
{
    "status": 422,
    "title": "The product is currently associated with an option set, please remove it before editing an option or modifier.",
    "type": "https://developer.bigcommerce.com/api#api-status-codes",
    "errors": {
        "product_id": "The product is currently associated with an option set, please remove it before editing an option or modifier."
    }
}
```

To fix this error:
* Modify the products using the V2 API
* Remove the option set using the V2 API or the Control Panel, then remake the variants and modifiers using V3



<a href='#products-overview_complex-rules' aria-hidden='true' class='block-anchor'  id='products-overview_complex-rules'></a>

## Complex Rules

[Complex rules](/api-reference/catalog/catalog-api/product-complex-rules/getcomplexrules) allow merchants to set up conditions and actions based on shopper option selections on the storefront. You can use them to vary the following based on option selections made by the shopper:
* Price
* Weight
* Image
* Purchasability

Adjustments made by complex rules are displayed to shoppers in real-time on the storefront.

For the majority of merchant use cases, **best practice** will be to either assign values (such as a price) directly to a variant or use adjusters on the modifier option itself. However complex rules exist for rare cases where a rule condition is too complex to express in those forms easily. 

Use complex rules when an adjustment should be triggered by:
* The selection of values across multiple modifier options
* The combination of a particular variant/SKU and a modifier option value.

### Complex Rules Example:

| If the product is | Variant Option | Variant |Modifier | Complex Rule |
| -- | -- | -- | -- | -- |
| T-Shirt | Blue</br>----------</br> Small<br> Medium</br> Large| SM-BLU<br> SM-MED <br> SM-LARG| Checkbox<br>Donate to Charity| Checkox<br> Donate to Charity.<br> Add $5
| Backpack | Black</br>Yellow<br>----------<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L</br>----------<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L| Text Field<br> Add Embroidery| N/A

<br>

### Creating Complex Rules Based On Modifiers

Complex rules must be based on a combination of two or more modifiers, such as two checkboxes. The following example will add $10 to the product price when both boxes are checked. 

{'method': 'put', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/{product_id}/complex-rules', 'body': '{\n  "product_id": 1200,\n  "enabled": true,\n  "price_adjuster": {\n    "adjuster_value": 10\n  },\n  "conditions": [\n    {\n      "modifier_id": 506,\n      "modifier_value_id": 852\n    },\n    {\n      "modifier_id": 507,\n      "modifier_value_id": 854\n    }\n  ]\n}', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

### Troubleshooting

Complex rules must consist of multiple conditions that trigger the rule adjustment. If multiple conditions are not specified, the request will return a 422 Unprocessable Entity:

<!--
title: ""
subtitle: ""
lineNumbers: true
-->

```json
{
    "status": 422,
    "title": "The rule must contain multiple modifier conditions with unique modifier ids or a variant condition and modifier condition",
    "type": "https://developer.bigcommerce.com/api#api-status-codes"
}
```



<a href='#products-overview_categories' aria-hidden='true' class='block-anchor'  id='products-overview_categories'></a>

## Categories

[Categories](/api-reference/catalog/catalog-api/category/getcategories) are a hierarchy of products available on the store, presented in a tree structure. A store’s category structure determines the primary menu structure of most storefront themes, which are directly tied to it.

All products must be associated with at least one Category, although a Category does not need to contain any products. Unlike some e-commerce platforms, products on BigCommerce can be associated with more than one Category. 

A product associated with categories does not currently have any priority or weighted order (there’s no “primary category”), which can make it difficult to integrate with some external systems which might wish to use a product’s categories to map to a category structure in that external system.

{'method': 'post', 'body': '{\n  "parent_id": 18,\n  "name": "Shoes",\n  "description": "Shoes Available for purchase",\n  "sort_order": 1,\n  "page_title": "Shoes",\n  "is_visible": true\n}', 'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/categories', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}

### Category Tree

[Category Tree](/api-reference/catalog/catalog-api/catalog/getcatalogsummary) returns a simple view of the parent > child relationship of all categories in the store. This endpoint can be used to fetch the categories if building out a custom navigation for a store.

<!--
title: "Category Tree Response Example"
subtitle: ""
lineNumbers: true
-->

```json
{
  "data": [
    {
      "id": 33,
      "parent_id": 0,
      "name": "Clothing",
      "is_visible": true,
      "url": "/clothing/",
      "children": []
    },
    {
      "id": 23,
      "parent_id": 0,
      "name": "Shop All",
      "is_visible": true,
      "url": "/shop-all/",
      "children": []
    },
    {
      "id": 25,
      "parent_id": 0,
      "name": "Towels",
      "is_visible": true,
      "url": "/towels/",
      "children": [
        {
          "id": 26,
          "parent_id": 25,
          "name": "Bath Towels",
          "is_visible": true,
          "url": "/towels/bath-towels/",
          "children": [
            {
              "id": 30,
              "parent_id": 26,
              "name": "Bath Towels",
              "is_visible": true,
              "url": "/towels/bath-towels/bath-towels/",
              "children": []
            },
            {
              "id": 29,
              "parent_id": 26,
              "name": "Hand Towels",
              "is_visible": true,
              "url": "/towels/bath-towels/hand-towels/",
              "children": [
                {
                  "id": 31,
                  "parent_id": 29,
                  "name": "Washcloths",
                  "is_visible": true,
                  "url": "/towels/bath-towels/hand-towels/wash-cloths/",
                  "children": []
                }
              ]
            }
          ]
        },
        {
          "id": 28,
          "parent_id": 25,
          "name": "Beach Towels",
          "is_visible": true,
          "url": "/towels/beach-towels/",
          "children": []
        },
        {
          "id": 27,
          "parent_id": 25,
          "name": "Kitchen Towels",
          "is_visible": true,
          "url": "/towels/kitchen-towels/",
          "children": []
        }
      ]
    },
    {
      "id": 18,
      "parent_id": 0,
      "name": "Bath",
      "is_visible": true,
      "url": "/bath/",
      "children": [
        {
          "id": 34,
          "parent_id": 18,
          "name": "Shoes",
          "is_visible": true,
          "url": null,
          "children": []
        }
      ]
    },
    {
      "id": 32,
      "parent_id": 0,
      "name": "Hoodies",
      "is_visible": true,
      "url": "/hoodies/",
      "children": []
    },
    {
      "id": 19,
      "parent_id": 0,
      "name": "Garden",
      "is_visible": true,
      "url": "/garden/",
      "children": []
    },
    {
      "id": 21,
      "parent_id": 0,
      "name": "Kitchen",
      "is_visible": true,
      "url": "/kitchen/",
      "children": []
    },
    {
      "id": 20,
      "parent_id": 0,
      "name": "Publications",
      "is_visible": true,
      "url": "/publications/",
      "children": []
    },
    {
      "id": 22,
      "parent_id": 0,
      "name": "Utility",
      "is_visible": true,
      "url": "/utility/",
      "children": []
    }
  ],
  "meta": {}
}
```

{'url': 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/summary', 'method': 'get', 'headers': {'Accept': 'application/json', 'Content-Type': 'application/json', 'X-Auth-Client': '{$$.env.X-Auth-Client}', 'X-Auth-Token': '{$$.env.X-Auth-Token}'}}



## Resources

### Webhooks
* [Products](/api-docs/getting-started/webhooks/webhook-events#webhook-events_products)
* [Categories](/api-docs/getting-started/webhooks/webhook-events#webhook-events_category)
* [SKU](/api-docs/getting-started/webhooks/webhook-events#webhook-events_sku)

### Related Endpoints
* [Catalog API](/api-reference/catalog/catalog-api)
