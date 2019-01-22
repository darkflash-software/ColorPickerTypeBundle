ColorPickerTypeBundle
==============================

The ``ColorPickerTypeBundle`` extends ``Symfony`` form types, 
creates a new  ``ColorPicker`` form type, to display a javascript color picker.

This Bundle use [jscolor](http://jscolor.com/).

## Installation

```sh
$ php composer.phar require xmon/color-picker-type-bundle
```

### Add Bundle to your application kernel
```php
// app/AppKernel.php
public function registerBundles()
{
    return array(
        // ...
        new Xmon\ColorPickerTypeBundle\XmonColorPickerTypeBundle(),
        // ...
    );
}
```
## Configuration

#### Option 1 - add asset manually to your template

```twig
{% extends '@Acme/layout.html.twig' %}

{% block javascripts %}
    {{ parent() }}
    <script type="text/javascript" src="{{ asset('bundles/xmoncolorpickertype/js/jscolor.min.js') }}"></script>
{% endblock %}
```

#### Option 1.1 - add asset manually to Sonata Admin template

Create new template extending default one:

```twig
{# src/Acme/AdminBundle/Resources/views/Sonata/standard_layout.html.twig #}
{% extends '@SonataAdmin/standard_layout.html.twig' %}

{% block javascripts %}
    {{ parent() }}
    <script type="text/javascript" src="{{ asset('bundles/xmoncolorpickertype/js/jscolor.min.js') }}"></script>
{% endblock %}
```

Set your custom template for Sonata Admin in config

```yml
#app/config/config.yml
sonata_admin:
    templates:
        layout: AcmeAdminBundle::Sonata/standard_layout.html.twig
```

### Include the template for the layout.

You can use default form field template shipped with the Bundle or modify it in your own bundle and use it instead.

```yml
# your config.yml
twig:
    form_themes:
        - '@XmonColorPickerType/Form/fields.html.twig'

```

## Usage

### Add validation to your model. 

```php
// src/AppBundle/Entity/MyEntity.php

use Symfony\Component\Validator\Constraints as Assert;
use Xmon\ColorPickerTypeBundle\Validator\Constraints as XmonAssertColor;

class MyEntity
{

    /**
     * @ORM\Column(type="string", length=6, nullable=true)
     * @XmonAssertColor\HexColor()
     */
    public $fieldName;

}
```

If you want change default message, try this:
```php
    /**
     * @XmonAssertColor\HexColor(
     *      message = "Custom message for value (%color%)."
     * )
     */
```

### How to use in your form. 

```php
use Xmon\ColorPickerTypeBundle\Form\Type\ColorPickerType;
...
$builder->add('fieldName', ColorPickerType::class)
...
```

This form type can be used without any problem with ``SonataAdminBundle``

### Credits

 - Thanks project used by this one:
	 - [jscolor](http://jscolor.com/)
 - Thanks project by inspiration:
	 - [OhColorPickerTypeBundle](https://github.com/ollieLtd/OhColorPickerTypeBundle)
