---
layout: post
title:  "Multiples Idiomas para Jekyll y Github Pages!"
author: Raquel Peces
date: '2020-06-15 14:35:23 +0530'
category: jekyll
thumbnail: /assets/img/posts/code.jpg
---
En este post voy a explicar como he conseguido hacer fu



## jekyll-multiple-laguages plug-in

Hay varios modos de instalar el plugin jekyll-multiple-languages. 

### Usando una gema de Ruby

En mi caso he elegido instalarlo a través de la gema de Ruby.
Para ello es necesario añadir la siguiente linea al archivo Gemfile

{% highlight ruby %}
gem 'jekyll-multiple-languages-plugin'
{% endhighlight %}

Una vez añadida la gema, hay que ejecutar:
`$ bundle install`

O instalar la gema concreta:
`$ gem install jekyll-multiple-languages-plugin`

Para activar el plugin añadirlo al fichero de Jekyll _config.yml, bajo la opcion de plugins:

{% highlight ruby %}
plugins:
  - jekyll-multiple-languages-plugin
{% endhighlight %}


### Como un submodulo de Git

En algunos casos, dependiendo del tema que se use puede haber problemas con instalar el plugin como gema. Para evitar estos problemas se puede optar por añadir el plugin como submodulo. Para ello hay que dirigirse al directorio raíz del proyecto y ejecutar:
`$ git submodule add git://github.com/screeninteraction/jekyll-multiple-languages-plugin.git _plugins/multiple-languages`

Para actualizarlo, cuando sea necesario habría que dirigirse a:
`$ cd _plugins/multiple-languages`
`$ git pull origin master`


## Configuración _config.yml file


## Estructura de directorios


## Configuracion idiomas.yml


## Navegar por paginas multi-idioma


## Publicación automática