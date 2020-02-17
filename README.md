# minima

*Minima is a one-size-fits-all Jekyll theme for writers*. It's Jekyll's default (and first) theme. It's what you get when you run `jekyll new`.

***Disclaimer:** The information here may vary depending on the version you're using. Please refer to the `README.md` bundled
within the theme-gem for information specific to your version or by pointing your browser to the Git tag corresponding to your
version. e.g. https://github.com/jekyll/minima/blob/v2.5.0/README.md*  
*Running `bundle show minima` will provide you with the local path to your current theme version.*


[Theme preview](https://jekyll.github.io/minima/)

![minima theme preview](/screenshot.png)

## Installation

Add this line to your Jekyll site's Gemfile:

```ruby
gem "minima"
```

And then execute:

    $ bundle


## Contents At-A-Glance

Minima has been scaffolded by the `jekyll new-theme` command and therefore has all the necessary files and directories to have a new Jekyll site up and running with zero-configuration.

### Layouts

Refers to files within the `_layouts` directory, that define the markup for your theme.

  - `default.html` &mdash; The base layout that lays the foundation for subsequent layouts. The derived layouts inject their contents into this file at the line that says ` {{ content }} ` and are linked to this file via [FrontMatter](https://jekyllrb.com/docs/frontmatter/) declaration `layout: default`.
  - `home.html` &mdash; The layout for your landing-page / home-page / index-page. [[More Info.](#home-layout)]
  - `page.html` &mdash; The layout for your documents that contain FrontMatter, but are not posts.
  - `post.html` &mdash; The layout for your posts.

#### Home Layout

`home.html` is a flexible HTML layout for the site's landing-page / home-page / index-page. <br/>

##### *Main Heading and Content-injection*

From Minima v2.2 onwards, the *home* layout will inject all content from your `index.md` / `index.html` **before** the **`Posts`** heading. This will allow you to include non-posts related content to be published on the landing page under a dedicated heading. *We recommended that you title this section with a Heading2 (`##`)*.

Usually the `site.title` itself would suffice as the implicit 'main-title' for a landing-page. But, if your landing-page would like a heading to be explicitly displayed, then simply define a `title` variable in the document's front matter and it will be rendered with an `<h1>` tag.

##### *Post Listing*

This section is optional from Minima v2.2 onwards.<br/>
It will be automatically included only when your site contains one or more valid posts or drafts (if the site is configured to `show_drafts`).

The title for this section is `Posts` by default and rendered with an `<h2>` tag. You can customize this heading by defining a `list_title` variable in the document's front matter.


### Includes

Refers to snippets of code within the `_includes` directory that can be inserted in multiple layouts (and another include-file as well) within the same theme-gem.

  - `disqus_comments.html` &mdash; Code to markup disqus comment box.
  - `footer.html` &mdash; Defines the site's footer section.
  - `google-analytics.html` &mdash; Inserts Google Analytics module (active only in production environment).
  - `head.html` &mdash; Code-block that defines the `<head></head>` in *default* layout.
  - `custom-head.html` &mdash; Placeholder to allow users to add more metadata to `<head />`.
  - `header.html` &mdash; Defines the site's main header section. By default, pages with a defined `title` attribute will have links displayed here.
  - `social.html` &mdash; Renders social-media icons based on the data provided in a (configurable) data file at source.


### Sass

Refers to `.scss` files within the `_sass` directory that define the theme's styles.

  - `minima-classic.scss` &mdash; The core file imported by preprocessed `css/style.scss`, it defines the variable defaults for
    the "classic" skin of the theme.
  - `minima/initialize.scss` &mdash; A component that defines the theme's *skin-agnostic* variable defaults and sass partials.
  - `minima/custom-variables.scss` &mdash; A hook that allows overriding variable defaults and mixins. (*Note: Cannot override styles*)
  - `minima/custom-styles.scss` &mdash; A hook that allows overriding styles. (*Note: Cannot override variables*)
  - `minima/_base.scss` &mdash; Sass partial for resets and defines base styles for various HTML elements.
  - `minima/_layout.scss` &mdash; Sass partial that defines the visual style for various layouts.

Refer the [skins](#skins) section for more details.


### Assets

Refers to various asset files within the `assets` directory.

  - `css/style.scss` &mdash; This imports Sass files from within the `_sass` directory gets processed into the theme's main
    stylesheet `style.css` called by `_layouts/default.html` via `_includes/head.html`.
  - `minima-social-icons.svg` &mdash; An SVG file that contains various social media icons in alphabetic order of their
    respective `id` attribute. Used to render social icons via `_includes/social.html`.

This directory can include sub-directories to manage assets of similar type (`img`, `fonts`, `svg`), and will be copied over as
is, to the final transformed site directory.


### Plugins

Minima comes with [`jekyll-seo-tag`](https://github.com/jekyll/jekyll-seo-tag) plugin preinstalled to make sure your website gets the most useful meta tags. See [usage](https://github.com/jekyll/jekyll-seo-tag#usage) to know how to set it up.


## Usage

Have the following line in your config file:

```yaml
theme: minima
```


### Customizing templates

To override the default structure and style of minima, simply create the concerned directory at the root of your site, copy the file you wish to customize to that directory, and then edit the file.
e.g., to override the [`_includes/head.html `](_includes/head.html) file to specify a custom style path, create an `_includes` directory, copy `_includes/head.html` from minima gem folder to `<yoursite>/_includes` and start editing that file.

The site's default CSS has now moved to a new place within the gem itself, [`assets/css/style.scss`](assets/css/style.scss).

In Minima 3.0, if you only need to customize the colors of the theme, refer to the subsequent section on skins. To have your
*CSS overrides* in sync with upstream changes released in future versions, you can collect all your overrides for the Sass
variables and mixins inside a sass file placed at `_sass/minima/custom-variables.scss` and all other overrides inside a sass file
placed at path `_sass/minima/custom.scss`.

You need not maintain entire partial(s) at the site's source just to override a few styles.

#### Skins

Minima 3.0 supports defining and switching between multiple color-palettes (or *skins*).

```
.
├── minima.scss
└── minima
    └── _syntax-highlighting.scss
```


A skin is a Sass file named in the format `minima-*` and is the core file imported by the `assets/css/style.scss`. It defines the
variable defaults related to the "color" aspect of the theme and imports two components:

  - `minima/initialize.scss` &mdash; Defines the theme's *skin-agnostic* variable defaults and sass partials for styles.
  - `minima/custom-styles.scss` &mdash; A hook for overriding the predefined styles. (*Note: Cannot override variables*)

A skin also embeds the Sass rules related to syntax-highlighting since that is primarily related to color and has to be adjusted
in harmony with the current skin.

The default color palette for Minima is defined within `_sass/minima-classic.scss`. To switch to another available skin, simply
declare it in the site's config file. For example, to activate `_sass/minima-sunrise.scss` as the skin, the setting would be:

```yaml
minima:
  skin: sunrise
```

As part of the migration to support skins, some existing Sass variables have been retired and some **have been redefined** as
summarized in the following table:

Minima 2.0      | Minima 3.0
--------------- | ----------
`$brand-color`  | `$link-base-color`
`$grey-*`       | `$brand-*`
`$orange-color` | *has been removed*


### Customize navigation links

This allows you to set which pages you want to appear in the navigation area and configure order of the links.

For instance, to only link to the `about` and the `portfolio` page, add the following to your `_config.yml`:

```yaml
header_pages:
  - about.md
  - portfolio.md
```


### Change default date format

You can change the default date format by specifying `site.minima.date_format`
in `_config.yml`.

```
# Minima date format
# refer to http://shopify.github.io/liquid/filters/date/ if you want to customize this
minima:
  date_format: "%b %-d, %Y"
```


### Extending the `<head />`

You can *add* custom metadata to the `<head />` of your layouts by creating a file `_includes/custom-head.html` in your source directory. For example, to add favicons:

1. Head over to [https://realfavicongenerator.net/](https://realfavicongenerator.net/) to add your own favicons.
2. [Customize](#customization) default `_includes/custom-head.html` in your source directory and insert the given code snippet.


### Enabling comments (via Disqus)

Optionally, if you have a Disqus account, you can tell Jekyll to use it to show a comments section below each post.

To enable it, add the following lines to your Jekyll site:

```yaml
  disqus:
    shortname: my_disqus_shortname
```

You can find out more about Disqus' shortnames [here](https://help.disqus.com/installation/whats-a-shortname).

Comments are enabled by default and will only appear in production, i.e., `JEKYLL_ENV=production`

If you don't want to display comments for a particular post you can disable them by adding `comments: false` to that post's YAML Front Matter.

:warning: `url`, e.g. `https://example.com`, must be set in you config file for Disqus to work.

### Author Metadata

From `Minima-3.0` onwards, `site.author` is expected to be a mapping of attributes instead of a simple scalar value:

```yaml
author:
  name: John Smith
  email: "john.smith@foobar.com"
```

To migrate existing metadata, update your config file and any reference to the object in your layouts and includes as summarized below:

Minima 2.x    | Minima 3.0
------------- | -------------------
`site.author` | `site.author.name`
`site.email`  | `site.author.email`


### Social networks

You can add links to the accounts you have on other sites, with respective icon. From `Minima-3.0` onwards, the theme yields
the users with greater control over rendering a social-icon.

Users are now expected to provide necessary details in a data file instead of using the config file. By default, Minima looks
for social information in a datafile named `social_media` (of any data type supported by Jekyll). In the event that your site
uses the said file for a different purpose, you can configure a different filename via `minima.social_datafile` in your site's
config file:

```yaml
# _config.yml

minima:
  social_datafile: "my-social-media-details"
```

However, the data provided should comply with the following pattern:

```yaml
- id: github
  base: "https://github.com/"
  username: "jekyll/minima"

- id: twitter
  base: "https://twitter.com/"
  username: jekyllrb

- id: rss
  feed_path: feed.xml
```

- The data comprises of a list of social entries. The order of entries is up to your preference.
- Icons can be repeated if desired.
- key `id` should be one of existing `<symbol id>` in `assets/minima-social-icons.svg`.
- keys `base` and `username` jointly yields the icon's link reference. Minima no longer escapes invalid HTML sequences.
- Feed entries generate link reference for given `feed_path`. Internally, the final link is prepended with `site.baseurl`.
- [Optional] key `title` generates the title attribute for the link. Defaults to the value of `id`.



### Enabling Google Analytics

To enable Google Analytics, add the following lines to your Jekyll site:

```yaml
  google_analytics: UA-NNNNNNNN-N
```

Google Analytics will only appear in production, i.e., `JEKYLL_ENV=production`

### Enabling Excerpts on the Home Page

To display post-excerpts on the Home Page, simply add the following to your `_config.yml`:

```yaml
show_excerpts: true
```


## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/jekyll/minima. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## Development

To set up your environment to develop this theme, run `script/bootstrap`.

To test your theme, run `script/server` (or `bundle exec jekyll serve`) and open your browser at `http://localhost:4000`. This starts a Jekyll server using your theme and the contents. As you make modifications, your site will regenerate and you should see the changes in the browser after a refresh.

## License

The theme is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
