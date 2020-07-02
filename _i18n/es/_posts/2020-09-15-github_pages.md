---
layout: post
title:  "¡Crea tu web gratis con Github Pages!"
summary: Cómo empezar con Github Pages, la forma más rápida, increible y gratis de crear tu blog o web.
author: Raquel Peces
date: '2020-08-08 14:35:23 +0530'
category: 
        - jekyll
        - github pages
thumbnail: /assets/img/posts/ghpages.png
image: /assets/img/posts/ghpages.png
---
<blockquote>
<p>Github Pages permite convertir cualquier repositorio en una página web con solo un par de clicks.</p>
</blockquote>

Si estás buscando un lugar en el que crear tu portfolio con proyectos personales o de trabajo, o si quieres crear tu blog o web de empresa y no sabes por donde empezar, quizá este sea tu sitio. Es probable que no quieras pagar por un servicio de hosting, dominio y todo lo que implica tener tu web "en el aire". Entonces sigue leyendo.

### ¿Por qué debería tener una web?

La verdad es que en el mundo en el que vivimos, es difícil imaginar que podría no beneficiarte de tener tu propia web. Puedes querer mostrar tu portfolio a futuras empresas o como freelance. Mostrar tus proyectos de estudiante y compartirlos con la comunidad universitaria Puedes querer tener tu propio blog donde contar los lugares que te gustan o qué estás haciendo. También puedes querer hacer publicidad o compartir tu negocio y abrirte a la venta online...

Una página web es el modo de conectarte con el mundo y una gran herramienta de comunicación. Es el modo de crear, construir y controlar tu imagen online. Además cuanto menos tiempo gastes en consstruir esa web, más tiempo tendrás para construir tu imagen y llegar a la gente que te interesa. Una web, puede ayudarte a alcanzar y superar a tus competidores.

Y, todos sabemos que no es lo más sencillo de crear si no sabes lo que estás haciendo.

Si estás empezando a informarte sobre como crear tu propia web, seguro que has oído hablar de algunas de las opciones mas sencillas, por un lado está Wordpress, pero yo quiero presentarte a Github.

Wordpress es la herramienta para principiantes por excelencia, para los que sólo quieren configurar algunos parámetros y escribir. Es una gran herramienta para las personas que quieren una web rápida sin tener ningún conocimiento técnico. El problema con Wordpress es que su plan gratuito no te deja configurar prácticamente nada. Es demasiado obvio que estamos usando Wordpress en nuestra página, tienes el logo de wordpress en todas las páginas, la direccion acaba con wordpress.com y las plantillas y personalización es mínima.

Si eres una persona un poco técnica seguro que conocerás Github como gestor de repositorio de código. Si eres una persona técnica que le gusta programar y tener sus proyectos en un mismo sitio seguro que tienes una cuenta de Github, con al menos un proyecto.
Lo que puede que no conozcas es la funcionalidad de Github Pages, por qué no crear tu web en Github y alojarla directamente ahí, en tu repositorio, sin necesitar nada más.

Si quieres mantener el código de tu web en secreto, quizá este artículo debería acabar aquí para ti. Si por el contrario te gusta colaborar con la filosofía de Código Libre y ayudar e inspirar a todos los que vengan detrás de ti. Esa es la gran idea de Github, compartir tu conocimiento y trabajo. Cuando tu compartes tus proyectos en Github, la gente puede ver tu código, ver qué haces y cómo lo haces, e incluso sugerirte mejoras. Sería la gran biblioteca del código hoy en día. 
La mayoría de las personas técnicas ya usan Git y/o Github de algún modo. Tener tu web en el mismo sitio es un plus, y además ayudará a subir las contribuciones en tu perfil =)

Si eres totalmente nuevo a todo lo que estoy contando, quizá deberías echar un vistazo a "Comenzar con Git y Github: Guía completa para novatos" En ese artículo puedes aprender lo básico de Git y Github, conceptos como "repositorio" o "rama". De aquí en adelante asumiré que conoces lo básico.


### Empecemos con nuestra web

Hay dos modos de empezar tu página web. Puede que comiences totalmente desde cero, no tienes nada, ni index.hmtl. O puedes tener una web o plantilla html ya creada, pero no sabes como subirla a Github y así poder tenerla online de forma gratuita.

### Ya tengo los ficheros de mi web, pero no sé qué hacer con ellos

Este es el caso más sencillo. Github hace todo el trabajo por ti. Asumiendo que ya tienes una cuenta de Github y que sabes lo que es un repositorio, sino, deberías echar un vistazo a mi anterior artículo sobre como empezar con Git y Github.

Digamos que nuestro repositorio será como el cascarón de un huevo, es donde nuestro proyecto vivie. Ahí puedes organizarlo por carpetas, añadir imagenes, videos, cualquier cosa que tu proyecto necesite puede estar en el repositorio.

Si todavía no lo has hecho, inicializa tu proyecto con un repositorio, o puedes crear un repositorio y añadir tus ficheros. Si en el directorio raíz ya tienes un fichero llamado `index.html` Github sabrá perfectamente qué hacer.

Ahora vas a aprender a aprovecharte de Github Pages. Tienes que ir a tu repositorio de Github y hacer click en `Settings`
![github settings](/assets/img/posts/gh_settings.png){:class="img-fluid"}

Una vez que estamos en la página de configuración hay que hacer scroll en la página hacia abajo hasta llegar a la seccion de `Github Pages`
![github pages](/assets/img/posts/gh_settings_pages.png){:class="img-fluid"}

Ahora desplega el menú de `Source` y selecciona la opción de `Master branch`. Esto hará que nuestra página tome como rama para mostrar nuestra página principal la rama master del repositorio, que sería como la rama principal por defecto del repositorio.
![github pages source](/assets/img/posts/gh_settings_pages_source.png){:class="img-fluid"}

En este caso verás una notificacion como que tu sitio está listo para ser publicado.
![github publishing](/assets/img/posts/gh_settings_publishing.png){:class="img-fluid"}

Sé paciente, puede tomar un par de minutos, entonces refresca la página y verás que la notificación ha cambiado y te dice que tu página ya ha sido publicada con la direccion web en la que podrás ver tu página.
![github published](/assets/img/posts/gh_settings_published.png){:class="img-fluid"}

Prueba a hacer click en el link y ¡MAGIA!

¡¡Ya tienes tu web gratis publicada!!


### No sé ni por donde empezar

No voy a explicar como hacer una web, ni las diferentes librerias de diseño que puedes usar, sino que me voy a enfocar en lo básico.
Prefiero que conozcas como crear algo de cero usando la herramienta que estoy presentando aquí y que con todo el tiempo que dispongas y las ganas que le pongas explores todo este mundo de diseño y programación web. Lo que voy a explicar aquí es como si eres totalmente nuevo crear una web en Github Pages.
Lo primero vamos a crear un repositorio
![github repository](/assets/img/posts/gh_new_repo.png){:class="img-fluid"}

Rellena los datos de tu repositorio, nombre, descripcion y selecciona la opción de inicializiar el repositorio con un README `Initialize this repository with a README` y entonces dile que lo cree `Create repository`
![github create](/assets/img/posts/gh_create_repo.png){:class="img-fluid"}

Ahora al igual que en la sección anterior tienes que ir a `Settings`, cerca de la parte alta de la página al lado derecho de la pantalla
![github settings](/assets/img/posts/gh_settings.png){:class="img-fluid"}

Una vez que estés aquí, haz scroll en la página hacia abajo hasta llegar a la sección de `Github Pages`
![github pages](/assets/img/posts/gh_settings_pages.png){:class="img-fluid"}

Ahora desplega el menú de `Source` y selecciona la opción de `Master branch`. Esto hará que nuestra página tome como rama para mostrar nuestra página principal la rama master del repositorio, que sería como la rama principal por defecto del repositorio.
![github pages source](/assets/img/posts/gh_settings_pages_source.png){:class="img-fluid"}

En este caso verás una notificacion como que tu sitio está listo para ser publicado.
![github publishing](/assets/img/posts/gh_settings_publishing.png){:class="img-fluid"}

Sé paciente, puede tomar un par de minutos, entonces refresca la página y verás que la notificación ha cambiado y te dice que tu página ya ha sido publicada con la direccion web en la que podrás ver tu página.
![github published](/assets/img/posts/gh_settings_published.png){:class="img-fluid"}

Ahora haz click en el link y podrás ver tu página.
![github web](/assets/img/posts/gh_basic_web.png){:class="img-fluid"}

¡Enhorabuena! ¡Ya estás online!


### ¿Pero esto no es un poco feo?

Te doy la razón, esta web es un poco bastante fea, si vuelves a tu repositorio podrás er que lo que se está mostrando es lo que hay en tu fichero `README.md`.
![github readme](/assets/img/posts/gh_readme.png){:class="img-fluid"}

Si quieres hacer algunos cambios, puedes ir a la parte de arriba y editar tu fichero, para editar lo que quieres que la gente vea. Para hacer esto, vuelve al repositorio, haz click en el icono del lapiz que puedes encontrar en el fichero README y modíficalo a tu antojo.
![github edit readme](/assets/img/posts/gh_edit_readme.png){:class="img-fluid"}

Ten en cuenta que estás modificando un fichero de tipo Markdown. Si no sabes mucho sobre este formato, puedes dirigirte a este [enlace](https://www.markdownguide.org/getting-started/) para ver la de opciones que te ofrece.


Este tipo de ficheros es en realidad un lenguaje de programación, este post está escrito en formato Markdown, donde puedes añadir el formato de los elementos mientras escribes en texto plano. Incluye funcionalidades para añadir texto, lins, imágenes, colores e incluso formato de código. Aquí puedes encontrar la [Guía Gásica de la sintaxis de Markdown](https://www.markdownguide.org/basic-syntax/)

¡Ahora vuelve a tu web, y comprueba como queda con los últimos cambios!
![github web2](/assets/img/posts/gh_basic_web2.png){:class="img-fluid"}

Ten en cuenta que a veces puede tomar varios minutos hasta que los cambios aparecen en la web publicada. También puedes tener algunos problemas con la cache de tu navegador, borrar la cache del navegador o abrir el enlace en un navegador con sesión oculta puede ayudar a ver los cambios antes.


### ¿No se puede hacer nada mejor?

Pues sí, sí se puede hacer mejor, a partir de aquí se pone interesante. Pero eso lo explicaré en otro post en el que os presentare Jekyll, framework con el que he creado yo esta página.
Mientras espero que este tutorial os haya servido para abrir el apetito.

=)
