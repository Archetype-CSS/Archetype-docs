# Architecture

>"By categorizing CSS rules we begin to see patterns and can define best practices around each of these patterns" -  [Jonathan Snook](http://smacss.com/book/categorizing)

## Directory Structure

Most of Archetype's modules (utilities, objects, and components) are managed with [Bower](http://bower.io) within the `bower_components/` directory. It is a best practice to [version control Front-End packages](http://addyosmani.com/blog/checking-in-front-end-dependencies/). These modules are `@import`-ed into a project, customized to your needs, and controlled by [Archetype](https://github.com/Archetype-CSS/Archetype).

| Directory/File       | Description    |
| ------------- | --------------------- |
| `main.scss`      | Partials should be used for all base, component, and layout styles. These partials are then `@import`-ed into `main.scss` which provides the opportunity to easily enable/disable design system modules as needed. When including partials within your `main.scss` stylesheet, leave off the file extension to allow for easier conversion between Sass and SCSS syntaxes if you ever need to do so [[17]](addendum.md). Example [Archetype's main.scss](https://github.com/Archetype-CSS/Archetype/blob/master/sass/main.scss) |
| `base/`      | The base directory contains styles and settings that apply to the entire project. These include the `_color-pallet.scss` and `_typography-pallet.scss` partials as well as settings for [compass](http://compass-style.org/) and compass plugins. The `base/` directory is where all site-wide settings are controlled. |
| `components/` | Components are modular and reusable entities of a design system. Everything within the design system is a component. Each component is maintained within its own repository, managed with [Bower](http://bower.io), and `@import`-ed into `main.scss`. All objects are prefixed with `o-`. They are installed using `bower install Archetype-o-[object-name]`. Archetype components have basic, default structure and skin styles applied for rapid prototyping. These default styles can be easily over-ridden. Archetype components are the equivalent to Modules within the [SMACSS](http://smacss.com/) methodology. Sub objects are defined in the same partial as the object they extend/modify. |
| `bower_components` | This is where all Archetype modules are downloaded by [Bower](http://bower.io) |
| `layout/` | Layout styles provide structure to mobile-first, linear content. These styles are used to progressively enhance the basic layout when device capability and/or viewport allow. Because layout is treated as an enhancement, these styles are kept separate from the components they enhance and are applied with their own class. Each component's layout is defined in its own partial inside the layout directory. Layout stylesheets are named by prefixing the component's name with `l-` in order to explicitly define the relationship between layout and component. |
| `temp/` | The temporary directory contains any styles that haven't yet been properly defined and organized within the project's architecture. This where any hacks or quick fixes belong. Each 'fix' placed within this directory should be given its own partial and should be accompanied by a corresponding issue properly tagged and filed in the project's repository so that it can be incorporated into the code base at a later date. Preventing sub-standard code from being committed into the code base helps to prevent unnecessary depreciation as well as unintentionally introducing bugs by keeping these 'fixes' quarantined within the temp directory. [[25]](addendum.md). |

## Object Oriented CSS (OOCSS)

>"[A] CSS “object” is a repeating visual pattern which can be abstracted into an independent snippet of HTML CSS and possibly JavaScript. Once created an object can then be reused throughout a site." - [Nichole Sullivan](https://twitter.com/stubbornella)

### Two Main Principles of OOCSS

  1. **Separation of Structure from Skin** - distinguish between structure styles (box-model) and skin styles (color, font, gradients) and abstract these styles in class-based modules to allow re-use [[6]](addendum.md).
  2. **Separation of Container and Content** - avoid all explicit parent-child relationship within style declarations so that a component's style is not dependant upon its container which allows the module to be reused [[6]](addendum.md).

### Utilities
Archetype utilities are low-level abstractions used globally throughout a design system via a class, function, or mixin to provide specific functionality. Utilities are maintained within their own repository, managed with [Bower](http://bower.io), and are `@import`-ed within `main.scss`. All utilities are prefixed with `Archetype-u-`. They are installed using `bower install Archetype-u-[utility-Name]`. Some utility abstractions, like [Archetype-u-display](https://github.com/Archetype-CSS/u-display) and [u-size](https://github.com/Archetype-CSS/u-size) can be applied to HTML elements directly.  In this case, they should be prefixed using the `Archetype-u-utilityName` (in camelCase). Other utilities, (like functions and mixins) are applied within the stylesheets, rather than the markup.

### Objects
Object styles are generic abstractions that can be extended to build a component. They are styles which remain consistent and unchanged within a component regardless of skin or structure and are abstracted to be used as a foundation for building UI components. The classic OOCSS example is the media-object [[16]](addendum). Each object is maintained within its own repository, managed with [Bower](http://bower.io), and `@import`-ed into `main.scss`. All objects are prefixed with `Archetype-o-`. They are installed using `bower install Archetype-o-[object-name]`.

### Sub Objects
An Archetype sub object is a context-dependant sibling of an object that performs a certain function and is represented by an additional HTML class attribute on the element. Sub Objects are denoted by the use of `__` (double underscores) for example, `.objectName__subObjectName` in order to maintain the sub object's context, maintain control of the cascade, and avoid location-dependant selectors [[2]](addendum.md). Sub objects extend or provide minor overrides to the object and is often applied to the same HTML element or a direct decendent. 

### Components
A discrete and independent entity designed to exist as a stand alone module without any dependencies to its container. A component can be simple or compound (contain one or more components) and it should be able to be relocated on the page without breaking [[1]](addendum). Example components include buttons, navigation bars, etc. An example of a compound component would be a search block composed of an input and a submit button [[2]](addendum.md).

In order to maintain modularity a component must adhere to the following:

  * Component styles must not declare any explicit size constraints, allowing the module to scale to it's parent container. A component can be placed inside a layout component, i.e. a grid; or extended with a layout class, but it must never be given an explicit width.
  * A component must remain independent from siblings, children, and parents allowing for arbitrarily placement within a design system. This means that CSS ID Selectors must be avoided to allow components to remain non-unique (able to appear on the same page more than once).
  * A component's name must be unique to the project to ensure that only instances of the same component can have the same name. Re-using a component also means re-using its behavior. To use the same component with differing behavior requires a new component.
  * Selectors must remain context free and un-coupled to HTML by avoiding the use of elements within CSS selectors. HTML element styles are scoped by placing a class on either the element itself or on a parent container. This means all HTML element styles are opt-in (opposed to opt-out) making the only "default" HTML element styles are those applied by normalize, thus avoiding redundant overrides. [[27]](addendum.md) [[28](addendum.md)

#### State
A state is a variant of a component that is triggered by an action or behavior. State styles are applied dynamically as an additional HTML class attribute on the component's root or child HTML element. State based styles are indicated with the `is-` prefix, for example `.is-active` or `.is-disabled`. These style declarations are shared by CSS and JS files [[1]](addendum.md) and are defined with the component in the same partial. Multiple states may be used at once on the same component.


---

## Component Composition (OOCSS Classes)

>component composition is the building of the discrete modules of a system using common, object oriented, abstractions represented as an additional HTML class attribute. 

Building complex components with smaller, abstracted code blocks leads to more reusable code, easier debugging, and a DRYer code base while cutting down on repetition and increasing performance. It also allows for easier prototyping within the browser when skin and structure styles can be applied to a component separately. A component is comprised of object, structure, skin, and in some cases utilities. Class naming and selector construct is very important. This syntax and naming convention illustrates the intention of a class and its relationship to others.

Components use a multi-class pattern in order to allow for easier contextual based adjustments when necessary, and to help simplify class and variable names[[3]](addendum.md). For example, structure, skin, and state styles are extended via their own class, rather than attaching a suffix to an existing component class.

In this way a component can be thought of as a specific combination of classes. Changing even one of these classes constitutes an entirely different component. For example, the same button component with two different skin classes is actually two different components. Additionally, an object could be represented as a single class or even a Sass `@extend` such as a `%u-clearfix`. Notice that a component does not have to be a visual entity.


### Structure Styles
Styles which control a component's physical structure. Structure styles include any properties involving spacing which could potentially affect surrounding elements on the page, i.e. box-model properties. Structure classes extend an object class. There must be no dependencies between structure and skin.

### Skin Styles
Styles which control a component's visual appearance. Skin styles include any properties involving color, typography, gradients, shadows, etc. Skin classes extend an object class. There must be no dependencies between skin and structure.

*Note: Sometimes the distinction between structure and skin is non-trivial. For example, the arrival of border-box has greatly simplified the box-model, but makes the border property a bit more difficult to define in this context because it no longer contributes to an element's width (structure). The best way to handle this is to split up border property defining `border-width` and `border-style` as structure and `border-color` as skin. An example that makes this more clear is when building a tab component where the structure of the tab requires a transparent bottom border for the active tab and the skin of the tab requires a light gray border.*

### Layout Styles
Styles that define how/where a component sits on the page. A component's layout class uses the `l-` prefix followed by the component's name [[1]](addendum.md). Layout styles include width and grid layout.

  * All components are fluid by nature and should never be given explicit width or height restraints. A component's width is determined by its parent container or grid system.
  * Heights should only be explicitly defined for elements which had dimensions before they entered the system; i.e. image, video. In all other cases use `line-height` instead which is far more flexible [[13]](addendum).
  * The grid system should never have styles or box-model properties directly applied - grid items contain content, but are not content in of themselves.

### Icons
  * Icons should be styled as independent entities to allow their use in any component without the need for duplication of code.
  * Icon components are prefixed with `i-`.
  * Icon styles should be split into structure and skin (`.i-small` & `.i-primary` classes) in order to allow for maximum flexibility and minimal code repetition [[1]](addendum.md).
  * Use [Compass to manage sprits](http://compass-style.org/help/tutorials/spriting/).
  * Sprited Icons should be added to empty elements that have their text hidden off canvas.
  * Use [Compass URL Helpers](http://compass-style.org/reference/compass/helpers/urls/) to manage asset directories


### JavaScript
  * Custom `data-` attributes are reserved for applying dynamic behavior to a component. This keeps behavior out of the class attribute where component composition takes place. 
 * A `data-` attribute should never be referenced in a stylesheet. They are used exclusively for JavaScript files [[3]](addendum.md). Keeping these concerns separated makes development easier.

### QA
  * The only acceptable use of the HTML ID attribute is for the integration of quality assurance tooling.  Dedicating the ID attribute, as well as name-spacing these hooks with `qa-` ensures that they will never be used for any other purpose or accidentally removed from the markup. 
  * The prefix indicates the ID’s purpose, the number appended after the dash can be dynamically generated so every element has a unique identifier to build testing scripts for.

---

## Class Semantics

>"We shouldn't be afraid of making the connections between layers clear and explicit rather than having class names rigidly reflect specific content. Doing this doesn't make classes "unsemantic," it just means that their semantics are not derived from the content." - [Nicolas Gallager](https://twitter.com/necolas)

Class names should remain content-independent[[3]](addendum.md). By avoiding tightly coupled class names and content semantics, code is more easily reused and modularized to allow for increased scalability of your architecture. Because the most reusable code components are those with content-independent class names, class names should be derived from repeating structural or functional patterns and never from the content.

  1. Increasing semantic value of a section of html and content [[1]](addendum)
    * Content-layer semantics are served by html elements and attributes [[3]](addendum)
  2. Class names communicate useful information to developers and serve hooks for CSS or JavaScript [[3]](addendum.md).
    * Decrease the expectation of a specific HTML structure [[1]](addendum).

The important distinction is that the HTML class attributes are semantic in the way they convey meaning to the developer, rather than the content. Content receives it's semantic value from its markup (HTML tags and ARIA attributes). Code receives its semantic value from its classes.

### Specificity

>"The problem with such a depth is that it enforces a much greater dependency on a particular HTML structure. Components on the page can’t be easily moved around" - [Jonathan Snook](https://twitter.com/snookca)

Minimize "depth of applicability" in order to avoid over-reliance on a predefined HTML structure and hindering modularity and flexibility of components. This also helps to prevent introducing potential specificity issues which are notoriously difficult to debug. When selectors are kept succinct, it also becomes easier to convert components into templates for dynamic content [[1]](addendum.md).

### Guidelines for Minimal Specificity

  * Do not use CSS ID selectors.
  * Do not use location based selectors to change a component's appearance based on its page position or region - i.e. (main-content, side-bar, footer, etc)[[17]](addendum.md). When a component has different appearances create a new component by changing out its structure or skin class.
  * Always name-space state class names e.g. `.is-disabled` or `.is-collapsed` with a prefix.
  * Avoid the use of element selectors in order to keep them free from context and un-coupled to the HTML. Scope HTML element selectors with a class on the root element or a parent element so that these styles are opt-in rather than opt-out. This will avoid redundant overrides of un-needed styles and keep specificity minimal. [[1]](addendum.md) [[27]](addendum.md) [[28]](addendum.md)
  * `!important` should be avoided as much as possible. State and utility styles are an examples of an acceptable use of `!important` [[1]](addendum.md). The reason for this is that they are applied to the element and must override any default component styles.
  * Never qualify a selector with an element selector e.g. `ul.nav`, as this decreases selector performance, creates a context dependency, and increases the selector's specificity. These are all things to be avoided [[1]](addendum.md) [[12]](addendum.md). Applying styles directly to the element, or qualifying a slector with an element name should be considered as harmful as polluting the global name space in JavaScript. Don't do it.

---

## Selector Construct and Naming Conventions
Selector construct must explicitly communicate the context and function of the entity being named. Also, selector construct must be consistently applied to allow for efficient use of grep and more meaningful diffs. The BEM Methodology [[2]](addendum.md) and interpretations of BEM [[3]](addendum.md) [[13]](addendum.md) [[26]](addendum.md) make use of an efficient system to accomplish these goals by explicitly communicating the function and context of the entity being named, as well as its relationship to both child and parent components while avoiding deeply nested selectors that tie content to container and make assumptions about markup. In this way, a BEM-like system helps to reinforce our primary objective of modularity.
Admittedly, there is an element of added complexity, but the sacrifice of simple selectors in order to preserve objected oriented principles is well worth it, especially considering that the GZIP algorythm handles repetition extremely well.

An effective naming convention explicitly communicates the context and function of the entity being named.  Archetype relies on a structured, BEM-like[[2]](2) naming convention for building class names using meaningful hyphens, underscores, and cammelCase syntax to communicate the relationship between classes and their place within the system. There is a major division between objects, components, and utilities, as well as a minor separation of responsibilities built on top.

### Naming Pattern

This naming pattern is inspired by the BEM Methodology [[2]](addendum.md) as well as several interpretations by other developers [[3]](addendum.md) [[26]](addendum.md).

Example:
```scss
// component name
.object {...}                        /* represents the higher-level abstraction of a component */
.object__subObject {...}             /* a minor modification or extension of an object */
.object__modifier {...}              /* represents a modification of an object */
.component--extension {              /* extends an component with a skin or structure */
  &.is-active {...}                  /* represents a change in the component's state */
}          
.prefix-component-name {}            /* targets all component entities i.e. for layout */
```

Exampe HTML:
```html
<ul class="object object__modifier object--extension is-object-state">
  <li class="object__element is-active">...</li>
</ul>  
```

### Component

```scss
.primaryNav {...}
.primaryNav__item {...}

```

Example HTML:
```html
<ul class="o-nav o-nav__vertical primaryNav">     /* component */
  <li class="primaryNav__item">Nav Item</li>      /* sub component */
</ul>

```

### State

Example:
```html
 <button type="submit" class="btn btn--large btn--primary is-disabled">Submit</button>
```
Example:
```html
<ul class="nav nav__vertical primaryNav--large primaryNav--primary">
  <li class="primaryNav__item is-active">...</li>
</ul>
```

### Layout

Example:
```scss
.l-primaryNav {
  // primaryNav layout styles here
}
```

Example HTML:
```html
<ul class="nav nav__vertical primaryNav--large primaryNav--primary l-primaryNav">
  <li class="primaryNav__item is-active">...</li>
</ul>

```

### Icons

Example:
```html
<span class="i-account">My Account</span>
```


### JavaScript

Example:
```js
<ul class="nav nav__vertical primaryNav--large primaryNav--primary l-primaryNav" data-nav="primaryNav">
  <li class="primaryNav__item is-active">...</li>
</ul>

```


### QA

Example:
```html
<button id="qa-1234" class="btn btn--large btn--success">Click Here Stupid</button>
```

### Objects

Example:
```scss
.o-objectName {...}
```

Practical Example:
```scss
.o-nav {...}
```

Example HTML:
```html
<ul class="o-nav">
...
</ul>
```

### Sub Objects

Example:
```scss
.o-objectName__subObjectName {...}
```

Example HTML:
```html
<ul class="o-objectName o-objectName__subObjectName">
  ...
</ul>
```

Practical Example:
```scss
.o-nav__vertical {...}
```

Example HTML:
```html
<ul class="o-nav o-nav__vertical">
...
</ul>
```

### Component Extension

Example:
```scss
.primaryNav--structure {
  // structure styles extending the primaryNav component
}

.primaryNav--skin {
  // skin styles extending the primaryNav component
}
```

