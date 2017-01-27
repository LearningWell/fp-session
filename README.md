# Functional programming

This is slides for introducing functional programming.

## Tech use

[Reveal.js](https://github.com/hakimel/reveal.js/) is used as the HTML presentation framework.

## How to add/modify slides

Markdown separated into their own files are used as presentation data. They're located under `/slides/`. To add a slide, add a markdown file somewhere in there and add a reference in `index.html`, where each file is referenced in the `body` like this: `<section data-markdown="/slides/fp/first.md"></section>`.

## How to run

First: `npm install`. Then, you'll need to host the `index.html` with any http server. If you got python (>= 2.0) installed, just execute `npm start` which will host the file with the built in http server in python. When the server is up and running, navigate to `http://localhost:3000` (or whatever port you hosted it on).