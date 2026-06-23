# Module Systems in JavaScript and Node.js

- JavaScript lacked a built-in module system for a long time.
- Browser code used multiple `<script>` tags to load files.
- This approach worked for simple sites but did not scale.
- Frameworks like jQuery, Backbone, and AngularJS highlighted the need for modules.
- AMD (RequireJS) and UMD were early module system proposals.
- Node.js introduced a filesystem-based module system instead of `<script>` tags.
- Node.js adopted CommonJS for browserless JavaScript environments.
- CommonJS was not part of ECMAScript; it was an independent standard.
- CommonJS became dominant in Node.js and influenced browser bundlers like Browserify and Webpack.
- ES modules were standardized in ES2015.
- ES modules aim to unify browser and server module handling.
- Node.js gained stable ES module support in version 13.2 (2019).
- During transition, developers published dual-mode libraries supporting both ESM and CommonJS.
- Today:
  - ES modules are the preferred choice for new projects.
  - CommonJS remains common in legacy code bases.
