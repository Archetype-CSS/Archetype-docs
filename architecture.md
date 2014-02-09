# Architecture

>"By categorizing CSS rules we begin to see patterns and can define best practices around each of these patterns" -  [Jonathan Snook](http://smacss.com/book/categorizing)

## Directory Structure

Archetype is a modular design system for building UI components. Most of Archetype's utilities, objects, and components are managed with [Bower](http://bower.io) within the `bower_components` directory. It is a best practice to [version control Front-End packages](http://addyosmani.com/blog/checking-in-front-end-dependencies/). These modules are `@import`-ed into a project, customized to your needs, and controlled with:

  * `main.scss`
  * `base/`
  * `components/`

## main.scss

Partials should be used for all base, component, and layout styles. These partials are then `@import`-ed into `main.scss` which provides the opportunity to easily turn components of the design system on and off as needed. When including partials within your `main.scss` stylesheet, leave off the file extension to allow for easier conversion between Sass and SCSS syntaxes if you ever need to do so [[17]](addendum.md). Example [Archetype's main.scss](https://github.com/Archetype-CSS/Archetype/blob/master/sass/main.scss)

### Base
The base directory contains styles and settings that apply to the entire project. These include the `_color-pallet.scss` and `_typography-pallet.scss` partials as well as settings for compass and compass plugins. The `base/` directory is where all site-wide settings are controlled.

### Component
Components are modular and reusable entities of a design system. Everything within the design system is a component. Each component is maintained within its own repository, managed with [Bower](http://bower.io), and `@import`-ed into `main.scss`. All objects are prefixed with `o-`. They are installed using `bower install Archetype-o-[object-name]`. Archetype components have basic, default structure and skin styles applied for rapid prototyping. These default styles can be over-ridden. Archetype components are the equivalent to Modules within the [SMACSS](http://smacss.com/) methodology.

### Layout
Layout styles provide structure to mobile-first, linear content. These styles are used to progressively enhance the basic layout when device capability and/or viewport allow. Because layout is treated as an enhancement, these styles are kept separate from the components they enhance and are applied with their own class. Each component's layout is defined in its own partial inside the layout directory. Layout stylesheets are named by prefixing the component's name with `l-` in order to explicitly define the relationship between layout and component. 

### Temporary
The temporary directory contains any styles that haven't yet been properly defined and organized within the project's architecture. This where any hacks or quick fixes belong. Each 'fix' placed within this directory should be given its own partial and should be accompanied by a corresponding issue properly tagged and filed in the project's repository so that it can be incorporated into the code base at a later date. Preventing sub-standard code from being committed into the code base helps to prevent unnecessary depreciation as well as unintentionally introducing bugs by keeping these 'fixes' quarantined within the temp directory. [[25]](addendum.md).


---

## Object Oriented CSS (OOCSS)

>"[A] CSS “object” is a repeating visual pattern which can be abstracted into an independent snippet of HTML CSS and possibly JavaScript. Once created an object can then be reused throughout a site." - [Nichole Sullivan](https://twitter.com/stubbornella)

### Two Main Principles of OOCSS

  1. **Separation of Structure from Skin** - distinguish between structure styles (box-model) and skin styles (color, font, gradients) and abstract these styles in class-based modules to allow re-use [[6]](addendum.md).
  2. **Separation of Container and Content** - avoid all explicit parent-child relationship within style declarations so that a component's style is not dependant upon its container which allows the module to be reused [[6]](addendum.md).

### Utilities
Archetype utilities are low-level abstractions used globally throughout a design system via a class, function, or mixin to provide specific functionality. Utilities are maintained within their own repository, managed with [Bower](http://bower.io), and are `@import`-ed within `main.scss` Archetype file. All utilities are prefixed with `u-`. They are installed using `bower install Archetype-u-[utility-Name]`. Some utility abstractions, like [u-display](https://github.com/Archetype-CSS/u-display) and [u-size](https://github.com/Archetype-CSS/u-size) can be applied to HTML elements directly.  In this case, they should be prefixed using the `u-utilityName` (in camelCase). Other utilities, (like functions and mixins) are applied within the stylesheet.

### Objects
Object styles are generic abstractions that can be extended to build a component. The classic OOCSS example is the media-object [[16]](addendum). Each object is maintained within its own repository, managed with [Bower](http://bower.io), and `@import`-ed into `main.scss`. All objects are prefixed with `o-`. They are installed using `bower install Archetype-o-[object-name]`.


### Sub Objects

An element is a context-dependant descendent of an object that performs a certain function and is represented by an additional class for a component or a descendent css selector. Sub Objects are denoted by the use of `__` (double underscores) i.e. `.component-name__element-name` in order to maintain the sub object's context, maintain control of the cascade, and avoid location-dependant selectors [[2]](addendum.md).

A sub-object is a context-dependant sibling of an object that performs a certain function and is represented by an additional class for a component. Sub-objects are similar to elements in syntax and in relation to an object, but they differ significantly in the way that a sub-object extends or provides minor overrides to the object and is applied to the same HTML element. Sub-objects are denoted by the use of __ (double underscores) i.e. .object-name__sub-object-name.

  * A variant of a component that inherits all the styles of its object, but differs by adding additional object styles, or providing minor overrides of its object. When object overrides become significant, the creation of an additional object should be considered.
  * A component's sub-object are siblings of the object and are prefixed with the full name of the parent object followed by __ (double underscores). This clearly indicates a sub-object's relationship to its object and also prevents the sub-object's styles from applying outside of the object's scope.
  * Sub-Objects are defined within their base object's partial file.

(~~this comes from 'Element', see: above:...~~)
An element is a context-dependant descendent of an object that performs a certain function and is represented by an additional class for a component or a descendent css selector. Elements are denoted by the use of __ (double underscores) i.e. .component-name__element-name in order to maintain the elements context, maintain control of the cascade, and avoid location-dependant selectors [[2]](addendum.md).


### Components

Styles which remain consistent and unchanged within a component regardless of skin or structure. These styles are abstracted and may be used as a foundation for building additional components. This is the base class that can be modified or extended with a structure and skin. Example: [Archetype's Objects](addendum.md)

A discrete and independent entity designed to exist as a stand alone module without any dependencies to its container. A component can be simple or compound (contain one or more components) and it should be able to be relocated on the page without breaking [[1]](addendum). Example components include buttons, navigation bars, etc. An example of a compound component would be a search block composed of an input and a submit button [[2]](addendum.md).

In order to maintain modularity a component must adhere to the following:

  *Component styles must not declare any explicit size constraints, allowing the module to scale to it's parent container. A component can be placed inside a layout component, i.e. a grid; or extended with a layout class, but it must never be given an explicit width.
  * A component must remain independent from siblings, children, and parents allowing for arbitrarily placement within a design system. This means that CSS ID Selectors must be avoided to allow components to remain non-unique (able to appear on the same page more than once).
  * A component's name must be unique to the project to ensure that only instances of the same component can have the same name. Re-using a component also means re-using its behavior. To use the same component with differing behavior requires a new component.
  * Selectors must remain context free and un-coupled to HTML by avoiding the use of elements within CSS selectors. HTML element styles are scoped by placing a class on either the element itself or on a parent container. This means all HTML element styles are opt-in (opposed to opt-out) making the only "default" HTML element styles are those applied by normalize, thus avoiding redundant overrides. [[27]](addendum.md) [[28](addendum.md)

#### State

A state is a variant of a component that is triggered by an action or behavior. State styles are applied dynamically as an additional class on the component's root or child HTML element.

  * State based styles are indicated with the is- prefix, i.e. .is-active.is-disabled. These style declarations are shared by CSS and JS files [[1]](addendum.md).
  * A component's state styles should be grouped with the component in the same partial.
  * Multiple states may be used at once.

*State styles are defined within their component*

---

## Component Composition (OOCSS Classes)

>component composition is the building of the discrete modules of a system using common, object oriented, abstractions represented as HTML class attributes. 

Building complex components with smaller, abstracted code blocks leads to more reusable code, easier debugging, and a DRYer code base by cutting down on repetition and increasing performance. It also allows for easier prototyping within the browser when skin and structure styles can be applied to a component separately. A component is comprised of object, structure, skin, and in some cases utilities. Class naming and [selector construct](https://github.com/Archetype-CSS/Archetype-docs/blob/master/architecture.md#selector-construct) is very important. This syntax and naming convention illustrates the intention of a class and its relationship to others.

Components use a multi-class pattern in order to allow for easier contextual based adjustments when necessary, and to help simplify class and variable names[[3]](addendum.md). For example, structure, skin, and state styles are extended via their own class, rather than attaching a suffix to an existing component class.

In this way a component can be thought of as a specific combination of classes. Changing even one of these classes constitutes an entirely different component. For example, the same button component with two different skin classes is actually two different components. Additionally, an object could be represented as a single class or even a Sass `@extend` such as a `%u-clearfix`. A component does not have to be a visual entity.


### Structure Styles
Styles which control a component's physical structure. Structure styles include any properties involving spacing which could potentially affect surrounding elements on the page, i.e. box-model properties. Structure classes extend an object class. There must be no dependencies between structure and skin.

### Skin Styles
Styles which control a component's visual appearance. Skin styles include any properties involving color, typography, gradients, shadows, etc. Skin classes extend an object class. There must be no dependencies between skin and structure.

*Note: Sometimes the distinction between structure and skin is non-trivial. For example, the arrival of border-box has greatly simplified the box-model, but makes the border property a bit more difficult to define in this context because it no longer contributes to an element's width (structure). The best way to handle this is to split up border property defining border-width and border-style as structure and border-color as skin. An example that makes this more clear is when building a tab component where the structure of the tab requires a transparent bottom border for the active tab and the skin of the tab requires a light gray border.*

### Layout Styles
Styles that define how a component sits on the page. A component's layout class uses the `l-` prefix followed by the component's name. Layout styles include width and grid layout.

  * All components are fluid by nature and should never be given explicit width or height restraints. A component's width is determined by its parent container or grid system.
  * Heights should only be explicitly defined for elements which had dimensions before they entered the system; i.e. image, video. In all other cases use line-height instead which is far more flexible [[13]](addendum).
  * The grid system should never have styles or box-model properties directly applied - grid items contain content, but are not content in themselves.
  * Layout based styles are indicated with the l- prefix in order to distinguish them from module or state styles [[1]](addendum.md)


### Icons

  * Icons should be styled as independent entities to allow their use in any component without the need for duplication of code.
  * Icon components are prefixed with `ico-`.
  * Icon styles should be split into structure and skin (`.ico-small` & `.ico-profile` classes) in order to allow for maximum flexibility and minimal code repetition [[1]](addendum.md).
  * Use Compass to manage sprits easily.
  * Sprited Icons should be added to empty elements that have their text hidden off canvas.
  * Use Compass to manage image directories easily


### JavaScript

  * Classes added dynamically via JavaScript are prefixed with .js- to indicate their dependency.
  * A '.js-' prefixed class should never be referenced in a stylesheet. They used exclusively from JavaScript files [[3]](addendum.md).


### QA
~~ (subset of utilities?? - only applied to the id attribute)~~

The only use of the HTML ID attribute is for the integration of quality assurance tooling.  Dedicating the ID attribute, as well as name-spacing these hooks with `qa-` ensures that they will never be used for any other purpose or accidentally removed from the markup. 

The prefix indicates the ID’s purpose, the number appended after the dash can be dynamically generated so every element has a unique identifier to build testing scripts for.


---

### Objects

Example:
```scss


```

### Sub Objects

Example:
```scss


```

### Object Extension

Example:
```scss


```

---
---


## Selector Construct and Naming Conventions

Selector construct must explicitly communicate the context and function of the entity being named. Also, selector construct must be consistently applied to allow for efficient use of grep and more meaningful diffs. The BEM Methodology [[2]](addendum.md) and interpretations of BEM [[3]](addendum.md) [[13]](addendum.md) [[26]](addendum.md) make use of an efficient system to accomplish these goals by explicitly communicating the function and context of the entity being named, as well as its relationship to both child and parent components while avoiding deeply nested selectors that tie content to container and make assumptions about markup. In this way, a BEM-like system helps to reinforce our primary objective of modularity.
Admittedly, there is an element of added complexity, but the sacrifice of simple selectors in order to preserve objected oriented principles is well worth it especially considering the fact that GZIP handles repetition extremely well.

An effective naming convention explicitly communicates the context and function of the entity being named.  Archetype relies on a structured, BEM-like[[2]](2) naming convention for building class names using meaningful hyphens, underscores, and cammelCase syntax to communicate the relationship between classes and their place within the system. There is a major division between objects, components, and utilities, as well as a minor separation of responsibilities built on top.


### Naming Pattern

This naming pattern is inspired by the BEM Methodology [[2]](addendum.md) as well as several interpretations by other developers [[3]](addendum.md) [[26]](addendum.md).

Example:
```scss


```

Exampe HTML:
```html


```

Exampe Use Case:
```html


```

**CONSIDER NAMESPACING SECTION HERE!!!!!
(QA/JS/U/ETC…)??**



### Component

```scss


```




```scss
***correction:  the above markup generates the following CSS:***

.object li {...}   //this is an over-qualified selector


***wither write this as: .object__li (ex: .nav__item) or explore using Sass3.3 @root syntax***
```

Example HTML:
```html


```


### State

Example:
```html

```

### Layout

Example:
```html

```

### Icons

Example:
```html

```


### JavaScript

Example:
```js

```


### QA

Example:
```html

<button id=”qa-1234” class=”btn btn--large btn--cta”>click here stupid</button>
```





### Class Semantics

Class names should remain content-independent[[3]](addendum.md). By avoiding tightly coupled class names and content semantics, code is more easily reused and modularized to allow for increased scalability of your architecture. Because the most reusable code components are those with content-independent class names, class names should be derived from repeating structural or functional patterns and never from the content.

>"We shouldn't be afraid of making the connections between layers clear and explicit rather than having class names rigidly reflect specific content. Doing this doesn't make classes "unsemantic"it just means that their semantics are not derived from the content." - [Nicolas Gallager](https://twitter.com/necolas)


  1. Increasing semantic value of a section of html and content [[1]](addendum)
    * Content-layer semantics are served by html elements and attributes [[3]](addendum)
  2. Class names communicate useful information to developers and serve hooks for CSS or JavaScript [[3]](addendum.md).
    * Decrease the expectation of a specific HTML structure [[1]](addendum).

The important distinction is that the HTML class attributes are semantic in the way they convey meaning to the developer, rather than the content. Content receives it's semantic value from its markup (HTML tags and ARIA attributes). Code receives its semantic value from its classes.

### Specificity

>"The problem with such a depth is that it enforces a much greater dependency on a particular HTML structure. Components on the page can’t be easily moved around" - [Jonathan Snook](https://twitter.com/snookca)

Minimize "depth of applicability" in order to avoid over-reliance on a predefined HTML structure and hindering modularity and flexibility of components. This also helps to prevent introducing potential specificity issues which are notoriously difficult to debug. When selectors are kept succinct, it also becomes easier to convert components into templates for dynamic content [[1]](addendum.md).

### Guidelines for Minimal Specificity

Do not use CSS ID selectors.
Do not use location based selectors to change a component's appearance based on its page position or region - i.e. (main-content, side-bar, footer, etc)[[17]](addendum.md). When a component has different appearances create a new component by changing out its structure or skin class.
Always name-space state class names e.g. `.is-disabled.is-collapsed`.

Example:
```scss


```

  * Avoid the use of element selectors in order to keep them free from context and un-coupled to the HTML. Scope HTML element selectors with a class on the root element or a parent element so that these styles are opt-in rather than opt-out. This will avoid redundant overrides of un-needed styles and keep specificity minimal. [[1]](addendum.md) [[27]](addendum.md) [[28]](addendum.md)
  * !important should be avoided as much as possible. State classes are an example of an acceptable use of important [[1]](addendum.md).
  * Never qualify a selector with an element selector e.g. `ul.nav`, as this decreases selector performance, creates a context dependency, and increases the selector's specificity. These are all things to be avoided [[1]](addendum.md) [[12]](addendum.md).


## ~~Practical Example (potentially eliminate this and instead link to code example)~~

### Object:
```scss


~~~

### Component:
```scss


```

### Layout:
```scss


```

### HTML:
```scss


```

