<h3>Controllers</h3>

<ul>
<li>Controllers are the glue between views and models. Most of their logic concerns event management. Keep controllers skinny.</li>
<li>Any communication between children and parent controllers should use events (do not pass an instance of the parent around).</li>
<li>Should only know about sub controllers.</li>
<li>Should be scoped to a single element, and not access or alter other parts of the DOM.</li>
<li>Should have a unique class name, and all CSS relevant to this controller should be namespaced by this class name.</li>
<li>Should work even if their element is not appended to the DOM tree. This is useful for testing and demonstrating the controller is properly scoped.</li>
<li>Should be testable by firing events programatically on their sub elements.</li>
<li>Should be able to be re-rendered at any time without adverse effects.</li>
<li>Should not use the DOM to store state &mdash; keep any view specific state stored as instance properties in the controller.</li>
</ul>

<h3>Views</h3>

<ul>
<li>Should be logic less except for flow control and helper functions.</li>
<li>Should be passed all the data they need to render directly. It should all be available in the current scope.</li>
</ul>

<h3>Models</h3>

<ul>
<li>Should purely be concerned with data, manipulating data and decorating data.</li>
<li>Should never access controllers or views.</li>
<li>Should never access or return DOM nodes.</li>
<li>Should only access or require other models at runtime.</li>
<li>Should abstract away XHR connections from the rest of the application.</li>
<li>Should contain all data validations.</li>
</ul>

<h3>Routers</h3>

<ul>
<li>Should be as logic-less as possible.</li>
<li>Should not know about or access the DOM.</li>
</ul>

<h3>Global state</h3>

<ul>
<li>Should be kept to a minimum as it arguably violates MVC. You can&#39;t get around it for some things though, like the current user, current view, CSRF token etc.</li>
<li>Should never be stored in global variables.</li>
<li>Should all be stored in one place (such as a singleton instance of a model).</li>
</ul>

<h3>Modules</h3>

<ul>
<li>You should always use a module system, whether it&#39;s CommonJS, AMD, ES6 modules, or something equivalent.</li>
<li>Never set or access global variables.</li>
</ul>

<hr>

<h3>Pull requests accepted</h3>

<p>A style guide should be a fluid document and evolve as your team encounters specific problems and gains experience. Its main purpose is to keep the codebase consistant and clean. If you have any suggestions for this document, tweet them to me at <a href="https://twitter.com/maccaw">@maccaw</a>.</p>

  </div>
</section>


  </article>

  inspired by: [mvc-style-guide](http://blog.sourcing.io/mvc-style-guide)
