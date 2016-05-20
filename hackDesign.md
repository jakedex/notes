# [Hack Design](https://hackdesign.org) Notes

### Lesson 2: Dive Into Typography
* [better web typography](http://www.creativebloq.com/typography/better-web-typography-few-simple-steps-5132803)
    * avoid using the `<b>` and `<i>` tags, instead use `<strong>` and `<em>`. The latter leaves you with the freedom to change the appearance via CSS
    * Use [HTML entities](https://www.w3.org/TR/html4/sgml/entities.html#h-24.1) for symbols like the trademark, multiplication sign, and apostrophes
    * Quote correctly - use a right single quotation mark for an apostrophe

### Lesson 4: Know Your Tools
* [towards a retina web](https://www.smashingmagazine.com/2012/08/towards-retina-web/)
    * CSS pixels are referred to as Device independent pixels (DIPs)
    * `<div height="200" width="300"></div>`
        * draws 400x600 device pixels to keep the same physical size
    * *Bitmap Pixels*: Smallest unit of data in a raster image (PNG, JPG, GIF, etc)
        * When raster image is displayed at full size on a standard-density display, 1 bitmap pixel corresponds to 1 device pixel  !(https://media-mediatemple.netdna-ssl.com/wp-content/uploads/2012/07/css-device-bitmap-pixels.png)
    * Retina solutions:
        * HTML/CSS sizing
        * 
