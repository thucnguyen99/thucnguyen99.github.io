---
layout: post
title:  "Multiple languages for Jekyll and Github Pages!"
author: Raquel Peces
date: '2020-06-15 14:35:23 +0530'
category: 
        - jekyll
        - github pages
thumbnail: /assets/img/posts/ghpages_jekyll_multilang.png
---
In this post, I will explain how to add multi-languages to your Jekyll template in [Github Pages](github_pages).
To apply the multilingual feature, It is better to use some plugin, but Github does not support any other plugins with itself other than a few basic plugins for security reasons, you can find the supported plugins [here](jekyll_allowed_plugins). So we can have our page working locally, but throwing errors in the Github build process.
It might help us skip the build process of Github to push pages that have been generated on your local environment to the repository `master` branch, we can still control the versions of your Jekyll project by creating a new branch for you projects to be pushed.

## Installing jekyll-multiple-laguages plug-in

There are several ways to install [jekyll-multiple-languages](jekyll_multile_languages). If you need more info, you will find the full documentation in their project repository. They are looking for more maintainers!!!

### Using Ruby gem

What I have chosen is to use Ruby gem.
What you have to do is to add the following line to your Gemfile

```ruby
gem 'jekyll-multiple-languages-plugin'
```

Then go to root directory of your Jekyll project and execute the following command
```console
$ bundle install
```

Or install the gem by yourself as:
```console
$ gem install jekyll-multiple-languages-plugin
```

To activate the plugin add it to Jekyll _config.yml file, under the plugins option:
```yml
plugins:
  - jekyll-multiple-languages-plugin
```


### As a Git Submodule

In some cases, depending on the theme that I use, there may be issues related to the dependencies of gems. To avoid these issues you can add the plugin as a git submodule.
To install this plugin as a git submodule, go to root directory and execute:
```console
$ git submodule add git://github.com/screeninteraction/jekyll-multiple-languages-plugin.git _plugins/multiple-languages
```

To update:
```console
$ cd _plugins/multiple-languages
$ git pull origin master
```


## Setting _config.yml file

Add the languages available in your website into your `_config.yml`:

```yml
# Multi-Language config
languages: ["es", "en"]
default_lang: "es"
exclude_from_localizations: ["assets", "gallery", "_sass"]
```

If not default language, the first element of the language list will be used as the default one.
To avoid redundancy, it is possible to exclude files and folders from being copied to the localization folders. The usual folders to exclude will be the images or other common resources folder

## Folder Structure

Ya está todo configurado, es la hora de añadir la estructura de ficheros para construir nuestra página con los diferentes idiomas. 
In the Jekyll project without multiple-languages-plugin, Jekyll builds the `.md` files under the folder structure, in posts cases, it will by in `_posts` folder. However, if you install jekyll-multiple-languages-plugin, jekyll serve command will build the _posts folder under the _i18n directory.

Create a folder called _i18n and add sub-folders for each language, using the same names used on the languages setting on the configuration file:
It should look similar to this folder structure:

```
_i18n
│   en.yml
│   es.yml    
│
└───es
│   └───pagename
│       │   file111.txt
└───en
│   └───pagename
│   │   file111.txt
│   ...
```


## Setting language.yml

The language.yml files are written in YAML syntax which caters to a simple grouping of strings.
Those files have the sentences that we want to be translated, and configuration for each language. For example the navbar titles.
For example, we have Spanish and English YAML file:

###### es.yml

```yml
global:
  site_title: Raquel Fishes web
  site_description: Sitio Web de Raquel Fishes
langs:
  english: Ingles
  spanish: Español
  en: EN
  es: ES
navbar:
  about: Sobre mí
  contact: Contacto
  blog: Blog
```

###### en.yml

```yml
global:
  site_title: Raquel Fishes website
  site_description: Raquel Fishes personal page
langs:
  english: English
  spanish: Spanish
  en: EN
  es: ES
navbar:
  about: About me
  contact: Contact
  blog: Blog
```

## Visiting multiligual pages

La navegación por nuestra página multi-idioma va a añadir automáticamente a nuestra web la subextensión correspondiente al idioma en el que estemos navegando cuando no se trate del idioma por defecto.
The explorer links will look similar to:

###### Default language (Spanish)
```
raquelfishes.githug.io/about
localhost:4000/about
```

###### Other language (English)
```
raquelfishes.githug.io/en/about
localhost:4000/en/about
```

## Switching languages

Now that you got a multilingual feature, you might need a language switcher.
In my case, I have added flag icons at the navigation bar for switching between both languages.
This snippet will create a link that will toggle between Spanish and English.

{% highlight html%}
{% raw %}
<li class="nav-item">
  {% if site.lang == "es" %}
    {% capture link1 %}{{ site.baseurl_root }}/en{{ page.url }}{% endcapture %}
      <a href="{{ link1 }}" class="lang-switcher spanish" title="Website en español"><img src="en.webp"/>{% t global.en %}</a>
  {% elsif site.lang == "en" %}
    {% capture link2 %}{{ site.baseurl_root }}{{ page.url }}{% endcapture %}
      <a href="{{ link2 }}" class="lang-switcher english" title="English Website"><img src="es.webp"/>{% t global.es %}</a>
  {% endif %}
</li>
{% endraw %}
{% endhighlight%}

## Auto publish

This is the hardest point of this project. At this point, your web is working locally, but you cant publish it to Github Pages. Then, I will explain it step by step.

#### Create a branch and set to default

We are changing our default branch, just to store all our commits history in a different branch fro master. If you already work with a develop branch and other for production, you don't have to do extra work. If not, this is the moment for creating it.
Run these commands below in your local repository, in my project the history branch is `source`:

```
$ git checkout -b source master
$ git push -u origin source
```

And then, go to your Github repository, and configure this branch as the default project branch `Github web > your repository > Settings > Branches > Default branch`

#### Rakefile

If you had a previous Rake build file in your site, it probably looks similar to:

```ruby
namespace :assets do
  task :precompile do
    puts `bundle exec jekyll build`
  end
end
```

That build script, built the Jekyll project, but it won't wokr anymore, because Github does not support the multilanguage plugin. 
We need that the new script builds ourt site, copy the built page to our master branch and push it, avoiding Github to build it. 
Our new Rakefile will be as follow:

```ruby
require "jekyll"
require "tmpdir"
require "rubygems"

# Auto publish

# Change your GitHub reponame
GITHUB_REPONAME = "username/username.github.io"


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "git init"
    system "git config --local user.name username"
    system "git config --local user.email usermail"
    system "git add ."
	  message = "Site updated at #{Time.now.utc}"
	  system "git commit -m #{message.inspect}"
    system "git remote add origin https://github.com/#{GITHUB_REPONAME}.git"
    system "git push origin master --force"

    Dir.chdir pwd
  end
end
```
I have added the user and email local config. Just copy and paste the code in your file and it replace with your personal info and repository.
If there is no `Rakefile`, you can just create a new one and copy the code.


#### Run rake publish

The last step to publish our website in our repository `master` branch, and then can visit this page at the public site.
Now can easily execute the following command:
```console
$ rake publish
$ git push
```
or:
```console
$ bundle exec rake publish
$ git push
```
And push your full local repository, so it will synchronize local commits at development state.


## Finishing this topic...

I always wanted to have this website project with two languages. Spanish is my native language, and from my point of view like a computer engineer, we use to read all the technical documentation in English, I appreciate and want to contribute to find technical info in Spanish.
I have spent A LOT OF TIME to have this Jekyll project in Github to have both languages, searching in several places, and the problem was integrate with Github because of failed builds.
I hope this article and Spanish one help others to not lose so many time with this functionality...

=)


[github_pages]: https://pages.github.com/
[jekyll_allowed_plugins]: https://pages.github.com/versions/
[jekyll_multile_languages]: https://github.com/kurtsson/jekyll-multiple-languages-plugin