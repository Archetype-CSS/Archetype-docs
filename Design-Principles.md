# Archetype Design Principles

## General Guiding Principles for Front-End Design

Archetype abstracts document semantics, presentation, and behavior in order to achieve a level of modularity that allows the modification of its components without impact on the overall system.

  * Front-end design principles must be clearly articulated so that the focus can be applied towards achieving project goals within this context. 
  * Design principles are defined as user versus developer driven so that if they ever come into conflict, the user centric goals are persevered [[22]](addendum.md).
  * Naming conventions are extremely important and must be clearly defined and strictly adhered to. This facilitates easy use of grep and more meaningful diffs.
  * All code in any code-base should appear as if the same person wrote it by remaining consistent in the application of coding standards.

### User Centered Goals
Above all else, a site must be highly performant, widely accessibly, and device agnostic. The achievement of these goals necessitates the understanding that a site likely will not appear exactly the same on all browsers and devices.

#### User Centric Objective
  1. Adhere to standards as they are defined by the language specification
  2. Apply [progressive enhancement](pe.md) by serving core site content and functionality to all user agents and serving an enhanced experience built on top of the basic experience to more capable browsers and devices.
  3. Polyfil only essential features and avoid including additional library code whenever possible. Performance *IS* user experience. 

### Developer Centric Goals
A code base must be maintainable, it must be readable, and it must be designed for modularity.

#### Development Objectives
  1. Minimize coupling between components by following Object Oriented methodologies
  2. Design systems not pages by building a collection of components and layouts, which can be assembled together to create a specific experience.  Avoid page-specific styling in favor of component modifiers and class extensions.
  3. Easily maintain the project's design system by following style guide driven development [[20]](addendum.md) that is made with HTML and CSS, uses production code, and uses git for version control [[21]](addendum.md). A project's style guide should also be automatically updated to reflect changes in the code base and facilitate testing throughout the project development cycle.
  4. Maintain minimal specificity whenever possible.
  5. Testable
    * Test for coding standard compliance
    * Test for visual regression (unit level)
    * Test for redundancies
  6. Documentation 
    * Style Guide
    * Coding Standard

### Object Oriented Principles

#### Single Responsibility Principle
An object or component should have only a single responsibility, and that responsibility should be entirely encapsulated by the object/component [[7]](addendum.md) [[8]](addendum.md). Avoid coupling skin, structure, and layout within a single rule (i.e. box-model styles should never be applied along with background or text color within in the same ruleset).

#### Extension over Modification
Never directly edit the base styles (the object) of a component, unless you are certain you wish for this change to apply globally to all components that extend it. Use an additional class applied to the same instance of the base component to extend or overwrite the base component.  Extensions should not radically alter the end user’s expectation of an object’s functionality.

#### Open/Closed Principle
Entities (classes, modules, functions, etc.) are open for extension, but closed for modification. Base rules may be extended, but not directly modifiable. This is why directly styling HTML tags is not acceptable - reduce the amount of global element styles in order to reduce the chances of breaking the open/closed principle [[7]](addendum.md) [[9]](addendum.md). Opt-in, never opt-out, in order to avoid redundant overrides and code bloat.

#### Composition over Inheritance
Whenever possible, abstract specific functionality into isolation to be used to compose complete UI components.  Whenever similar code is being written more than once, look to abstract (i.e. vertical-spacing).  Standardizing similar styles cuts down on excess code and needless and/or inadvertent divergent implementation of similar patterns.

Composition takes place in the HTML applying classes directly to the elements you wish to style.

#### Liskov Substitution Principle
Object extensions should be replaceable with other extensions of the same object without breaking. For example, applying a different component skin or structure to a base object must not affect the object itself.

#### Entity Segregation Principle
It is sometimes better to have multiple base objects opposed to a single generic object with multiple sub-objects. Never make sacrifices in functionality in the name of utility. Taken too far, code abstraction becomes  detrimental [[7]](addendum.md). When writing modular CSS, it's not about maintaining modularity in the actual code, but rather modularity in the actual design system [[10]](addendum.md).

#### Minimize Coupling
Build multiple, specific objects, rather than overly generic ones.  This helps to avoid tight coupling between unrelated modules, making it easier to make changes without inadvertently affecting other modules.  Avoid abstractions that attempt to do too much.  Smaller, more specific abstractions are preferred. Never couple styles to particular DOM elements or to a particular DOM structure. Never assume specific node children. (i.e. use a `.nav-item` class on each child rather than a `.nav & li a` selector chain).

#### Encapsulation
The UI of complex applications becomes needlessly brittle when components are not built independent of one-another.  Never write UI code that reaches into ancestral and/or sibling context.  Never write UI code that leaks styles downstream into nested components.  A component should never rely on the existence or appearance of descendant components, as long as they don’t break the layout of the parent component.

#### DRY
Reduce repetition when ever possible. Every piece of knowledge must have a single, un-ambiguous, and authoritative representation within the system.

#### Documentation
Heavily document components describing how it should be used, why specific CSS properties are needed, and the recommended markup pattern.  Any browser specific hacks should documented particularly well.

