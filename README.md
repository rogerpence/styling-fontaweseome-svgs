Styling Font Awesome SVGs
=============

>See this code at [CodePen](https://codepen.io/rogerpence/pen/KKzZQKq).

When you use Font Awesome SVGs:

-   No Font Awesome fonts or CSS necessary.
-   No other requests fetching fonts or CSS (but page size grows).
-   SVG's aren't cached--as HTML content they are included in the page
    response every time.
-   You need to style the icons with your own CSS (see coloring and
    sizing below).

> I'm a big fan of Andy Bell's [CUBE
> CSS](https://piccalil.li/blog/cube-css/) methodology (which is also
> embraced by [Every Layout](https://every-layout.dev/)). Andy's
> concepts styling at the highest level possible makes a lot of sense.
> I'm still experiment with his concepts, but tried to appy some of them
> here to style Font Awesome SVGs. The idea of having CSS primitives
> that apply ripple-down styling eliminates the need to style SVGs at
> the SVG tag level. That said, you could easily apply more specfic,
> granular CSS to do localized styling.

### Coloring SVGs

Font Awesome SVGs set the `path` tag's `fill` attribute to
`currentColor` (as shown below).
[`currentColor`](https://www.quackit.com/css/color/values/css_currentcolor_keyword.cfm)
refers to the current color in the cascade (think of it as imposing
`inherit` where `inherit` doesn't usually apply.). Therefore, you can
set the Font Awesome icon color by setting a color to an owning element.

    <svg aria-hidden="true" focusable="false"
            data-prefix="fas" data-icon="home"
            class="svg-inline--fa fa-home fa-w-18"
            role="img" xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 576 512">
        <path fill="currentColor" d="..."></path>
    </svg>

For example, this markup puts Font Awesome's SVG inside a `button`:

    <button class="icon-button" title="bed">
        <svg ....>
            <path fill="currentColor" d="...""/>
        </svg>
    </button>

and uses CSS custom properties to set the colors on the
`button.icon-button` element:

    .icon-button {
        color: var(--color, #303030);
        ...
    }

    .icon-button {
        --color: navy;
    }

You could also set the color on the SVG element.

### Sizing SVGs

SVGs are infinitely scalable and heights and widths constrain to the
size of their container. If you drop an SVG in an empty HTML file and it
will scale to fill the entire page. To avoid needing to manage icon size
individually, consider adopting a couple of icon patterns.

For buttons, consider settting the button size and and then scaling the
icon to button.

    .icon-button {
        ...
        width: 6rem;
        height: 3rem;
        ...
    }

    .icon-button-container svg[data-icon] {
        width: 33%;
    }

If you aren't putting SVGs in buttons, you could place them within `div`
tags like this:

    <div class="icon-large-container">
        &ltsvg...
          full Font Awesome SVG here
        </svg>
    </div>

and then use general-purpose CSS like this to size the SVGs:

    div.icon-small-container {
        width: 2rem;
    }

    div.icon-medium-container {
        width: 3rem;
    }

    div.icon-large-container {
        width: 5rem;
    }

    You could as many sizing options as needed.

