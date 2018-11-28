- **[Basic Usage](INDEX.md)**
- [Structs](STRUCTS.md)
- [Hooks](HOOKS.md)
- [Example App](EXAMPLE-APP.md)

# Basic Usage

For a full reference of what **could** go to your `<head>` see [joshbuchea's HEAD](https://github.com/joshbuchea/HEAD)

### Recommended Minimum

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Page Title</title>
```

```php
use romanzipp\Seo\Structs\Meta\Charset;
use romanzipp\Seo\Structs\Meta\Viewport;
use romanzipp\Seo\Structs\Title;

seo()->add(Charset::make()->charset('utf-8'));
seo()->add(Viewport::make()->content('width=device-width, initial-scale=1, viewport-fit=cover'));
seo()->add(Title::make()->body('Page Title'));
```

### Meta

```html
<meta name="application-name" content="Application Name">
<meta name="theme-color" content="#f00">
<meta name="description" content="A description of the page">
```

```php
use romanzipp\Seo\Structs\Meta;

seo()->add(Meta::make()->attr('name', 'application-name')->attr('Application Name'));
seo()->add(Meta::make()->attr('name', 'theme-color')->attr('#f00'));
seo()->add(Meta::make()->attr('name', 'description')->attr('A description of the page'));
```

## SeoService Macros

The `romanzipp\Seo\Services\SeoService` class uses the Laravel `Macroable` trait which allows creating short macros.

### Example

Let's say you want to display a page title in the document body but added a hook to append the site name.

In this case, we'll create a macro to retreive the original Title Struct body value.

```php
use romanzipp\Seo\Facades\Seo;
use romanzipp\Seo\Structs\Title;

Seo::macro('getTitle', function () {

    if ( ! $title = $this->getStruct(Title::class)) {
        return null;
    }

    if ( ! $body = $title->getBody()) {
        return null;
    }

    return $body->getOriginalData();
});
```