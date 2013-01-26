## jQuery RS Carousel Quick Start

### Include the following JavaScript and CSS:
    
    <!-- carousel CSS -->
    <link rel="stylesheet" type="text/css" href="css/jquery.rs.carousel.css" media="all" />

    <!-- lib -->
    <script type="text/javascript" src="js/lib/jquery.js"></script>
    <script type="text/javascript" src="js/lib/jquery.ui.widget.js"></script>
    
    <!-- carousel core -->
    <script type="text/javascript" src="js/jquery.rs.carousel.js"></script>

    <!-- carousel extensions (optional) -->
    <script type="text/javascript" src="js/jquery.rs.carousel-autoscroll.js"></script>
    <script type="text/javascript" src="js/jquery.rs.carousel-continuous.js"></script>

### This is the basic HTML structure required:

    <div class="rs-carousel">
        <ul>
            <li>
                <!-- item 1 content -->
            </li>
            <li>
                <!-- item 2 content -->
            </li>
            <li>
                <!-- item 3 content -->
            </li>
            <li>
                <!-- item 4 content -->
            </li>
            <li>
                <!-- item 5 content etc. -->
            </li>
        </ul>
    </div>
	
### Here's the JavaScript:

    $(document).ready(function () {
        $('.rs-carousel').carousel();
    });

### And here's the generated markup:

    <div class="rs-carousel rs-carousel-horizontal">
        <div class="rs-carousel-mask">
            <ul class="rs-carousel-runner">
                <li class="rs-carousel-item">
                    <!-- item 1 content -->
                </li>
                <li class="rs-carousel-item">
                    <!-- item 2 content -->
                </li>
                <li class="rs-carousel-item">
                    <!-- item 3 content -->
                </li>
                <li class="rs-carousel-item">
                    <!-- item 4 content -->
                </li>
                <li class="rs-carousel-item">
                    <!-- item 5 content etc. -->
                </li>
            </ul>
        </div>
        <ol class="rs-carousel-pagination">
            <li class="rs-carousel-pagination-link rs-carousel-pagination-link-active"><a href="#page-1">1</a></li>
            <li class="rs-carousel-pagination-link"><a href="#page-2">2</a></li>
        </ol>
        <a class="rs-carousel-action rs-carousel-action-prev" href="#">Previous</a>
        <a class="rs-carousel-action rs-carousel-action-next rs-carousel-action-disabled" href="#">Next</a>
    </div>

## Documentation

### Options
#### `mask: '> div'` (string)
A jQuery selector to match the `.rs-carousel-mask` element. The DOM is queried from the widgets root element. If the mask isn't found it will get dynamically added by the plugin.

#### `runner: '> ul'` (string)
A jQuery selector to match the `.rs-carousel-runner` element. If the mask was found the DOM is queried from the mask otherwise it will be queried from the widgets root element.

#### `items: '> li'` (string)
A jQuery selector to match the `.rs-carousel-item` element(s). The DOM is queried from the widgets runner.

#### `itemsPerTransition: 'auto'` (string, number)
Sets the number of items to scroll per transition, if set to 'auto' the number of items scrolled will be based on how many items are visible.

#### `orientation: 'horizontal'` (string)
Sets the orientation of the carousel, either 'horizontal' or 'vertical'.

#### `loop: false` (boolean)
If set to true carousel will loop back to first or last page accordingly.

#### `whitespace: false` (boolean)
If set to true the carousel will allow whitespace to be seen when there aren't enough items to fill the last page.

#### `nextPrevActions: true` (boolean)
Sets whether the next and prev actions are included, next and prev actions are inserted as anchor tags.

#### `insertPrevAction: function () { return $('<a href="#" class="rs-carousel-action rs-carousel-action-prev">Prev</a>').appendTo(this); }` (function)
Allows you to define the prev actions mark-up as well as its location in the DOM.

The context of the function will be the carousels root element and the function should return a jQuery object, e.g.

    function () {
        // this === <div class="rs-carousel"></div>
        return $('<a href="#">Prev</a>').appendTo(this);
    }

#### `insertNextAction: function () { return $('<a href="#" class="rs-carousel-action rs-carousel-action-next">Next</a>').appendTo(this); }` (function)
Allows you to define the prev actions mark-up as well as its location in the DOM.

The context of the function will be the carousels root element and the function should return a jQuery object, e.g.

    function () {
        // this === <div class="rs-carousel"></div>
        return $('<a href="#">Next</a>').appendTo(this);
    }

#### `pagination: true` (boolean)
Sets whether pagination links should be included, pagination links are constructed as an ordered list.

#### `insertPagination: function (pagination) { return $(pagination).insertAfter($(this).find('.rs-carousel-mask')); }` (function)
Allows you to override where in the DOM the pagination links are inserted as well as decorate them with any required HTML.

The context of the function will be the carousels root element and the function should return a jQuery object containing the `pagination`, e.g.

    function (pagination) {
        // this === <div class="rs-carousel"></div>
        // pagination === <ol class="rs-carousel-pagination"> ... </ol>
        return $(pagination).insertAfter($(this).find('.rs-carousel-mask'));
    }

#### `speed: 'normal'` (string)
Sets the speed of the carousel.

#### `easing: 'swing'` (string)
Sets the easing equation used.

#### `disabled: false` (boolean)
If set to true carousel will no longer change state.

#### `autoScroll: false` (boolean)
Set to true to invoke auto scrolling, note when the mouse enters the carousel the interval will stop, it'll consequently begin when the mouse leaves.

NOTE: Requires the autoScroll extension (jquery.rs.carousel-autoscroll.js).

#### `pause: 8000` (number)
Sets the amount of time in miliseconds the carousel waits before it automatically scrolls.

NOTE: Requires the autoScroll extension (jquery.rs.carousel-autoscroll.js).

#### `continuous: false` (boolean)
If set to true the carousel will continuously loop through its pages rather than scrolling all the way back to the first page.

NOTE: Requires the continuous extension (jquery.rs.carousel-continuous.js).

### Events
#### `create: null` (function)
Fired on first call.

It can be passed in the options object like this:

    $(':rs-carousel').carousel({
       create: function (event, data) { ... }
    });
	
and bound as an event like this:
	
    $(':rs-carousel').on('carouselcreate', function (event, data) {
        ...
    });

#### `before: null` (function)
Fired before transition. Calling `preventDefault` on the event object will prevent the carousel from scrolling.

It can be passed in the options object like this:

    $(':rs-carousel').carousel({
        before: function (event, data) { ... }
    });
	
and bound as an event like this:
	
    $(':rs-carousel').on('carouselbefore', function (event, data) {
        ...
    });

#### `after: null` (function)
Fired after transition.

It can be passed in the options object like this:

    $(':rs-carousel').carousel({
        after: function(event, data) { ... }
    });
	
and bound as an event like this:
	
    $(':rs-carousel').on('carouselafter', function(event, data) {
        ...
    });

All callbacks provide two arguments, the first of which is the `event` object which contains an `animate` property to determine whether the transition was animated or not (this can be useful if you're syncing up other animations with the slide). Also the `event.originalEvent` can be inspected to determine which method was used to invoke the transition, be it `next`, `prev` or `goToPage`.

The second argument is `data` which provides access to the carousels core elements as well as the current and previous pages:
    
    {
        page: (jQuery object),
        prevPage: (jQuery object),
        elements: {
            mask: (jQuery object)
            runner: (jQuery object)
            items: (jQuery object)
            pagination: (jQuery object)
            nextAction: (jQuery object)
            prevAction: (jQuery object)
        }
    }

### Methods
#### next `$(':rs-carousel').carousel('next')`
Moves to the next page.

#### prev `$(':rs-carousel').carousel('prev')`
Moves to the prev page.

#### goToPage `$(':rs-carousel').carousel('goToPage', page [, animate])`
Moves to the specified zero based `page`. If `animate` is set to false it'll jump straight there.

#### goToItem `$(':rs-carousel').carousel('goToItem', item [, animate])`
Moves to page containing `item`, `item` can be a zero based number, a vanilla DOM element
or a jQuery object. If `animate` is set to false it'll jump straight there.

#### refresh `$(':rs-carousel').carousel('refresh')`
Refreshes carousel based on new state. The carousel can be made responsive by calling this method on the windows resize event.

#### getPage `$(':rs-carousel').carousel('getPage' [, index])`
Returns a jQuery object containing the items on the page found at `index`. If `index` is omitted it'll return the current page.

#### getPages `$(':rs-carousel').carousel('getPages')`
Returns the array of pages e.g. [jQuery(li, li, li), jQuery(li, li, li, li), jQuery(li, li, li), jQuery(li, li)]

#### getIndex `$(':rs-carousel').carousel('getIndex')`
Returns the index of the current page.

#### getPrevIndex `$(':rs-carousel').carousel('getPrevIndex')`
Returns the index of the previous page.

#### getNoOfPages `$(':rs-carousel').carousel('getNoOfPages')`
Returns the number of pages.

#### getNoOfItems `$(':rs-carousel').carousel('getNoOfItems')`
Returns number of items in carousel.

#### add `$(':rs-carousel').carousel('add', items)`
Appends items to carousel, `items` can be DOM element, HTML string, or jQuery object.

#### remove `$(':rs-carousel').carousel('remove', selector)`
Removes the items matched by `selector` from the carousel.

#### option `$(':rs-carousel').carousel('option', optionName [, value])`
Get or set any carousel option. If no `value` is specified, will act as a getter.

#### option `$(':rs-carousel').carousel('option' [, options])`
Get or set multiple carousel options at once by providing an `options` object. If `options` is omitted it will return all options.

#### disable `$(':rs-carousel').carousel('disable')`
Disables the carousel and adds the `'rs-carousel-disabled'` className to the root element.

#### enable `$(':rs-carousel').carousel('enable')`
Enables the carousel and removes the `'rs-carousel-disabled'` className from the root element.

#### widget `$(':rs-carousel').carousel('widget')`
Returns the root element.

#### destroy `$(':rs-carousel').carousel('destroy')`
Removes the carousel functionality completely. This will return the element back to its pre-init state.