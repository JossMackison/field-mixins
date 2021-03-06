Field Mixins
============

A collection of [Jade mixins](http://jade-lang.com/reference/#mixins) for defining form fields. Whilst anyone is welcome to use these mixins they were initially crafted for recreating a front-end admin UI for [KeystoneJS](https://github.com/JedWatson/keystone) applications. The style and structure follows [Bootstrap's](https://github.com/twbs/bootstrap) form implementation, but could easily be repurposed.

To get a better idea of how you might use them checkout the [real world example](http://www.jossmackison.me/playpen/field-mixins).




## Quickstart

If you have [Bower](http://bower.io/) installed run the following command in the root of your project:

```bash
bower install jade-field-mixins
```




## Table of Contents  
- [Standalone](#standalone)
  - [Field](#field)
  - [Textarea](#textarea)
  - [Cloudinary Image](#cloudinary-image)
  - [Checkbox](#checkbox)
  - [Checkbox Inline](#checkbox-inline)
  - [Radio Button](#radio-button)
  - [Radio Button Inline](#radio-button-inline)
  - [Address field](#address-field)
  - [Upload](#upload)
  - [Icon Field](#icon-field)
  - [Character Field](#character-field)
  - [Button](#button)
- [Labelled](#labelled)
  - [Labelled Field](#labelled-field)
  - [Labelled Textarea](#labelled-textarea)
  - [Labelled Cloudinary Image](#labelled-cloudinary-image)
  - [Labelled Checkbox](#labelled-checkbox)
  - [Labelled Address field](#labelled-address-field)
  - [Labelled Upload](#labelled-upload)
  - [Labelled Button](#labelled-button)
- [Attributes](#attributes)





<a name="standalone">
## Standalone Fields

<a name="field">
### Field

The base input field that we extend to build everything. Accepted arguments:
* type (String) : defaults to "text"
* name (String)
* value (String)
* placeholder (String)

```Jade
+field({ type: 'email', name: 'email', value: 'email@example.com', placeholder: 'Email Address' })
```

Will yield:

```HTML
<input type="email" class="form-control" name="email" value="email@example.com" placeholder="Email Address">
```

<a name="textarea">
### Textarea

A simple textarea. Accepted arguments:
* name (String)
* value (String)
* placeholder (String)

```Jade
+textarea({ name: 'message', value: 'Hi there', placeholder: 'Message' })
```

Will yield:

```HTML
<textarea name="message" class="form-control" placeholder="Message">Hi there</textarea>
```

<a name="cloudinary-image">
### Cloudinary Image

Detect the existance of an image and display it, otherwise just show the upload field. Accepted arguments:
* name (String)
* value (Object) { secure_url, url, resource_type, format, height, width, signature, version, public_id }
* dimensions (Boolean) displays the image dimensions top left
* url (Boolean) provides a url for the full image
* upload args (name, note)

```Jade
+cloudinary_image({ name: 'profileAvatarImage', value: {...}, dimensions: true, url: true, note: 'Recommended: 200&times;300px' })
```

Will yield:

```HTML
<div class="image-field">
  <div class="image-field__object">
    <a class="image-field__url" href="...">
      <img class="image-field__image" src="...">
    </a>
    <span class="image-field__dimensions">400 × 600</span>
  </div>
  <div class="image-field__body">
    <div class="field-upload">
      <input type="file" name="profileAvatarImage_upload">
      <div class="form-info">Recommended: 200×300px</div>
    </div>
    <label class="image-field__label">
      <input type="checkbox" class="image-field__checkbox" value="delete" name="profileAvatarImage_action">
        <span class="btn btn-narrow btn-default image-field__label-remove">Remove</span>
        <span class="btn btn-narrow btn-default image-field__label-undo">Undo</span>
        <span class="image-field__label-save">Removed. Save to delete.</span>
    </label>
  </div>
</div>
```

<a name="checkbox">
### Checkbox

For a single checkbox, or list of checkboxes. Accepted arguments:
* checkboxlabel (String)
* name (String)
* value (String) : defaults to "true"
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ checkboxlabel: 'I accept the Terms and Conditions', name: 'acceptedTermsAndConditions' })
```

Will yield:

```HTML
<div class="checkbox">
  <label>
    <input type="checkbox" value="true" name="acceptedTermsAndConditions">
    I accept the Terms and Conditions
  </label>
</div>
```

<a name="checkbox-inline">
### Checkbox Inline

For a group of inline checkboxes. Accepted arguments:
* checkboxlabel (String)
* name (String)
* value (String) : defaults to "true"
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox-inline({ checkboxlabel: 'I accept the Terms and Conditions', name: 'acceptedTermsAndConditions' })
```

Will yield:

```HTML
<label class="checkbox-inline">
  <input type="checkbox" value="true" name="acceptedTermsAndConditions">
  I accept the Terms and Conditions
</label>
```

<a name="radio-button">
### Radio Button

For a single radio button, or list of radio buttons. Accepted arguments:
* radiolabel (String)
* name (String)
* value (String)
* checked (Boolean)
* disabled (Boolean)

```Jade
+radio({ radiolabel: 'Jade', name: 'templatelang_jade' })
```

Will yield:

```HTML
<div class="radio">
  <label>
    <input type="radio" value="true" name="templatelang_jade">
    Jade
  </label>
</div>
```

<a name="radio-button-inline">
### Radio Button Inline

For a group of inline radio buttons. Accepted arguments:
* radiolabel (String)
* name (String)
* value (String)
* checked (Boolean)
* disabled (Boolean)

```Jade
+radio-inline({ radiolabel: 'Jade', name: 'templatelang_jade' })
```

Will yield:

```HTML
<label class="radio-inline">
  <input type="radio" value="true" name="templatelang_jade">
  Jade
</label>
```

<a name="address-field">
### Address field

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* name (String)
* value (Object) { street1, street2, suburb, state, postcode }

> ###### Note
> The location field also stores "name', "number', "country', and "geo" whilst this mixin ignores them.

```Jade
+address-field({ name: 'location', value: { street1: 'Shop 36, 468 Oxford St', suburb: 'Bondi', state: 'NSW', postcode: '2098' } })
```

Will yield:

```HTML
<div class="form-control-wrapper">
  <input name="location.street1" value="Shop 36, 468 Oxford St" placeholder="Street 1" class="form-control" type="text">
</div>
<div class="form-control-wrapper">
  <input name="location.street2" placeholder="Street 2" class="form-control" type="text">
</div>
<div class="form-control-wrapper">
  <input name="location.suburb" value="Bondi" placeholder="Suburb" class="form-control" type="text">
</div>
<div class="form-control-wrapper form-control-row">
  <div class="col-xs-6">
    <input name="location.state" value="NSW" placeholder="State" class="form-control" type="text">
  </div>
  <div class="col-xs-6">
    <input name="location.postcode" value="2098" placeholder="Postcode" class="form-control" type="text">
  </div>
</div>
```

<a name="upload">
### Upload

Browsers provide nice, native UI for file fields; let them handle it. Accepted arguments:
* name (String)

```Jade
+upload({ name: 'image' })
```

Will yield:

```HTML
<div class="field-upload">
  <input type="file" name="image">
</div>
```

<a name="icon-field">
### Icon Field

Display an icon left of the field to indicate context to the user eg; "ion-social-twitter" from the amazing [Ionicons icon set](http://ionicons.com)

This was built for icon fonts though should work fine with sprited images.

Accepted arguments:
* icon (String)
* field args (type, name, value, placeholder)

```Jade
+icon-field({ type: 'text', name: 'twitter', icon: 'ion-social-twitter' })
```

Will yield:

```HTML
<div class="icon-field">
  <span class="ion-social-twitter icon"></span>
  <input type="text" class="form-control" name="twitter">
</div>
```

<a name="character-field">
### Character Field

Display a character left of the field to indicate context to the user eg; "$" for a money field

Accepted arguments:
* character (String)
* field args (type, name, value, placeholder)

```Jade
+icon-field({ type: 'text', name: 'twitter', icon: 'ion-social-twitter' })
```

Will yield:

```HTML
<div class="icon-field">
  <span class="ion-social-twitter icon"></span>
  <input type="text" class="form-control" name="twitter">
</div>
```

<a name="button">
### Button

Buttons rather than `<input type="submit">` because they're more flexible. Accepted arguments:
* type (String) : defaults to "button"
* buttonlabel (String)

> ###### Note
> The button class defaults to "btn-default". See [attributes](#attributes)

```Jade
+button({ buttonlabel: 'Save changes', type: 'submit'})
```

Will yield:

```HTML
<button type="submit" class="btn btn-default">Save changes</button>
```




<a name="labelled">
## Labelled Fields

Labelled fields include their dependent mixins so you don't have to. For instance "+labelled-field()" includes "mixin field()" etc. These mixins expect a parent of '.form-horizontal' to display a label left of the field. Learn more about [Bootsrap forms](http://getbootstrap.com/css/#forms-horizontal)
<a name="labelled-field">
### Labelled Field

Accepted arguments:
* label (String)
* field args (type, name, value, placeholder)

```Jade
+labelled-field({ label: 'Admin Name', name: 'name', type: 'text', value: 'TJ Holowaychuk' })
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Admin Name</label>
  <div class="col-sm-9">
    <input type="text" class="form-control" value="TJ Holowaychuk" name="name">
  </div>
</div>
```

<a name="labelled-textarea">
### Labelled Textarea

Accepted arguments:
* label (String)
* field args (name, value, placeholder)

```Jade
+labelled-textarea({ label: 'Summary', name: 'summary', value: 'Programmer, author & artist. Creator of the Luna programming language, Express, Koa, Stylus, Component, Mocha, Jade, rework, node-canvas and others. Pastafarian', placeholder: 'Tell us about yourself' })
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Summary</label>
  <div class="col-sm-9">
    <textarea class="form-control" placeholder="Tell us about yourself" name="summary">Programmer, author &amp; artist. Creator of the Luna programming language, Express, Koa, Stylus, Component, Mocha, Jade, rework, node-canvas and others. Pastafarian</textarea>
  </div>
</div>
```

<a name="labelled-cloudinary-image">
### Labelled Cloudinary Image

Detect the existance of an image and display it, otherwise just show the upload field. Accepted arguments:
* label (String)
* name (String)
* value (Object) { secure_url, url, resource_type, format, height, width, signature, version, public_id }
* dimensions (Boolean) displays the image dimensions top left
* url (Boolean) provides a url for the full image
* upload args (name, note)

```Jade
+cloudinary_image({ label: 'Profile Image', name: 'profileAvatarImage', value: {...}, dimensions: true, url: true, note: 'Recommended: 200&times;300px' })
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Profile Image</label>
  <div class="col-sm-9">
    <div class="image-field">
      <div class="image-field__object">
        <a class="image-field__url" href="...">
          <img class="image-field__image" src="...">
        </a>
        <span class="image-field__dimensions">400 × 600</span>
      </div>
      <div class="image-field__body">
        <div class="field-upload">
          <input type="file" name="profileAvatarImage_upload">
          <div class="form-info">Recommended: 200×300px</div>
        </div>
        <label class="image-field__label">
          <input type="checkbox" class="image-field__checkbox" value="delete" name="profileAvatarImage_action">
            <span class="btn btn-narrow btn-default image-field__label-remove">Remove</span>
            <span class="btn btn-narrow btn-default image-field__label-undo">Undo</span>
            <span class="image-field__label-save">Removed. Save to delete.</span>
        </label>
      </div>
    </div>
  </div>
</div>
```

<a name="labelled-checkbox">
### Labelled Checkbox

Offset the checkbox so its inline with the rest of the fields, leaving the label column empty. Accepted arguments:
* checkboxlabel (String)
* name (String)
* value (String) : defaults to "true"
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ checkboxlabel: 'I accept the Terms and Conditions', name: 'acceptedTermsAndConditions', checked: true, disabled: true })
```

Will yield:

```HTML
<div class="form-group">
  <div class="col-sm-9 col-sm-offset-3">
    <div class="checkbox">
      <label>
        <input type="checkbox" disabled="" checked="" value="true" name="acceptedTermsAndConditions">
        I accept the Terms and Conditions
      </label>
    </div>
  </div>
</div>
```

<a name="labelled-address-field">
### Labelled Address field

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* label (String)
* name (String)
* value (Object) { street1, street2, suburb, state, postcode }

> ###### Note
> The location field also stores "name', "number', "country', and "geo".

```Jade
+address-field({ label: 'Address', name: 'location', value: { street1: 'Shop 36, 468 Oxford St', suburb: 'Bondi', state: 'NSW', postcode: '2098' } })
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Address</label>
  <div class="col-sm-9">
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Street 1" value="Shop 36, 468 Oxford St" name="address.street1">
    </div>
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Street 2" name="address.street2">
    </div>
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Suburb" value="Bondi" name="address.suburb">
    </div>
    <div class="form-control-wrapper form-control-row">
      <div class="col-xs-6">
        <input type="text" class="form-control" placeholder="State" value="NSW" name="address.state">
      </div>
      <div class="col-xs-6">
        <input type="text" class="form-control" placeholder="Postcode" value="2098" name="address.postcode">
      </div>
    </div>
  </div>
</div>
```

<a name="labelled-upload">
### Labelled Upload

Browsers provide nice, native UI for file fields; let them handle it. Accepted arguments:
* label (String)
* name (String)

```Jade
+labelled-upload({ label: 'Image', name: 'image' })
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Image</label>
  <div class="col-sm-9">
    <div class="field-upload">
      <input type="file" name="image">
    </div>
  </div>
</div>
```

<a name="labelled-button">
### Labelled Button

Offset the button so its inline with the rest of the fields. Leaving the label column empty. Accepted arguments:
* type (String) : defaults to "button"
* buttonlabel (String)

> ###### Note
> The button class defaults to "btn-default". See [attributes](#attributes)

```Jade
+labelled-button({ buttonlabel: 'Click me' })
```

Will yield:

```HTML
<div class="form-group">
  <div class="col-sm-9 col-sm-offset-3">
    <button class="btn btn-default" type="button">Click me</button>
  </div>
</div>
```




<a name="attributes">
## Attributes

All mixins accept appended attributes so you can add your own classes and IDs. For instance:

```Jade
+field({ name: 'username' })#js-username-hook
```

Will yield:

```HTML
<input name="username" type="text" class="form-control" id="js-username-hook">
```

##### They can also be chained:

```Jade
+labelled-field({ label: 'Username', name: 'username' })#special-field.big-field.light-text
```

Will yield:

```HTML
<div class="form-group">
  <label class="col-sm-3">Username</label>
  <div class="col-sm-9">
    <input type="text" name="username" class="form-control big-field light-text" id="special-field">
  </div>
</div>
```

> ###### Note
> Attributes are applied to the field itself and not a wrapper. You can wrap your mixin `#my-wrapper-id: +mixin(args)` if you need more control. Also classes append to the existing `.form-control` class rather than replace it.









