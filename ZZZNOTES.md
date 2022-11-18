---
title: zzznotes
---

{% raw %} <!-- prevents code from being read -->

### PROJECT INFO
- attempt #3: followed jekyll tutorial again https://jekyllrb.com/docs/step-by-step/01-setup/, satisfying success B^)
- no posts or production build, just normal and collection pages
- no spaces in filenames (standard practice + breaks navigation highlighting)
- use relative_url filter instead of site.baseurl, fewer moving parts
  - {{ "/about.html" | relative_url }}
  - [description]({{ '/about.html' | relative_url }})
  - (i think the only /webbed-site is in main.scss custom font import)

### TEST SITE LOCALLY
- http://localhost:4000/webbed-site/
- bundle exec jekyll serve
- bundle exec jekyll serve --livereload

### JEKYLL
- prefix all commands with "bundle exec" to ensure correct jekyll version
- to use variables, metadata (ex: title), and liquid, add front matter to any markdown or html file

### MARKDOWN
- markdown guide https://itsfoss.com/markdown-guide/
  - line break: 2 spaces after line + enter
  - new paragraph: enter x2
  - to escape characters that would be used to format markdown (ex: * _ () #) prepend with backslash \
  - image = link prepended with !
- using html tags in markdown is encouraged https://daringfireball.net/projects/markdown/syntax#html
  - inline can be used anywhere
  - block-level elements (ex: div, table, p) must be at root level and surrounded by a blank line on top and bottom

### LINKS: SITE URL / BASE URL
- url vs. baseurl https://mademistakes.com/mastering-jekyll/site-url-baseurl/
  - both are site-wide variables set in config, do not include trailing /'s
  - url: site's full url (https://makena-s.github.io)
  - baseurl: subdirectory the site is served from (/webbed-site), recommended for subdomains like github project sites
  - page url: everything after base url (/about.html)
- no way to automatically prepend baseurl to all site links...
- links: prepend {{ site.baseurl }} or use {{ "/about.html" | relative_url }} filter
- markdown links: [about page]({{ site.baseurl }}/about.html) or [about page]({{ '/about.html' | relative_url }})
- with baseurl defined in config, localhost now includes baseurl, so i can test links as they would be on github

### HTML / CSS NOTES
- class vs. id: an element can have many classes and can appear many times per page, while id's are exclusive and unique
- padding = inside element, margin = outside element
  - margin: auto; will horizontally center element within container
- value order based on number of values
  - 2: topbottom, rightleft
  - 3: top, rightleft, bottom
  - 4: top, right, bottom, left (clockwise)
- css selectors https://www.w3schools.com/cssref/css_selectors.php
  - a:link:not(.current) {} selects elements besides those with the "current" class
  - :last-child selects last child of parent (ex: last p in body)
- shadows
  - text-shadow for text, box-shadow for elements
  - filter: drop-shadow(1px 1px 1px orange)
- display: the most important css property for layout
  - a
- position: choose value then move with top/right/bottom/left properties
  1. static: default, not affected by properties, normal page flow (won't overlap)
  2. relative: can be moved relative to its normal position
  3. fixed: relative to viewport, doesn't move when scrolled
  4. absolute: can be moved relative to its nearest positioned ancestor (the box it's in), outside normal page flow
  5. sticky: toggles between relative and fixed depending on scroll position
- font size: em is a relative unit that allows users to resize text in browser menu
  - 1em = current font size, browser default is 16px
  - w3schools rec: set default size (100%) in body and use em to change other elements

### DATA LOCATIONS
- /_layouts: stores html page templates that can be used by other files
- /_includes: stores source code (ex: navigation bar) that can be used in other files
- /_data: stores YAML, JSON, and CSV files whose data can be used in other files
- /assets: stores CSS, JS, images, etc. that can be used in other files
  - css/styles.scss: CSS hub
- /_sass: stores SCSS that will be imported into CSS hub styles.scss
- /_coolpages: stores this collection's documents
- /_site: stores static site built by jekyll serve
- _config.yml: site settings such as title, collections, and layout defaults, does not automatically refresh with jekyll serve
- Gemfile: lists site's gems
- Gemfile.lock: locks current gem versions

### JEKYLL GLOSSARY
- ruby: the coding language jekyll is written in
- gem: ruby code package that performs specific functions
- jekyll: gem, a static site generator
- Gemfile: lists your site's gems, every jekyll site has one
- liquid: templating language with 3 main components: objects, tags, and filters
  - object: outputs predefined variables as page content, ex: {{ page.title }} displays the "page.title" variable
  - tag: defines logic and control flow, ex: {% if page.show_sidebar %} sidebar content {% endif %}
  - filter: changes the output of an object, ex: {{ "hi" | capitalize }}
- front matter: tells jekyll to process liquid, the YAML code between two ---'s at the start of your page
- front matter variable: defined in front matter, call in liquid with "page" variable, ex: my_num: 5 -> {{ page.my_num }} -> 5
- front matter defaults: config option to automatically add values to files' front matter  
- YAML: common ruby file format, stores data
- layout: html template that wraps around markdown page content, can be used by any page
  - you can call front matter in your layout file, it will use the front matter of the page the layout is called on
- layout inheritance: a layout can be wrapped in another layout
- {{ content }}: object used in layouts, a special variable that returns the rendered content of the page the layout is called on
- {% include name.html %}: tag used in layouts, includes content from files in _includes
- sass/scss: css extension used by jekyll, supports variables, nesting, operators, etc.
- collection: group of documents, similar to a jekyll blog of posts but not organized by date (can be selected by config defaults)
- document: item in a collection

### SITE PLANNING
- features: responsive, sidebar menu, click images to enlarge, embedded twines/code bits, footer image?
- index: landing page with main menu
- topic menus: school + mobile projects, twine, html/css/js showcase, code templates and cheatsheets, coding resources
  - sort projects by class/type of code? p3, p5js, etc. with short explanations of each
- nav is the same as div, most navs (vertical and horizontal) seem to use ul's or div class="sidebar"
  - can show/hide with display:none (maybe more popular?) or width:0px
- footer is currently pushed down 1 screen size, so it's not visible upon load
  - footerimg doesn't show up in the correct place on mobile
- trying to figure out how to test on mobile
- CURRENT
  - working on overlay to close sidebar menu
  - can't transfer scss variable $sidebarwidth to js open/close functions

### DISCOVERIES / PROBLEMS SOLVED
- can't use $sidebarwidth to set content margin-left because the em's are based on different local font sizes, just use px
- sass can nest normal selectors (nav{ ul{} li{} }) and same prefix (font:{ family:; size:; })
  - but not .classes or a:selectors
- strange top gap was caused by header/paragraph/etc. margins
- when starting css, make sure to include a long page, it catches so many problems
- small gap under img is because img is inline, it's treated as text and sits on baseline
  - common fixes: display block, vertical-align bottom, container line-height 0%
- localhost bugs
  - sometimes command line does not auto refresh, ctrl+c to wake it up
  - if css changes are not showing up, ctrl + f5 to force reload, clearing cache and downloading latest version from server
  - (ctrl + shift + r may do same thing)
- css class styling showing up in inspector html but not in element css was caused by misplaced css {}'s

### BONUS NOTES
- if this is your first site, bundle add webrick before testing site locally
- info on filtering collection items https://jekyllrb.com/docs/step-by-step/09-collections/
- filter that allows liquid in front matter https://github.com/gemfarmer/jekyll-liquify
- sass nesting https://www.w3schools.com/sass/sass_nesting.asp
- sass numberics, ex: random https://www.w3schools.com/sass/sass_functions_numeric.php
- css image gallery https://www.w3schools.com/csS/css_image_gallery.asp
- referenced for footer at bottom of page https://stackoverflow.com/questions/18469262/position-footer-at-bottom-of-page-having-fixed-header

{% endraw %}
