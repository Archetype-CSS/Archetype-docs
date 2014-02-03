# Archetype Design Principles

## General Guiding Principles for Front-End Design

Archetype abstracts document semanticspresentationand behavior in order to achieve a level of modularity that allows the modification of its components without impact on the overall system.

  * Front-end design principles must be clearly articulated so that the focus can be applied towards achieving project goals within this context. 
  * Design principles are defined as user versus developer driven so that if they ever come into conflictthe user centric goals are persevered [22](addendum.md).
  * Naming conventions are extremely important and must be clearly defined and strictly adhered to. This facilitates easy use of grep and more meaningful diffs.
  * All code in any code-base should appear as if the same person wrote it by remaining consistent in the application of coding standards.

### User Centered Goals
Above all elsea site must be highly performantwidely accessiblyand device agnostic. The achievement of these goals necessitates the understanding that a site likely will not appear exactly the same on all browsers and devices.

#### User Centric Objective
  1. Adhere to standards as they are defined by the language specification
  2. Apply [progressive enhancement](pe.md) by serving core site content and functionality to all user agents and serving an enhanced experience built on top of the basic experience. ~~Apply JavaScript to enhance the site with a richer experience when it is supported and enabledbut do not require it in order to complete any core tasks on the site.~~
  3. Polyfil only essential features and avoid including additional library code whenever possible. 

### Developer Centric Goals
A code base must be maintainableit must be readableand it must be designed for modularity.

#### Development Objectives
  1. Minimize coupling between components by following Object Oriented methodologies
  2. Design systems not pages by building a collection of components and layoutswhich can be assembled together to create a specific experience.  Avoid page-specific styling in favor of component modifiers and class extensions.
  3. Easily maintain the project's design system by following style guide driven development [20](addendum.md) that is made with HTML and CSSuses production CSSand uses git for version control [21](addendum.md). A project's style guide should also be automatically updated to reflect changes in the code base and facilitate testing throughout the project development cycle.
  4. Maintain minimal specificity whenever possible.
  5. Testable
    * Test for coding standard compliance
    * Test for visual regression (unit level)
    * Test for selector chain redundancy 
  6. Documentation 
    * Style Guide
    * Coding Standard

### Object Oriented Principles

**Single Responsibility Principle**
An object or component should have only a single responsibilityand that responsibility should be entirely encapsulated by the object/component [7](addendum.md) [8](addendum.md). Avoid coupling skinstructureand layout within a single rule (i.e. box-model styles should never be applied along with background or text color within in the same ruleset).

**Extension over Modification**
Never directly edit the base styles (the object) of a componentunless you are certain you wish for this change to apply globally to all components that extend it. Use an additional class applied to the same instance of the base component to extend or overwrite the base component.  Extensions should not radically alter the end user’s expectation of an object’s functionality.

**Open/Closed Principle**
entities (classesmodulesfunctionsetc.) are open for extensionbut closed for modification. Base rules may be extendedbut not directly modifiable. This is why directly styling HTML tags is not acceptable - reduce the amount of global element styles in order to reduce the chances of breaking the open/closed principle [7](addendum.md) [9](addendum.md). Opt innever opt out - in order to avoid redundant overrides and code bloat.

**Composition over Inheritance**
Whenever possibleabstract specific functionality into isolation to be used to compose complete UI components.  Whenever similar code is being written more than oncelook to abstract (i.e. vertical-spacing).  Standardizing similar styles cuts down on excess code and needless and/or inadvertent divergent implementation of similar patterns.

Composition takes place in the HTML applying classes directly to the elements you wish to style.

**Liskov Substitution Principle**
objects should be replaceable with instances or their sub-components without breaking. Sub-components that extend a module should be interchangeable with the base module itself. To keep true to this principlea module's subcomponent(s) should never affect layout [7](addendum.md).

**~~Entity Segregation Principle~~**
~~If ever it becomes awkward to interchange a subcomponent with its base moduleor if it becomes necessary to redefine too many propertiesmove the subcomponent into its own custom module. It is sometimes better to have multiple base modules opposed to a single generic module with multiple sub-components. Never make sacrifices in functionality in the name of utility. Taken too farcode abstraction becomes [7](addendum.md) detrimental. When writing modular CSSit's not about maintaining modularity in the actual codebut rather modularity in the actual design [10](addendum.md).~~

**Minimize Coupling** ~~(isn’t this similar to segregation principle?)~~
Build multiplespecific objectsrather than overly generic.  This helps to avoid tight coupling between unrelated modulesmaking it easier to make changes without inadvertently affecting other modules.  Avoid abstractions that attempt to do too much.  Smallermore specific abstractions are prefered.

Never couple styles to particular DOM elements or to a particular DOM structure. Never assume specific node children. (i.e. use a .nav-item class on each child rather than a .nav & li a selector chain).

**Encapsulation**
The UI of complex applications becomes needlessly brittle when components are not built independant of one-another.  Never write UI code that reaches into ancestral and/or sibling context.  Never write UI code that leaks styles downstream into nexted components.  A component should never rely on the existence or appearance of descendant componentsas long as they don’t break the layout of the parent component.

**DRY**
(don't repeat yourself) - aimed at reducing repetition of information of all kinds. Every piece of knowledge must have a singleunambiguousand authoritative representation within the system.

**Documentation**
Heavily document components describing how it should be usedwhy specific CSS properties are neededand the recommended markup pattern.  Any browser specific hacks should documented particularly well.




