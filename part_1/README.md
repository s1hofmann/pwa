# xkcd PWA - Part 1

Basic starter code, no styling, webmanifest and simple layout tweaks.

## What's happening?

The first part configures the project's baseline.
A simple HTML page with currently no styling, Material Design Lite and some icons in various sizes.

But it already contains things specific to our progressive web app, which we'll take a closer look at.
The files we're going to examine a bit more are:

* `index.html`
* `manifest.webmanifest`

# `index.html`

Besides serving as our applications main view, our `index.html` also contains some adjustments regarding it's look and feel.

```HTML
<meta name="viewport" content="width=device-width, user-scalable=yes, initial-scale=1.0, maximum-scale=2.5, minimum-scale=0.5">
```

The `viewport` meta tag allows us to configure our application's size and scaling behavior.

`user-scalable=yes` tells the browser that users should be able to zoom in and out in our application.
Setting this value to `no` would disable pinch-to-zoom and users wouldn't be able to zoom in on e.g. pictures.

When enabled, the initial scale is configured via `initial-scale`.
In our little demo it's set to a value of `1.0`.
The `maximum-scale` and `minimum-scale` values let you define the maximum / minimum percentage users could zoom in or out of the page.

```HTML
<link rel="manifest" href="./manifest.webmanifest">
```

The above `<link ...>` tag with relationship `rel="manifest` includes our webmanifest.
Unfortunately, not all major browsers are fully supporting webmanifests yet.
[caniuse.com](https://caniuse.com/#feat=web-app-manifest) provides an overview which browsers already do.

As you can see, only the latest releases of Safari support manifest files.
In order to achieve similar functionality, `index.html` contains quite a bit of additional tags.

```HTML
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="white">
<meta name="apple-mobile-web-app-title" content="xkcdpwa">
<meta name="theme-color" content="grey">
<meta name="Description" content="Let's build a PWA to stay entertained!">
<link rel="apple-touch-icon" sizes="57x57" href="./src/img/icons/apple-icon-57x57.png">
<link rel="apple-touch-icon" sizes="60x60" href="./src/img/icons/apple-icon-60x60.png">
<link rel="apple-touch-icon" sizes="72x72" href="./src/img/icons/apple-icon-72x72.png">
<link rel="apple-touch-icon" sizes="76x76" href="./src/img/icons/apple-icon-76x76.png">
<link rel="apple-touch-icon" sizes="114x114" href="./src/img/icons/apple-icon-114x114.png">
<link rel="apple-touch-icon" sizes="120x120" href="./src/img/icons/apple-icon-120x120.png">
<link rel="apple-touch-icon" sizes="144x144" href="./src/img/icons/apple-icon-144x144.png">
<link rel="apple-touch-icon" sizes="152x152" href="./src/img/icons/apple-icon-152x152.png">
<link rel="apple-touch-icon" sizes="180x180" href="./src/img/icons/apple-icon-180x180.png">
```

These `<meta ...>` and `<link ...>` tags contain data regarding the app title, theming, icons and a description.
These details would also be contained in a manifest file.

# `manifest.webmanifest`

```
{
  "name": "xkcdpwa",
  "short_name": "xkcdpwa",
  "start_url": "./index.html",
  "scope": ".",
  "display": "standalone",
  "background_color": "#aaa",
  "theme_color": "#aaa",
  "description": "Let's build a PWA to stay entertained!",
  "dir": "ltr",
  "lang": "en-US",
  "orientation": "any",
  "icons": [{
      "src": "./src/img/icons/app-icon-48x48.png",
      "type": "image/png",
      "sizes": "48x48"
    },
    {
      "src": "./src/img/icons/app-icon-96x96.png",
      .
      .
      .
  ]
}
```

The above snippet shows the content of our app's webmanifest.
Many of the fields should be self-explanatory, but let's take a closer look nonetheless.

`"name"` specifies the full application name. This name will be displayed on the splash screen.

`"short_name"` provides a short name for our application. This value will be used for our homescreen icon.

The `"start_url"` lets us configure which relative path will be called on application start.
This way we could configure a different landing page when accessing our page via installed web app.
Another use-case could be to append a query string to the URL in order to measure the usage of our installable web app.

`"scope"` defines for which resources our application should be displayed as

`"display"` plays a major role when it comes to app integration.
When set to `"standalone"`, our PWA will be displayed like a native application.
No URL bar, no navigation buttons, just the default platform UI with status bar etc.
`"fullscreen"` would display our application in actual fullscreen mode, also hiding status bars and other native UI elements.

Installed web apps will display a splash screen on start-up.
This screen is assembled using manifest data and displays the application's icon and its `name` on a configurable background. Via the `"background_color"` field we're able to paint the background in a color which suits our overall app theme.

When using the task switcher on mobile devices every application's top bar has a certain color. This property is also configurable for PWAs an is set via `"theme_color"` field in the manifest.

The `"description"` value will be shown on the startup splash-screen.

`"dir"` specifies the primary reading direction for `name`, `short_name` and `description`.
Our application is configured to a reading direction from **l**eft **t**o **r**ight.

`"lang"` contains the primary language for `name` and `short_name`.

The `"orientation"` field configures screen rotation.
When set to `"any"`, our application will rotate as we rotate the device.

`"portrait"` would keep it fixed to portrait mode, `"landscape"` would neglect device rotation and keep the application in landscape mode.

# Further reading

* [Webmanifest spec](https://w3c.github.io/manifest/)
* [Mozilla developer page on manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest)
* [Google explaination on manifest](https://developers.google.com/web/fundamentals/web-app-manifest/)
