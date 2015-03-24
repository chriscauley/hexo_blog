title: "Pure CSS Golden Rectangle"
date: 2014-04-12 16:14:01
tags:
- CSS
- fractals
post_asset_folder: true
---

<div class="first-image">
<img src="/img/golden_rectangle.png" />
{% asset_img golden_rectangle.png %}
</div>

The [golden ratio](http://en.wikipedia.org/wiki/Golden_rectangle "Wikipedia: Golden Rectangle") has long fascinated mankind because blah blah blah... And the [golden rectangle](http://en.wikipedia.org/wiki/Golden_rectangle "Wikipedia: Golden Rectangle") has aesthetic properties because of yadda yadda yadda... If you don't already know about this magical number, I'm not the person to educate you. Trust me, it's cool. About a year ago I decided to create the golden rectangle in pure CSS as a way to learn about inheritance and to prepare myself to create more complex fractals in CSS/HTML.

The golden rectangle has sides with a ratio of 1.618... which is special because, if you divide the rectangle into a square and another rectangle, the sides of the inner rectangle has the same ratio as the outer rectangle. It is made by repeating the same rectangle scaled down, rotated, and embedded into itself over and over. So we start with embedded divs, the first of which has a set size and the remaining are 62% (1/1.618x100%) the size to its parent div.

<p data-height="350" data-theme-id="0" data-slug-hash="RNvZbm" data-default-tab="result" data-user="chriscauley" class='codepen'>See the Pen <a href='http://codepen.io/chriscauley/pen/RNvZbm/'>Pure CSS Golden Rectangle Step 1</a> by Chris Cauley (<a href='http://codepen.io/chriscauley'>@chriscauley</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Then the child divs are placed at the top right corner, outside of the parent div using absolute positioning. The children are then rotated a quarter turn to create the golden rectangle. If you hover over any of the rectangles in the following figure, the :hover pseudo class will rotate the child and all of it's ancestor divs. This forms the golden rectangle.

<p data-height="350" data-theme-id="0" data-slug-hash="gbqxbY" data-default-tab="result" data-user="chriscauley" class='codepen'>See the Pen <a href='http://codepen.io/chriscauley/pen/gbqxbY/'>Pure CSS Golden Rectangle Step 2</a> by Chris Cauley (<a href='http://codepen.io/chriscauley'>@chriscauley</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Next, :before (circle) and :after (background) elements are added to create colors. This creates the golden spiral. In the final product, all squares inside the golden rectangle are set to the same colors (red, blue, and yellow), which is then hue rotated to product a unique set of colors at each level. The hue rotation adds up as you go down the DOM tree, creating a wide array of colors with only 3 color declarations.

In this example, if you hover over a div it will remove hue-rotate for all child divs.

<p data-height="350" data-theme-id="0" data-slug-hash="xbMLZJ" data-default-tab="result" data-user="chriscauley" class='codepen'>See the Pen <a href='http://codepen.io/chriscauley/pen/xbMLZJ/'>Pure CSS Golden Rectangle Final</a> by Chris Cauley (<a href='http://codepen.io/chriscauley'>@chriscauley</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
