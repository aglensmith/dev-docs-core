<h1>schema.json (Store Design Metadata)</h1>

<div class="otp" id="no-index">
	<h3> On This Page </h3>
	<ul>
    <li><a href="#schema_enabling">Enabling Store Design</a></li>
    <li><a href="#schema_best-practices">Best Practices</a></li>
    <li><a href="#schema_how-json">How .json Entries Govern Store Design's UI</a></li>
    <li><a href="#schema_theme-editor-data">Store Designs Data Types</a></li>
    <li><a href="#schema_data-structure">Store Design Data Structure in schema.json</a></li>
    <li><a href="#schema_ui-scope">Arbitrary UI Scope and Sequence</a></li>
	</ul>
</div>

<a href='#schema_enabling' aria-hidden='true' class='block-anchor'  id='schema_enabling'></a>

## Enabling Store Design

To provide merchants with Store Design support for your theme's settings, you must declare those settings in the theme's <span class="fn">schema.json file</span>. You must also include those settings in your theme's <span class="fn">config.json</span> file, templates, and Sass/CSS files. The basic division of labor is this:
* <span class="fn">schema.json</span> is an array of objects, declaring which theme settings are editable in Store Design. These objects also declare all possible values to display in Store Design's GUI.
* <span class="fn">config.json</span> assigns (and updates) a default value for each of the editable settings.
* Each <span class="fn">schema.json</span> entry has an id element that maps it to its corresponding config.json entry. The id value identifies the relevant config.json key name.
* For front-matter properties to be editable, your theme's Handlebars template must call certain Handlebars helpers to transform the config.json entries into JavaScript values.
* For fonts to be editable, a Sass stylesheet must call certain custom Sass functions to transform the <span class="fn">config.json</span> font entries into CSS values.
* For styles to be editable, a Sass stylesheet must call certain custom Handlebars helpers to transform the <span class="fn">config.json</span> entries into CSS values.

As users select options within the Store Design UI (and save their selections), Stencil will automatically rewrite <span class="fn">config.json</span> to record new defaults for the theme.

### File Management Requirements

See Stencil's default Cornerstone theme for examples that fulfill all of the above requirements. However, remember these hard requirements:

* For any theme setting (such as a Sass variable or a front-matter value) to be merchant-customizable,
that setting – and its possible values – must be present in <span class="fn">schema.json</span>. You must manually provide these declarations, according to the structure described here.

* Also, each key that you create in schema.json must have a corresponding <span class="fn">config.json</span> key whose name matches its id value. This <span class="fn">config.json</span> key sets the default value (even if that is simply an empty string). A <span class="fn">schema.json</span> setting without an `id`-matched <span class="fn">config.json</span> key will not appear to users in the Store Design GUI.

<a href='#schema_best-practices' aria-hidden='true' class='block-anchor'  id='schema_best-practices'></a>

## Best Practices

Please follow these guidelines to head off errors upon theme upload, and to avoid possible loss of customizations made via the Store Design GUI at runtime:

* Single-Instance Restriction per Storefront: We strongly recommend opening only one instance of Store Design, at a time, against each storefront. This is because there is currently no synchronization mechanism to reconcile configuration changes made by multiple Store Design instances. So <span class="fn">schema.json</span> will record the last changes made by any instance – but changes saved earlier by other instances might be lost.

* Single-Storefront Restriction per Editor: In the current release, users can have only one storefront at a time open in Store Design. (A workaround is to open an "Incognito"/private-browsing window on an additional storefront, to bypass the cookie that imposes this restriction.)

* File Name, Location, and Structure: Your theme's <span class="fn">schema.json</span> file must be named schema.json, must reside in the root of your `<theme-name>` subdirectory (e.g.: <span class="fp">/cornerstone/schema.json</span>), and must be valid JSON.

* File Size: The maximum allowable size for a theme's <span class="fn">schema.json</span> file is 64 KB. Exceeding this limit will trigger an error upon uploading the theme to BigCommerce. (Other than this size constraint, there is no limit on the number of keys and values that you can place in a theme's <span class="fn">schema.json</span>.)



<a href='#schema_how-json' aria-hidden='true' class='block-anchor'  id='schema_how-json'></a>

## How .json Entries Govern Store Design's UI

Your entries in the <span class=”fn”>schema.json</span> and <span class=”fn”>config.json</span> directly shape users' options in Store Design:
* Theme Variations always appear at the top of the Store Design panel. These variations are defined only in <span class="fn">config.json</span>, and their definition order in that file governs their display order in Store Design.
* Merchants must select one variation to edit, at a time, in Store Design. The selections that they make in the remainder of Store Design's UI will apply to only that selected variation.
* Store Design's remaining sequence of top-level (Section) headings corresponds directly to the sequence of top-level (Section) objects that you declare in `schema.json`

The options displayed within these expandable Section headings correspond directly to the keys/values that you nest within <span class="fn">schema.json</span>'s corresponding Section objects.

In all, the structure that you give your theme's <span class="fn">config.json</span> and <span class="fn">schema.json</span> files directly governs the UI that Store Design exposes to merchants. So these files provide your UI design tools.

<a href='#schema_theme-editor-data' aria-hidden='true' class='block-anchor'  id='schema_theme-editor-data'></a>

## Store Design Data Types

Store Design supports these data types:
* color
* font
* select [drop-down list]
* checkbox
* imageDimension
* text

Within <span class="fn">schema.json</span>, each object's data type is declared in a statement like the one highlighted here:


<!--
title: ""
subtitle: ""
lineNumbers: true
-->

```json
 {
        "type": "color",
        "label": "Text Color",
        "id": "body-font-color"
      },
```

### Types versus "heading" Labels

Within <span class="fn">schema.json</span>, you will also see `"type": "heading"` statements like this one – highlighted earlier in the same object used for the above example:

<!--
title: ""
subtitle: ""
lineNumbers: true
-->

```json
{
    "name": "Colors",
    "settings": [
      {
        "type": "heading",
        "content": "General"
      },
      {
        "type": "color",
        "label": "Text Color",
        "id": "body-font-color"
      },
    {...}
     ]
}
```

These `"type": "heading"` statements do not reference data types. Rather, they declare display captions for the Store Design UI's subcategories – the middle level nested within the Section headings, but outside the individual options from which merchants can select. (Those inner options are designated by `"label": <label-text>` statements.)

<a href='#schema_data-structure' aria-hidden='true' class='block-anchor'  id='schema_data-structure'></a>

## Store Design Data Structure in <span class="fn">schema.json</span> 

The <span class="fn">schema.json</span> nesting structure that you just saw maps directly to the Store Design UI displayed to merchants: Below the `variations` section (whose data are imported from <span class="fn">config.json</span>), the order and nesting of options in Store Design's UI directly matches the order and nesting of your <span class="fn">schema.json</span> entries.


<a href='#schema_ui-scope' aria-hidden='true' class='block-anchor'  id='schema_ui-scope'></a>

## Arbitrary UI Scope and Sequence

You are free to decide which properties of your theme to make editable in Store Design, and in which order to display them. Store Design can expose any set of properties as long as your <span class="fn">schema.json</span> declares them using the data types that Store Design supports.

