---
layout: post
title:  "Multiples Idiomas para Jekyll y Github Pages!"
author: Raquel Peces
date: '2020-08-13 14:35:23 +0530'
category: 
        - jekyll
        - github pages
thumbnail: /assets/img/posts/ghpages_jekyll_multilang.png
image: /assets/img/posts/ghpages_jekyll_multilang.png
---
En este post voy a explicar como añadir la funcionalidad de multi-idioma a tu plantilla de Jekyll usando [Github Pages](github_pages).
Para añadir esta funcionalidad a nuestra web lo mejor es usar uno de los plugins que existen, pero Github no soporta todos los plugins, en este [enlace](jekyll_allowed_plugins) podeis encontrar los plugins soportados en Github. Por lo que puede que tengamos nuestra página funcionando en local pero luego cuando subamos nuestra página cause errores de compilación durante el proceso de build. Un modo de conseguir que nuestra página funcione es saltarnos ese proceso de build y subiendo nuestra página ya compilada a la rama `master` de nuestro proyecto, y mantener el control de versiones en otra rama a parte.


## jekyll-multiple-laguages plug-in

Hay varios modos de instalar el plugin [jekyll-multiple-languages](jekyll_multile_languages). Si necesitáis más información podeis dirigiros al repositorio del proyecto. ¡Buscan colaboradores!

### Usando una gema de Ruby

En mi caso he elegido instalarlo a través de la gema de Ruby.
Para ello es necesario añadir la siguiente linea al archivo Gemfile

```ruby
gem 'jekyll-multiple-languages-plugin'
```

Una vez añadida la gema, hay que ejecutar:
```console
$ bundle install
```

O instalar la gema concreta:
```console
$ gem install jekyll-multiple-languages-plugin
```

Para activar el plugin añadirlo al fichero de Jekyll _config.yml, bajo la opcion de plugins:

```yml
plugins:
  - jekyll-multiple-languages-plugin
```


### Como un submodulo de Git

En algunos casos, dependiendo del tema que se use puede haber problemas con instalar el plugin como gema. Para evitar estos problemas se puede optar por añadir el plugin como submódulo. Para ello hay que dirigirse al directorio raíz del proyecto y ejecutar:
```console
$ git submodule add git://github.com/screeninteraction/jekyll-multiple-languages-plugin.git _plugins/multiple-languages
```


Para actualizarlo, cuando sea necesario habría que dirigirse a:
```console
$ cd _plugins/multiple-languages
$ git pull origin master
```


## Configuración del fichero _config.yml

Una vez instalado el plugin, hay que añadir los idiomas que queramos en nuestro fichero de configuracion `_config.yml`.

```yml
# Multi-Language config
languages: ["es", "en"]
default_lang: "es"
exclude_from_localizations: ["assets", "gallery", "_sass"]
```

También podemos especificar cual será nuestro idioma por defecto. En caso de no añadir esa variable se seleccionará por defecto el primero de la lista de idiomas.
Otra funcionalidad a tener cuenta es decir qué directorios no vamos a replicar por cada idioma, de este modo eliminaremos redundancias posibles y replicar ficheros que son iguales en todos los idiomas. Estos directorios serán aquellos en los que tengáis imágenes u otros recursos comunes.


## Estructura de directorios

Ya está todo configurado, es la hora de añadir la estructura de ficheros para construir nuestra página con los diferentes idiomas. 
En un proyecto de Jekyll sin multi-idioma, se compilan los ficheros `.md` sobre la estructura base, en el caso de los posts, sería bajo la carpeta `_posts`. En caso de tener multiples idiomas habría que crear ese directorio por cada idioma. Igual para cualquier fichero que cambiemos por idioma.

En primer lugar, en el directorio raíz hay que crear una carpeta con el nombre `_i18n` y añadir subcarpetas por cada uno de los idiomas usando los mismos nombres que hemos usado en nuestro fichero de configuración.
Vuestro directorio de ficheros debería añadir una estructura similar a esta:

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


## Configuracion idiomas.yml

Estos ficheros son a los que se llamara cuando queramos traducir un texto concreto. Por ejemplo, los textos del menú de navegación. 
Estos ficheros deberían ser similares a estos ejemplos:

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

## Navegar por paginas multi-idioma

La navegación por nuestra página multi-idioma va a añadir automáticamente a nuestra web la subextensión correspondiente al idioma en el que estemos navegando cuando no se trate del idioma por defecto.
Por lo que las direcciones que veremos en el explorador serán:

###### Idioma por defecto (Español)
```
raquelfishes.githug.io/about
localhost:4000/about
```

###### Pagina en otro idioma (Inglés)
```
raquelfishes.githug.io/en/about
localhost:4000/en/about
```

## Intercambio de idiomas

Si añadimos la funcionalidad de multi-idioma, también hay que añadir un botón de switch para cambiar entre idiomas. Eso lo puedes hacer de forma bastante sencilla.
En mi caso lo he añadido con iconos de idioma en la barra de navegación.


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

## Publicación automática

Este es el punto más controvertido de todo el desarrollo. Hasta aquí puedes tener tu web perfectamente funcional en local, pero que no puedas publicarla en Github Pages.
Así que vamos a ir paso a paso

#### Crear una rama y ponerla como default

En primer lugar vamos a cambiar nuestra rama principal, para guardar todo nuestro historial de código a una rama diferente a master. Puede que ya trabajes con una rama de desarrollo y otra de procucción, pero si no es así es el momento de crearla.
Ejecuta los siguientes comandos en tu repositorio en local, en mi caso mi rama para guardar el historial la he llamado `source`:

```
$ git checkout -b source master
$ git push -u origin source
```

Luego dirigete a tu repositorio de Github y configura esta rama recien creada como la rama por defecto del proyecto `Github web > your repository > Settings > Branches > Default branch`

#### Rakefile

Si ya tenías un fichero de compilación de Rake luciría similar a:

```ruby
namespace :assets do
  task :precompile do
    puts `bundle exec jekyll build`
  end
end
```

Simplemente compilaba como podemos compilar en nuestro local, pero eso ahora no funcionará porque Github no soporta el plugin que queremos que incorpore nuestro proyecto de Jekyll. Ahora nuestro fichero de Rake necesitamos que nos copie la página compilada ya a nuestra rama master y la suba tal cual, evitando que Github haga ese paso. Para ello nuestro fichero de compilación será:

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
En mi caso además he añadido la configuración de usuario y email. Simplemente copia y pega este código en tu fichero y reemplaza con tu usuario y repositorio.

Si no tienes un fichero `Rakefile` simplemente crea uno y copia el código


#### Ejecutar rake publish

Como último paso para publicar nuestra web en la rama `master` de nuestro repositori y que así seá la web que queremos que esté en producción.
Simplemente ejecuta el comando:
```console
$ rake publish
$ git push
```
o también:
```console
$ bundle exec rake publish
$ git push
```
Y haz push de tu proyecto completo, así sincronizaras los commits que también tengas en la rama de desarrollo.


## Para cerrar el tema...

La verdad es que desde el principio he querido tener esta web en dos idiomas. Mi lengua principal es el Español y considero que aunque como personas técnicas estamos acostumbrados a buscar todo en inglés, siempre se agradece encontrar documentación en tu propio idioma. 
He invertido bastante tiempo en conseguir configurar Jekyll en Github para poder tener ambos idiomas, buscando en muchos sitios, y el problema siempre llegaba a la hora de subirlo a Github... porque fallaba la build. 
Espero que este artículo así como su correspondiente también en inglés ayuden a otros a no perder tanto tiempo en esta funcionalidad... 

=)


[github_pages]: https://pages.github.com/
[jekyll_allowed_plugins]: https://pages.github.com/versions/
[jekyll_multile_languages]: https://github.com/kurtsson/jekyll-multiple-languages-plugin