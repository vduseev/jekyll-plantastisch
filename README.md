[![Gem Version](https://badge.fury.io/rb/jekyll-plantastisch.svg)](https://badge.fury.io/rb/jekyll-plantastisch)

# Jekyll Plantastisch
> "Ein fantastischer PlantUML plugin!"

## Description

`jekyll-plantastisch` is a **PlantUML** Jekyll plugin with several 
distinguishable features:

- It uses `<object>` html tag instead of `<img>` tag, when embedding 
  rendered diagrams on page. 

  This allows you to use interactive SVG 
  diagrams with links (see [PlantUML docs on this][plantuml_links]).

- It requires you to put `@startuml` and `@enduml` tags into the
  source of your diagram instead of forcibly inserting them. 

  This was an issue with `jekyll-plantuml` plugin, because it
  automatically adds these keywords to any content wrapped in a
  `{% plantuml %}` tag.

  Not having this enables you to store the diagram's source in a completely
  separate file in `_includes` directory and reuse it in several
  places, while simply embedding it, when required.

## Usage

<table style="width:100%">
  <tr>
    <th>Example</th>
    <th>Output</th>
  </tr>
  <tr>
    <td>
<pre>
{% plantuml %}
@startuml
class "[[https://www.nypl.org/ Foo]]" as foo
note left of foo
  This is <u>riabrary</u>
  This is [[https://github.com link]]
  <img:https://image.ibb.co/e6KstT/thislibrarrrr.jpg>
end note
@enduml
</pre>
    </td>
    <td>
      <img src="https://image.ibb.co/fz60f8/jekyll_plantastisch_output.jpg">
    </td>
  </tr>
  <tr>
    <td>
<pre>
{% plantuml %}
{% include diagram.uml %}
{% endplantuml %}
</pre>
    </td>
    <td>
      <img src="https://image.ibb.co/fz60f8/jekyll_plantastisch_output.jpg">
    </td>
  </tr>
</table>

`WARNING`: this plugin is not compatible with **Github Pages**, because it's
a custom plugin and it is not included into the default `github-pages`
bundle.
If you want to use this plugin with GitHub Pages you will need to generate
the `_site` directory locally and push its contents to GitHub rather than
pushing website sources to GitHub to have it build and render them for you.

## Installation

### Jekyll `3.7` and above

Add this line to your `Gemfile` to the `group :jekyll_plugins do` section.
```ruby
group :jekyll_plugins do
  gem "jekyll-plantastisch"
end
```

Add plugin to the `_config.yml`
```yaml
plugins:
  - jekyll-plantastisch
```

Run `bundle install` or `bundle update`
```console
bundle install
```

### Previous versions

Install it first:
```console
gem install jekyll-plantastisch
```

With Jekyll 2, simply add the gem to your `_config.yml` gems list:
```yaml
gems: ['jekyll-plantastisch', ... your other plugins]
```

Or for previous versions,
create a plugin file within your Jekyll project's `_plugins` directory:
```ruby
# _plugins/plantuml-plugin.rb
require "jekyll-plantastisch"
```

## Installing plantuml.jar

Then, make sure [PlantUML](http://plantuml.sourceforge.net/download.html)
is installed on your build machine, and can
be executed with a simple `plantuml` command.

For Linux user, you could create a `/usr/bin/plantuml` with contents:

```
#!/bin/bash

java -jar /home/user/Downloads/plantuml.jar "$1" "$2"
```

Remember to change the path to `plantuml.jar` file.

Then set executable permission.

```
chmod +x /usr/bin/plantuml
```

## Test

Now, it's time to create a diagram, in your Jekyll blog page:

```
{% plantuml %}
@startuml
[First] - [Second]
@enduml
{% endplantuml %}
```

[plantuml_links]: http://plantuml.com/link
