

# website-scraper-puppeteer
Plugin for [website-scraper](https://github.com/s-codes14/node-website-scrapper) which returns html for dynamic websites using [puppeteer](https://github.com/puppeteer/puppeteer).

This module is an Open Source Software maintained by one developer in free time. 

## Requirements
* nodejs version >= 8
* [website-scraper](https://github.com/s-codes14/node-website-scrapper)

## Installation
```sh
git clone https://github.com/s-codes14/node-website-scrapper.git

git clone https://github.com/S-codes14/puppeteer-scrape-plugin.git
```

## Usage
```javascript
const scrape = require('./website-scraper');
const PuppeteerPlugin = require('./puppeteer-scrape-plugin');

scrape({
    urls: ['https://www.instagram.com/gopro/'],
    directory: '/path/to/save',
    plugins: [ 
      new PuppeteerPlugin({
        launchOptions: { headless: false }, /* optional */
        scrollToBottom: { timeout: 10000, viewportN: 10 }, /* optional */
        blockNavigation: true, /* optional */
      })
    ]
});
```
Puppeteer plugin constructor accepts next params:
* `launchOptions` - *(optional)* - puppeteer launch options, can be found in [puppeteer docs](https://github.com/puppeteer/puppeteer/blob/v1.20.0/docs/api.md#puppeteerlaunchoptions)
* `scrollToBottom` - *(optional)* - in some cases, the page needs to be scrolled down to render its assets (lazyloading). Because some pages can be really endless, the scrolldown process can be interrupted before reaching the bottom when one or both of the bellow limitations are reached:
    * `timeout` - in milliseconds
    * `viewportN` - viewport height multiplier
* `blockNavigation` - *(optional)* - defines whether navigation away from the page is permitted or not. If it is set to true, then the page is locked to the current url and redirects with `location.replace(anotherPage)` will not pass. Defaults to `false`

## How it works
It starts Chromium in headless mode which just opens page and waits until page is loaded.
It is far from ideal because probably you need to wait until some resource is loaded or click some button or log in. Currently this module doesn't support such functionality.
