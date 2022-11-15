## JEKYLL SITE NOTES
- attempt #3: followed jekyll tutorial again https://jekyllrb.com/docs/step-by-step/01-setup/
- satisfying success B^)

## TEST SITE LOCALLY
- http://localhost:4000/jekyll-boogaloo/
- bundle exec jekyll serve
- bundle exec jekyll serve --livereload

## JEKYLL
- prefix all commands with "bundle exec" to ensure correct jekyll version
- to use variables, metadata (ex: title), and liquid, add front matter to any markdown or html file
- published site url vs baseurl help https://mademistakes.com/mastering-jekyll/site-url-baseurl/
  - both are site-wide variables set in config, do not include trailing /'s
  - url: site's full url (https://makena-s.github.io)
  - baseurl: subdirectory the site is served from (/webbed-site), recommended for subdomain sites like github project sites
  - relative url filter: prepends baseurl config value {{ "/category/page.html" | relative_url }}

## MARKDOWN
- markdown guide https://itsfoss.com/markdown-guide/
  - line break: 2 spaces after line + enter
  - new paragraph: enter x2
- using html tags in markdown is encouraged https://daringfireball.net/projects/markdown/syntax#html
  - inline can be used anywhere
  - block-level elements (ex: div, table, p) must be at root level and surrounded by a blank line on top and bottom

## SITE PLANNING
- no posts or prodbuild nonsense, just normal + collection pages
- features: responsive, sidebar menu, click images to enlarge, embedded twines/code bits, footer image?
- index: landing page with main menu
- topic menus: school + mobile projects, twine, html/css/js showcase, code templates, jekyll notes, coding resources
  - sort projects by class/type of code? p3, p5js, etc. with short explanations of each

## DATA LOCATIONS
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

## JEKYLL GLOSSARY
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
- YAML: common ruby file format, stores data
- layout: html template that wraps around markdown page content, can be used by any page
  - you can call front matter in your layout file, it will use the front matter of the page the layout is called on
- layout inheritance: a layout can be wrapped in another layout
- {{ content }}: object used in layouts, a special variable that returns the rendered content of the page the layout is called on
- {% include name.html %}: tag used in layouts, includes content from files in _includes
- sass: css extension used by jekyll, supports variables, nesting, operators, etc.
- collection: group of documents, similar to a jekyll blog of posts but not organized by date
- document: item in a collection

## BONUS NOTES
- if this is your first site, bundle add webrick before testing site locally
- info on filtering collection items https://jekyllrb.com/docs/step-by-step/09-collections/
