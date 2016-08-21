The nCoda amazeUI Repository
============================

This fork of amazeUI holds nCoda-specific customizations on nCoda infrastructure. We're using the
customization strategy envisioned by the amazeUI developers themselves, however there are two
shortcomings for us: (1) their idea of a "customization" is letting you choose which CSS/JS
components to include in the generated output, where we also need to add and modify styles;
and (2) they predict we'll only have one customization, where we need at least three.

The way we're using amazeUI in nCoda has two benefits for us. First, it helps retain visual
consistency everywhere we use amazeUI. Second, it helps us know where to make a change to CSS rules.


Setup
-----

Build the Sphinx customization for nCoda.

1. Run `npm install`
2. Run `npm install -g gulp-cli`


Build
-----

Generate the CSS for one of the amazeUI customizations.

1. Make a symlink from `tools/tasks/config.json` to one the relevant theme-specific config file.
2. Run `gulp customize`.
3. Find the resulting CSS and JavaScript in the `dist/customized` directory.
4. Do not commit the `config.json` symlink.


Where to Make Changes
---------------------

1. Avoid changing LESS or CSS anywhere but the nCoda amazeUI "themes."
2. If the change is sensible for all nCoda web properties, put it in the "ncoda" theme.
3. If the change is only useful for one web property, but it in that theme.

Example 1: If we change the nCoda "active" colour, that belongs in the "ncoda" theme.

Example 2: If we change spacing in the StructureView, that belongs in the "julius" theme.


The nCoda Plan
--------------

We're combining the "customization" with "themes" held in the `less/themes` directory. The "flat"
and "one" themes are from amazeUI itself; at the moment nCoda uses four themes:

- The "ncoda" base theme provides a consistent visual appearance across all our web properties.
- To the base, the "sphinx" theme adds rules required only for Sphinx-generated Python documentation.
- To the base, the "ncodamusic.org" theme adds rules required only for the Pelican-generated website.
- To the base, the "julius" theme adds rules required only for *Julius* components.

You can't build the base theme by itself. You can build any of the other themes by LESS compiling
the "theme.less" file in its directory. This is done automatically when you run `gulp customize` as
described above, which also minifies the CSS and generates the JavaScript required for the theme.

Each nCoda theme is hooked into the `gulp customize` task with its own JSON configuration file.
Unfortunately, the gulp task requires its configuration file to be called "config.json" and to be
held in the `tools/tasks` directory. That's why we have to use the symlink mentioned above in the
"Build" section. Eventually we'll add a commandline flag to allow setting the path to the JSON config
file at runtime, then contribute this to upstream amazeUI, but we haven't had time yet.
