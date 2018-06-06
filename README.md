[![Gem Version](https://badge.fury.io/rb/jekyll-plantastisch.svg)](https://badge.fury.io/rb/jekyll-plantastisch)

# Jekyll Plantastisch
> "Ein fantastischer PlantUML plugin!"

`jekyll-plantastisch` is a PlantUML jekyll plugin with several 
distinguishable features:

- It uses `<object>` html tag instead of `<img>` tag, when embedding 
  rendered diagrams on page. 

  This allows you to use interactive SVG 
  diagrams with links (see [PlantUML docs on this][plantuml_links]).

- It requires you to put `@startuml` and `@enduml` tags into the
  source of your diagram instead of forcibly inserting them. 

  This enables you to store the diagram's source in a completely
  separate file in `_includes` directory and reuse it in several
  places, while simply embedding it, when required:
  ```jekyll
  {% plantuml %}
  {% include diagram.uml %}
  {% endplantuml %}
  ```

## Install Jekyll plugin

Install it first:

```
gem install jekyll-plantuml
```

With Jekyll 2, simply add the gem to your `_config.yml` gems list:

```yaml
gems: ['jekyll-plantuml', ... your other plugins]
```

Or for previous versions,
create a plugin file within your Jekyll project's `_plugins` directory:

```ruby
# _plugins/plantuml-plugin.rb
require "jekyll-plantuml"
```

Highly recommend to use Bundler. If you're using it, add this line
to your `Gemfile`:

```
gem "jekyll-plantuml"
```

## Install plantuml.jar

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
