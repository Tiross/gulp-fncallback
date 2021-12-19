gulp-custom-callback
=============

[![npm version](https://badge.fury.io/js/gulp-custom-callback.svg)](https://www.npmjs.com/package/gulp-custom-callback)
[![Build status](https://github.com/Tiross/gulp-custom-callback/actions/workflows/build.yml/badge.svg)](https://github.com/Tiross/gulp-custom-callback/actions/workflows/build.yml)
[![Coverage Status](https://coveralls.io/repos/github/Tiross/gulp-custom-callback/badge.svg?branch=master)](https://coveralls.io/github/Tiross/gulp-custom-callback?branch=master)
[![Greenkeeper badge](https://badges.greenkeeper.io/Tiross/gulp-custom-callback.svg)](https://greenkeeper.io/)

Add own callback to streaming

## Install

```
npm install --dev gulp-custom-callback
```

## Usage transformFunction
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      console.log(file);
      cb();
    }))
    .pipe(gulp.dest('./public/css'));
});
```

## Usage transformFunction and flushFunction
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      console.log(file);
      cb();
    }, function (callback) {
      callback();
    }))
    .pipe(gulp.dest('./public/css'));
});
```

## Usage transformFunction with error
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      console.log(file);
      cb('error');
    }))
    .pipe(gulp.dest('./public/css'));
});
```

## Usage transformFunction with new file
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      var newFile = ...
      cb(null, newFile);
    }))
    .pipe(gulp.dest('./public/css'));
});
```

## Usage transformFunction with new file and append old file
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      var newFile = ...
      cb(null, newFile, true);
    }))
    .pipe(gulp.dest('./public/css'));
});
```

## Options

once - Run callback once
```javascript
var less = require('gulp-less');
var callback = require('gulp-custom-callback');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(callback(function (file, enc, cb) {
      console.log(file);
      cb();
    }, {
      once: true
    }))
    .pipe(gulp.dest('./public/css'));
});
```
