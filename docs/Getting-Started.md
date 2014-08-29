# Getting Started

## Dependencies
  * ~~[Archetype-Utilities](https://github.com/kwaledesign/Archetype-Utilities)~~
  * [Modular-Scale](https://github.com/Team-Sass/modular-scale)
  * [Breakpoint](https://github.com/Team-Sass/breakpoint)
  * ~~[Colorkit](https://github.com/kwaledesign/Colorkit)~~

Archetype does not make any assumptions regarding layout allowing you to pull in your favorite grid or roll your own dependending on your project requirements.  However, there is a `_singularity-grid.scss` and a `_susy-grid.scss` partial file (disabled by default) to get started with either of those grid systems simply uncomment within `screen.scss` and also within `config.rb`.

  * [Singularity](https://github.com/Team-Sass/Singularity)
  * [Susy](http://susy.oddbird.net)

### Dexy
[Dexy](www.dexy.it) is an incredibly flexible documentation software built on Python that uses numerous filter plugins to allow for the use of live code examples to be output into any document you wish. Because everything is based on live code, updating documentation requires only a single command.  

Using Dexy to build responsive design deliverables is incredibly efficient because you can display code snippets, or the actual rendered output to document HTML, CSS and Sass, and JavaScript. Because this documentation is automatically updated, building and maintaining living, breathing style guides and pattern libraries is simple.

### Moving parts
There is a staggering amount of use cases that Dexy can satisfy and, therefore, quite a few moving parts. 

  * [Jinja](http://jinja.pocoo.org/) - The templating engine for Python which
    allows you to output you code any where you want using the appropriate
    filter.
  * [htmlsections](http://www.dexy.it/filters/Htmlsections.html) - Dexy's HTML
    filter that allows you to split markup according to HTML comments
  * [idio](http://www.dexy.it/filters/Idio.html) - Dexy filter to split
    document at comments that can be used with CSS, Sass, and JavaScript
  * [Pandoc](http://johnmacfarlane.net/pandoc/) - A very powerful markup 
    conversion utility that allows you to convert between markup language
    syntaxes.
  * [PhantomJS](http://phantomjs.org/) - a headless WebKit scriptable with
    a JavaScript API and [CasperJS](http://casperjs.org/) - a navigation
    scripting & testing utility written in JavaScript for PhantomJS. These two
    utilities allow for scriptable screen shots of components that can include
    both state (ie hover and active) and context (screen deminsion).




## Installation
~~Archetype can be installed as using the [Archetype Yeoman Generator](https://github.com/kwaledesign/generator-archetype) or via Git. There is also a [Archetype Jekyll Yeoman Generator](https://github.com/kwaledesign/generator-archetype-jekyll) that has an option to include [Style Docs](https://github.com/kwaledesign/Style-Docs), a framework for responsive design deliverables.~~

### Installation via Git

```bash
$ git clone https://github.com/Archetype-CSS/Archetype.git <your-project-name>

```
This creates a cloned Archetype repository named `<your-project-name>` within your root
project. To complete the setup of your new project you can run the
`archetype-setup.sh` shell script to automate the removal of unnecessary files,
initialize Git, and then remove the setup-script when complete.

Next, run the setup script

```
$ . archetype-setup.sh
```

You can now make your first commit

```
$ git commit -m "init commit"
```

You are now setup and ready to begin development on your project. For further
infomation, consult the [Archetype
Docs](http://kwaledesign.github.io/Archetype/).

### Installing Dexy
See the [Dexy Documentation](http://dexy.it).

### Use
If you are brand new to [Dexy](www.dexy.it) I would highly recommend completing several of the [tutorials](http://www.dexy.it/guide/getting-started.html) and familiarizing your self with [Dexy's commands](http://www.dexy.it/guide/command-line-interface.html). Once you wrap your head around how Dexy's filter system works along with several of the other moving parts used in our specific use case, it becomes pretty strait forward.

Setup Dexy

```
$ Dexy setup
```

Run Dexy (optionally pass the -r flag which resets Dexy before running)

```
$ Dexy -r
```

Dexy will then run and if successful it will output your static site files into the `output-site` directory. If there were errors, Dexy will print those to the screen and also record them within the `log` directory.

Dexy also has a built in server that runs on Python and is configured to symlink your generated site files into your root directory.

To start a server run the following from your root directory

```
$ Dexy serve
```
Copy and paste the output URL into a browser to view your site files.




## Customize and Extend


## Build Process

Archetype is built on [Bower](http://bower.io), [Grunt](http://gruntjs.com), and [Git](https://github.com/Archetype-CSS). The integrated build process can be managed with the following grunt commands. 

Archetype's build process is configured with the following:
  * `config.json` - provide global path variable to use within tasks
  * `Gruntfile.js` - main Grunt config, setup to use modular tasks with [load-grunt-tasks](https://github.com/sindresorhus/load-grunt-tasks)
  * `tasks/aliases.yml` - provide task aliases and trigger sub-tasks sequentially
  * `tasks/options/` - where the individual tasks are kept

| Grunt Task       | Description        |
| ------------- | --------------------- |
| `grunt`      | run all default grunt tasks in succession (`clean`, `compass`, `coffee`, )  |
| `grunt build`      | rebuild the project, create production assets. runs `clean`, `compass`, `coffee` |
| `grunt concat` | run only the concatenation tasks. combines all the CSS files generated by the compass task in `tmp/assets/css` and outputs a single `main.scs` file within the `public/assets/css/` directory  |


