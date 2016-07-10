# [Hack Design](https://hackdesign.org) Notes

### Lesson 2: Dive Into Typography

* [Better Web Typography](http://www.creativebloq.com/typography/better-web-typography-few-simple-steps-5132803)
    * avoid using the `<b>` and `<i>` tags, instead use `<strong>` and `<em>`. The latter leaves you with the freedom to change the appearance via CSS
    * Use [HTML entities](https://www.w3.org/TR/html4/sgml/entities.html#h-24.1) for symbols like the trademark, multiplication sign, and apostrophes
    * Quote correctly - use a right single quotation mark for an apostrophe

### Lesson 4: Know Your Tools

* [Towards a Retina Web](https://www.smashingmagazine.com/2012/08/towards-retina-web/)
    * CSS pixels are referred to as Device independent pixels (DIPs)
    * `<div height="200" width="300"></div>`
        * draws 400x600 device pixels to keep the same physical size
    * *Bitmap Pixels*: Smallest unit of data in a raster image (PNG, JPG, GIF, etc)
        * When raster image is displayed at full size on a standard-density display, 1 bitmap pixel corresponds to 1 device pixel  ![](https://media-mediatemple.netdna-ssl.com/wp-content/uploads/2012/07/css-device-bitmap-pixels.png)

### Lesson 5: Typography in Product Design

* [Practice Guide to Typography on the Web](http://webdesign.tutsplus.com/articles/choosing-the-right-font-a-practical-guide-to-typography-on-the-web--webdesign-15)  
    * Readability
        * Choose body of at least size 12px
        * Title should only be as big as it needs to be
        * Measure is the length of a line of text
        * Leading (rhymes with wedding) is the space between lines of text. For large blocks of text, 1.5 times the size of the text is good
            * Measured from the baseline of each line of text
                * Descenders, parts of the letters that are longer (e.g. lowercase g), fall below the baseline
                * Ascenders are the opposite (e.g. h)
        * Kerning is to adjust the spacing between a pair of letters, numerals, punctuation.
        * Tracking (letter spacing) adjusts the spacing between all the glyphs in one text

* [More Meaningful Typography](http://alistapart.com/article/more-meaningful-typography)
    * Modular scale: Sequence of numbers that relate to each other in a meaningful way (e.g. golden ratio - 1:1.618)

* [http://www.gridlover.net/](http://www.gridlover.net/)

* [Technical Web Typography](https://www.smashingmagazine.com/2011/03/technical-web-typography-guidelines-and-techniques/)

### Lesson 7: Responsive Typography in Action

* Example of great resp. typo: [The Great Discontent](http://thegreatdiscontent.com/interview/steven-harrington)
* Tool for experimenting with Typography/Typefaces: [Typecast](https://hackdesign.org/tasks/53)

### Lessson 8: Typography in Practice

* [The Elements of Typographic Style Applied to the Web](http://webtypography.net/)
    * "[t]he em is a sliding measure. One em is a distance equal to the type size. In 6 point type, an em is 6 points; in 12 point type an em is 12 points and in 60 point type an em is 60 points. Thus a one em space is proportionately the same in any size."
    * Generally best to use percentages when setting box width
    * Use a single space between sentences

* [Five Simple Steps to Designing Grid Systems](http://www.markboulton.co.uk/journal/five-simple-steps-to-designing-grid-systems-preface)
    * Part 1:
        * In this example, divide paper using 1:1.414 (A4 ratio)
        ![](http://www.markboulton.co.uk/images/portfolio/grid_pt1_1.gif)
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt1_2.gif)
    * Part 2: Ratios and Complex Grid Systems
        * With the given double page spread, a asymetrical grid is required
        * Shaping the page
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt2_1.gif)
        * Applying the Golden Section to get two columns, A and B
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt2_2.gif)
        * Extend lines of content area
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt2_3.gif)
        * Add in 'hanging lines' to give the reader a consistent place to rest their eyes
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt2_4.gif)
        * Add content
        ![](http://www.markboulton.co.uk/images/uploads/grid_pt2_5.gif)
    * Part 3: Grid systems for the Web
        * 9, 12 grid systems are good - let's use them correctly, though
    * Part 4: Fixed
        * Export grid as .gif and set as background-image element on the body tag

### Lesson 12: Understanding the User in UX

* [When should your startup focus on UX](http://uxceo.com/post/46777371976/when-should-your-startup-focus-on-ux)
    * ![](http://66.media.tumblr.com/b7f7468a090189e5be16b13541996a4a/tumblr_inline_mkjgg7m86R1qz4rgp.png)

* [Quick Course On Effective Website Copywriting](https://www.smashingmagazine.com/2012/05/quick-course-on-effective-website-copywriting/)


* [Using webfonts in 2015](https://helloanselm.com/2015/using-webfonts-in-2015/)
    1. Load webfonts asynchonously with *font face observer*
    2. Avoid big reflows in layout with a proper fallback font
    3. Load webfonts as fast as possible by using a `preload` attribute to the font headers
    4. Avoid loading web fonts again with cookies

* [Typography in Ten Minutes](http://practicaltypography.com/typography-in-ten-minutes.html)
    * Line spacing should be 120-145% of the point size
    * Line length should be an average of 45-90 characters per line
    * [Summary of key rules](http://practicaltypography.com/summary-of-key-rules.html)

### Lesson 17: Building Color Confidence

* [Color Theory For Designers, Part 2: Understanding Concepts And Terminology](https://www.smashingmagazine.com/2010/02/color-theory-for-designers-part-2-understanding-concepts-and-terminology/)

* [Color Theory For Designers, Part 3: Creating Your Own Color Palettes](https://www.smashingmagazine.com/2010/02/color-theory-for-designer-part-3-creating-your-own-color-palettes/)
    * Scheme Types:
        * Monochromatic: Monochromatic color schemes are made up of different tones, shades and tints within a specific hue
        * Analogous: Analogous schemes are created by using three colors that are next to each other on the 12-spoke color wheel
            * May require toning down chroma to make usable as a color scheme
        * Complementary: Complementary schemes are created by combining colors from opposite sides of the color wheel
        * Split Complementary: In this scheme, instead of using colors that are opposites, you use colors on either side of the hue opposite your base hue
        * Triadic: Triadic schemes are made up of hues equally spaced around the 12-spoke color wheel
        * DOUBLE-COMPLEMENTARY (TETRADIC)



### Misc

* [8 pt grid](http://spec.fm/specifics/8-pt-grid)
    * Baseline text to develop vertical consistency - best to combine 8pt UI grid with 4pt baseline grid
    * *Basic Principle*: Use multiples of 8 to define dimensions, padding, and margin of both block and inline element
    * *Tips*:
        * Use snap to grid
        * With REMs, if you set your root text size to 16, you can use .5rem increments to build layouts on an 8pt grid
        * Change big nudge value with *Nudg.it* in Sketch
        * Learn nudge, resize, adjust increment shortcuts
        * Put a frame around icons

* [8pt workflow with soft grids](https://medium.com/sketch-app-sources/8-point-soft-grids-in-sketch-e8f1d5ca2cd4#.vhlh3ey3l)

* [Desiging at 1x](https://medium.com/sketch-app-sources/designing-at-1x-33240842180c#.q56eh965v)
