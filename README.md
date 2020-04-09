Before running `./watch.sh` you must install some npm packages:

```bash
npm i -g watchify tsify typescript
```

I do not care which module system I use if I am able to use the ES6 TypeScript import/export syntax. Why does AMD put just main.ts in the bundle.js file, while UMD puts all the needed modules in it? How can I use AMD (which I understood that is good for the browsers) so that the bundle.js file contains all the needed code? I just change between AMD and UMD:

AMD:

> 1879 bytes written to js/bundle.js (0.06 seconds) at 14:57:28

UMD:

> 164682 bytes written to js/bundle.js (0.34 seconds) at 14:58:10

If I use UMD, I get a single relevant error in the browser console:

```
Uncaught ReferenceError: define is not defined
    at Object.1 (_prelude.js:1)
    at o (_prelude.js:1)
    at r (_prelude.js:1)
    at _prelude.js:1
1 @ _prelude.js:1
o @ _prelude.js:1
r @ _prelude.js:1
(anonymous) @ _prelude.js:1
```

The contents of `_prelude.js` as received by the browser: a single line of code:

```js
(function(){function r(e,n,t){function o(i,f){if(!n[i]){if(!e[i]){var c="function"==typeof require&&require;if(!f&&c)return c(i,!0);if(u)return u(i,!0);var a=new Error("Cannot find module '"+i+"'");throw a.code="MODULE_NOT_FOUND",a}var p=n[i]={exports:{}};e[i][0].call(p.exports,function(r){var n=e[i][1][r];return o(n||r)},p,p.exports,r,e,n,t)}return n[i].exports}for(var u="function"==typeof require&&require,i=0;i<t.length;i++)o(t[i]);return o}return r})()
```
