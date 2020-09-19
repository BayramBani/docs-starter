# Gulp
---

- Install

```bash
npm install --save-dev gulp
```

- Create a gulpfile.js

````javascript
const {src, dest, parallel, series} = require('gulp');
const cleanBuild = require('gulp-clean');
const minifyCSS = require('gulp-csso');
const minifyJS = require('gulp-uglify');
const minifyHTML = require('gulp-minify-html');
const concat = require('gulp-concat');
const babel = require("gulp-babel");
const {phpMinify} = require('@cedx/gulp-php-minify');

function clean() {
  return src('build/*', {read: false})
      .pipe(cleanBuild())
}

function css() {
  return src('assets/css/*.css')
      .pipe(minifyCSS())
      .pipe(concat('bundel.min.css'))
      .pipe(dest('build/'))
}

function js() {
  return src('assets/js/*.js', {sourcemaps: true})
      .pipe(babel())
      .pipe(minifyJS())
      .pipe(concat('bundel.min.js'))
      .pipe(dest('build/', {sourcemaps: true}))
}

function html() {
  return src('gulp.html', {sourcemaps: true})
      .pipe(minifyHTML())
      .pipe(concat('index.html'))
      .pipe(dest('build/'))
}

function php() {
  return src('php.php', {read: false})
      .pipe(phpMinify())
      .pipe(dest('build/'))
}

exports.clean = clean;
exports.js = js;
exports.css = css;
exports.html = html;
exports.php = php;
exports.default = series(clean, parallel(css, js, html, php));

````

- Run gulp

```bash
gulp
```
