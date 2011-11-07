# Sass example code for A List Apart

This project contains full source code examples for my article "[TITLE TBD]" appearing in the Nov. 29 issue of A List Apart.

## What's in this project

The `examples/` directory contains both my Sassy CSS (`.scss`) style sheet source files and their compiled CSS. The files are named for the SCSS feature or concept they're intended to illustrate, and numbered in order of appearance in the article.

### A brief note about Sass output styles

All of the style sheets in this project have been processed using Sass's "expanded" style. Sass supports three styles of CSS output, which roughly translate to different levels of readability and minification.

The _nested_ style (which is the default one used if you don't specify a style) balances readability and download size: every selector and property is on its own line, but there are no extra linebreaks between rules, or before or after closing curly braces. It also tries to represent nested properties in the output through indentation:

    body.home .media-unit {
      border: 1px solid #ccc;
      background-color: #fff; }
      body.home .media-unit .right {
        border-left: 1px solid #ccc; }
        body.home .media-unit .right h1 {
          font-size: 24px; }

The _compact_ style places each rule on its own line, with properties (or, in the case of media queries, nested rules) following on the same line. This can be useful when debugging, making it somewhat easier to identify which rule is responsible for a given style.

    .container { width: 940px; }
    @media screen and (max-width:940px) { .container { width: auto; } }
    .container .main-content { width: 600px; }
    @media screen and (max-width:940px) { .container .main-content { width: 63.8%; } }

The _compressed_ style is full minification, with all rules on a single line with no unnecessary white space.

    .result-with-highlights span{font-weight:bold}.highlighted{font-weight:bold}

Finally the _expanded_ style, which (again) I used to compile the examples contained in this project, is designed to look like well-formed, handcrafted CSS, emphasizing readability over compactness.

    .container {
      width: 97.917%;
    }
    .container .main-content {
      width: 65.957%;
    }
    .container .sidebar {
      width: 31.915%;
    }

In production, you will probably want to use the _compressed_ style to improve download times. When designing/developing, any of the others will do.

## Compiling SCSS from the command line

For the technically minded, or anyone who's handy with their computer's command line shell, you can use this command to start the Sass compiler and set it to automatically watch for and process changes to any of the .scss files in this project:

    sass --watch=examples:examples --style=expanded
    
You can easily use this on your own project; the command follows the following pattern:

    sass --watch=<INPUT_DIRECTORY>:<OUTPUT_DIRECTORY> --style=<STYLENAME>

For example, if you're working on a static site where you want all your compiled CSS to be saved to the `css` directory, you can keep all your SCSS source files in a subdirectory called `css/_scss` and use this command to start the compiler:

    sass --watch=css/_scss:css --style=expanded

If you're using a graphical interface to Sass, such as the [Scout](http://scout-app.com) app I mentioned in my article, just follow its on-screen directions and you should be set.

## Debugging Sass

If you're accustomed to debugging issues with your CSS code in a tool like Firebug for Firefox, or the Web Inspector in Safari or Chrome, you may find you run into some difficulty caused by the line numbers in your compiled CSS not matching the ones in your original Sass code.

To address this (at least for Firebug users), Sass co-creator Nathan Weizenbaum created a plugin called [FireSass](https://addons.mozilla.org/en-US/firefox/addon/firesass-for-firebug/), which can read special debug information you can optionally embed in your CSS by passing a command-line flag to the Sass compiler or flipping a setting in Scout.

If you're compiling from the command shell, just add the `--debug-info` flag when starting Sass:

    sass --debug-info --watch:css/_scss:css

The debug info looks like this:

    @media -sass-debug-info{filename{font-family:file\:\/\/\/Users\/david\/Work\/Personal\/ala_sass_examples\/examples\/08_fluid_layout\.scss}line{font-family:\000031}}
    .container {
      width: 97.917%;
    }

The debug info tells FireSass what file and line number of your original Sass code generated a particular rule, so it can display that instead of the compiled CSS's info. The font-family and `@media` stuff disguises the debug info as valid CSS, so your style sheet can be parsed and read by the browser. It's very verbose, so you probably don't want to include it in your production output, but it can be very handy during development.

