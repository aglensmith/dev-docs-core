<h1>Using Custom Fonts</h1>

<div class="otp" id="no-index">
	<h3> On This Page </h3>
	<ul>
    <li><a href="#using-custom-fonts_stage-the-fonts">Stage the Fonts</a></li>
    <li><a href="#using-custom-fonts_reference-fonts">Reference Fonts in Templates' <code>head</code></a></li>
    <li><a href="#using-custom-fonts_video-demo">Video Demo</a></li>
    <li><a href="#using-custom-fonts_update-the-css">Update the CSS</a></li>
	</ul>
</div>


<div class="HubBlock--callout">
<div class="CalloutBlock--warning">
<div class="HubBlock-content">
    
<!-- theme: warning -->

### Custom Fonts Unavailable on Theme Editor
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

<a href='#using-custom-fonts_stage-the-fonts' aria-hidden='true' class='block-anchor'  id='using-custom-fonts_stage-the-fonts'></a>

## Stage the Fonts

First, acquire your custom fonts. In this logo scenario, we'll assume the single (nonexistent) font `MyFontFile.ttf`.
Next, [use WebDav to upload each custom font](). (Upload to WebDAV's default `/content/` folder.)




<a href='#using-custom-fonts_reference-fonts' aria-hidden='true' class='block-anchor'  id='using-custom-fonts_reference-fonts'></a>

## Reference Fonts in Templates' `<head>`

Next, edit the appropriate template files' `<head>` sections to reference your custom fonts. In this logo example, you would edit the `/cornerstone/templates/layout/base.html` file's `<head>` section to insert the following code, which references the custom font you just uploaded:
	
```
<style type="text/css" media="screen, print">
           @font-face {
               font-family: "MyFont";
               src: url("{{cdn 'webdav:MyFontFile.ttf'}}");
           }
</style>
```



<a href='#using-custom-fonts_video-demo' aria-hidden='true' class='block-anchor'  id='using-custom-fonts_video-demo'></a>

## Video Demo

Watch a video demonstration of referencing custom fonts in your template files' `<head>` sections: 

<iframe width="560" height="315" src="https://www.youtube.com/embed/-w7Hbn_p_pw" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>



<a href='#using-custom-fonts_update-the-css' aria-hidden='true' class='block-anchor'  id='using-custom-fonts_update-the-css'></a>

## Update the CSS

Finally, update the appropriate CSS to reference the same font. Here, you would edit the `/cornerstone/assets/scss/layouts/header/_header.scss` file to include the two lines below `.header-logo-text`:

```
.header-logo-text {
display: block;
   font-family: 'MyFont';
   [...]
}
```

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
<!-- theme:  -->

### Notes
> There is no way to re-display this pop-up after selecting Done, so be sure to securely store the credentials before leaving this screen.

</div>
</div>
</div>

