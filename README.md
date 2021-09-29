
# ¿Qué es Webpack?
**Webpack** es un module bundler que nos permite trabajar con una variedad de tecnologías web empezando desde HTML y terminando con JS. Además de tener soporte para archivos estáticos

**Module bundlers** son herramientas de frontend que nos permiten usar archivos con módulos JavaScript, entre otras características y convertiros a un JavaScript el cual el navegador pueda entender

Webpack es una herramienta que nos permite preparar nuestro código para llevarlo a producción (module bundler)
Webpack nos permite trabajar con:
* HTML
* CSS
* JavaScript
* Archivos estáticos
* Imágenes
* Fuentes

Tambien nos permite tener un modo en desarrollo para nuestros proyectos para hacer pruebas
Nacio en el 2012, desde ese entonces varias empresas lo usan como ser
* Twitter
* Instagram
* PayPal

También nos permite
* Gestionar dependencias
* Ejecutar tareas
* Conversión de archivos

Nos permite trabajar en módulos
* Permitiéndonos tener un código separado en desarrollo, pero en producción en una fuente
* Webpack permite tener módulos de JS en formato
    * AMD
    * Common JS
    * ES15

# Conceptos Básicos Webpack
**Entry** (punto de entrada): este le indica a webpack cual modulo de JavaScript debe de usar para empezar a crear una salida.
Ejemplo : index.js. también podemos tener múltiples puntos de entrada pero eso es otra historia.

**Output** (punto de salida): Este archivo es el bundle o nuestro archivo de salida, seria nuestra caja donde empaquetamos toda nuestra aplicación, normalmente este archivo final se crea en una carpeta llamada dist

**Loader** (transformador): Los loaders lo que hacen es decirle a webpack como tiene que transformar el código de un modulo en concreto. Ejemplo : Los loaders pueden transformar ficheros a JavaScript, o cargar CSS directamente en archivos JS, (si usas reactjs ya sabrás como)

**Plugins** (complementos): Nos van a ayudar a extender las funcionalidades con los loaders, añadir otras configuraciones.
Ejemplo : hay un modulo llamado HTMLWebpackPlugin que este se encarga de crear un HTML personalizado que le inyecta todos los bundles finales que compilamos.

# Tu primer build con Webpack
Creamos una carpeta como le quieras llamar
(Bueno no! si eres de Windows te dejo este articulo cortito de los nombres de carpetas PROHIBIDOS )
La creamos desde la terminal con mkdir y luego entramos a ella con cd
```
mkdir curso-webpack
cd curso-webpack
```
una vez que entres a la carpeta inicializamos nuestro repositorio con git
```
git init
```
El paso que sigue es inicializar nuestro proyecto con npm y si no sabes de npm aqui esta el curso del profesor
```
npm init -y
```
o si les da error “Invalid Name” usen para personalizar la configuración
```
npm init
```
y para abrir el proyecto como flash es poner en la terminal y les abre el editor ( si usas VS CODE)
```
code .
```
La carpeta SRC es el source de todo el proyecto ( index.js , imágenes, utils, assets, helpers, database, etc).

**Instalación de Webpack**

si no quieres escribir ese comando también puedes usar este
la i de install
```
npm i webpack webpack-cli -D
```
o si usas yarn usa
```
yarn add webpack webpack-cli -D
```
Y luego ejecutamos webpack
npx lo que hace es ejecutar paquetes directamente de npm, este viene instalado de npm
```
npx webpack
```
Al hacer esto webpack creo una carpeta llamada dist, esto lo hace por defecto webpack sin preguntarnos.
Modo de desarrollo
Por defecto webpack al compilar nuestro proyecto setea el modo “production” implícitamente pero podemos definirle el modo explícitamente corriendo:
```
npx webpack --mode production
npx webpack --mode development
```
La diferencia radica que el modo development deja el código mas legible para los desarrolladores pero con comentarios, el modo production deja el código comprimido y mas limpio para usarse.

# Instalación de webpack y construcción del proyecto
Entendimos las bases de webpack pero ahora vamos a crear un proyecto que nos va a permitir trabajar con todas las particularidades que nos brinda webpack y preprarlo para mandarlo a produccion

* CSS
* Imágenes
* fonts
* optimización de código

El proyecto que realizaremos será un pequeño portafolio en el que podremos ver nuestra foto y nuestro nombre y redes sociales.

## Pasos de la clase
Clonar el proyecto
```
git clone https://github.com/gndx/js-portfolio.git
```
Instalar webpack
con npm
```
npm install webpack webpack-cli -D 
```
con Yarn
```
yarn add webpack webpack-cli -D 
```

# Configuración de webpack.config.js
Puedes crear un archivo webpack.config.js en el cual estarán las configuraciones con las cuales webpack trabajara, entre ellas están los puntos de entrada y salida, extensiones de archivos, entre otras características.

El archivo de configuración nos va ayudar a poder establecer la configuración y elementos que vamos a utilizar
Para poder crear el archivo de configuración en la raíz del proyecto creamos un archivo llamado ``webpack.config.js``
En el mismo debemos decir
* El punto de entrada
* Hacia a donde a enviar la configuración de nuestro proyecto
* Las extensiones que vamos usar
```
const path = require('path');

module.exports = {
  // Entry nos permite decir el punto de entrada de nuestra aplicación
  entry: "./src/index.js",
  // Output nos permite decir hacia dónde va enviar lo que va a preparar webpacks
  output: {
    // path es donde estará la carpeta donde se guardará los archivos
    // Con path.resolve podemos decir dónde va estar la carpeta y la ubicación del mismo
    path: path.resolve(__dirname, "dist"),
    // filename le pone el nombre al archivo final
    filename: "main.js"
  },
  resolve: {
    // Aqui ponemos las extensiones que tendremos en nuestro proyecto para webpack los lea
    extensions: [".js"]
  },
}
```
El flag ``—-config`` indica donde estará nuestro archivo de configuración
```
npx webpack --mode production --config webpack.config.js
```
Para poder hacerlo más amigable el comando puedes crear un script en ``package.json``
```js
"scripts": {
		...
    "build": "webpack --mode production --config webpack.config.js"
  },
```
# Babel Loader para JavaScript
Babel te ayuda a transpilar el código JavaScript, a un resultado el cual todos los navegadores lo puedan entender y ejecutar. Trae “extensiones” o plugins las cuales nos permiten tener características más allá del JavaScript común

Babel te permite hacer que tu código JavaScript sea compatible con todos los navegadores
Debes agregar a tu proyecto las siguientes dependencias

NPM
```
npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
```
Yarn
```
yarn add -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
```
* **babel-loader** nos permite usar babel con webpack
* **@babel/core** es babel en general
* **@babel/preset-env** trae y te permite usar las ultimas características de JavaScript
* **@babel/plugin-transform-runtime** te permite trabajar con todo el tema de asincronismo como ser ``async`` y ``await``
* Debes crear el archivo de configuración de babel el cual tiene como nombre ``.babelrc``
```js
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-transform-runtime"
  ]
}
```
Para comenzar a utilizar webpack debemos agregar la siguiente configuración en ``webpack.config.js``
```js
{
...,
module: {
    rules: [
      {
        // Test declara que extensión de archivos aplicara el loader
        test: /\.js$/,
        // Use es un arreglo u objeto donde dices que loader aplicaras
        use: {
          loader: "babel-loader"
        },
        // Exclude permite omitir archivos o carpetas especificas
        exclude: /node_modules/
      }
    ]
  }
}
```
# HTML en webpack
## HtmlWebpackPlugin
Es un plugin para inyectar javascript, css, favicons, y nos facilita la tarea de enlazar los bundles a nuestro template HTML.

Instalación
npm
```
npm i html-webpack-plugin -D
```
yarn
```
yarn add html-webpack-plugin -D
```
Al webpack config queda asi
```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'production', // LE INDICO EL MODO EXPLICITAMENTE
    entry: './src/index.js', // el punto de entrada de mi aplicación
    output: { // Esta es la salida de mi bundle
        path: path.resolve(__dirname, 'dist'),
        // resolve lo que hace es darnos la ruta absoluta de el S.O hasta nuestro archivo
        // para no tener conflictos entre Linux, Windows, etc
        filename: 'main.js', 
        // EL NOMBRE DEL ARCHIVO FINAL,
    },
    resolve: {
        extensions: ['.js'] // LOS ARCHIVOS QUE WEBPACK VA A LEER
    },
    module: {
        // REGLAS PARA TRABAJAR CON WEBPACK
        rules : [
            {
                test: /\.m?js$/, // LEE LOS ARCHIVOS CON EXTENSION .JS,
                exclude: /node_modules/, // IGNORA LOS MODULOS DE LA CARPETA
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    },
    // SECCION DE PLUGINS
    plugins: [
        new HtmlWebpackPlugin({ // CONFIGURACIÓN DEL PLUGIN
            inject: true, // INYECTA EL BUNDLE AL TEMPLATE HTML
            template: './public/index.html', // LA RUTA AL TEMPLATE HTML
            filename: './index.html' // NOMBRE FINAL DEL ARCHIVO
        })
    ]
}
```
# Loaders para CSS y preprocesadores de CSS
Puedes dar soporte a CSS en webpack mediante loaders y plugins, además que puedes dar superpoderes al mismo con las nuevas herramientas conocidas como pre procesadores y post procesadores

Un preprocesador CSS es un programa que te permite generar CSS a partir de la syntax única del preprocesador. Existen varios preprocesadores CSS de los cuales escoger, sin embargo, la mayoría de preprocesadores CSS añadirán algunas características que no existen en CSS puro, como variable, mixins, selectores anidados, entre otros. Estas características hacen la estructura de CSS más legible y fácil de mantener.

post procesadores son herramientas que procesan el CSS y lo transforman en una nueva hoja de CSS que le permiten optimizar y automatizar los estilos para los navegadores actuales.

Para dar soporte a CSS en webpack debes instalar los siguientes paquetes
Con npm
```
npm i mini-css-extract-plugin css-loader -D
```
Con yarn
```
yarn add mini-css-extract-plugin css-loader -D
```
* css-loader ⇒ Loader para reconocer CSS
* mini-css-extract-plugin ⇒ Extrae el CSS en archivos
* Para comenzar debemos agregar las configuraciones de webpack
```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
	...,
	module: {
    rules: [
      {
        test: /\.(css|styl)$/i,
        use: [
          MiniCssExtractPlugin.loader,
          "css-loader",
        ]
      }
    ]
  },
  plugins: [
		...
    new MiniCssExtractPlugin(),
  ]
}
```
Si deseamos posteriormente podemos agregar herramientas poderosas de CSS como ser:
* pre procesadores
    * Sass
    * Less
    * Stylus
* post procesadores
    * Post CSS

# Copia de archivos con Webpack
Si tienes la necesidad de mover un archivo o directorio a tu proyecto final podemos usar un plugin llamado “copy-webpack-plugin”
Para instalarlo debemos ejecutar el comando
Para npm
```
npm i copy-webpack-plugin -D
```
Para yarn
```
yarn add copy-webpack-plugin -D
```
Para poder comenzar a usarlo debemos agregar estas configuraciones a ``webpack.config.js``

const CopyPlugin = require('copy-webpack-plugin');
```js
module.exports = {
	...
  plugins: [
    new CopyPlugin({
      patterns: [
        {
          from: path.resolve(__dirname, "src", "assets/images"),
          to: "assets/images"
        }
      ]
    }),
  ]
}
```
Es importante las propiedades from y to
* From ⇒ que recurso (archivo o directorio) deseamos copiar al directorio final
* To ⇒ en que ruta dentro de la carpeta final terminara los recursos

# Loaders de imágenes
Puedes usar una forma de importar las imágenes haciendo un import de las mismas y generando una variable

No es necesario instalar ninguna dependencia, webpack ya lo tiene incluido debemos agregar la siguiente configuración
```js
module.exports = {
	...
  module: {
    rules: [
      {
        test: /\.png/,
        type: "asset/resource"
      }
    ]
  },
}
```
Para empezar a usar esta configuración debemos importar la imagen de la siguiente forma
```js
import github from '../assets/images/github.png';
```
Para incluirlo en el HTML debes hacer lo siguiente
```js
// Ejemplo en Vanilla JS
const imagen = `<img src=`${github}` />`;
```
```
// Ejemplo en React
<img src={`${github}`} />
```
# Loaders de fuentes
Cuando utilizamos fuentes externas una buena práctica es descargarlas a nuestro proyecto
* Debido a que no hara un llamado a otros sitios

Por ello es importante usarlo dentro de webpack
Para esta tarea instalaras y usaras “file-loader” y “url-loader”

instalación con NPM
```
npm install url-loader file-loader -D
```
instalación con YARN
```
yarn add url-loader file-loader -D
```
Para aplicar esta configuración debes agregar la siguiente información
```js
module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.js',
    assetModuleFilename: 'assets/images/[hash][ext][query]'
  },
	...
  module: {
    rules: [
			...
      {
        test: /\.(woff|woff2)$/,
        use: {
          loader: "url-loader",
          options: {
            // limit => limite de tamaño
            limit: 10000,
            // Mimetype => tipo de dato
            mimetype: "application/font-woff",
            // name => nombre de salida
            name: "[name].[ext]",
            // outputPath => donde se va a guardar en la carpeta final
            outputPath: "./assets/fonts/",
            publicPath: "./assets/fonts/",
            esModule: false,
          }
        }
      }
    ]
  },
	...
}
```
Es importante que dentro de los estilos agregues @font-face
```css
@font-face {
	font-family: "Ubuntu";
	src: url("../assets/fonts/ubuntu-regular.woff2") format('woff2'),
			 url("../assets/fonts/ubuntu-regular.woff") format('woff');
	font-weight: 400;
	font-style: normal;
}
```
> una pagina para descargar las fuentes http://google-webfonts-helper.herokuapp.com/fonts/ubuntu?subsets=cyrillic,latin


# Optimización: hashes, compresión y minificación de archivos
Unos de las razones por que utilizamos webpack es porque nos permite optimizar y comprimir nuestro proyecto
Debes utilizar los siguientes paquetes
* **css-minimizer-webpack-plugin** ⇒ Nos ayuda a comprimir nuestros archivos finales CSS
* **terser-webpack-plugin** ⇒ Permite minificar de una mejor forma
Instalación
NPM
```npm i css-minimizer-webpack-plugin terser-webpack-plugin -D
```
YARN
```
yarn add css-minimizer-webpack-plugin terser-webpack-plugin -D
```
Una vez instalado el plugin debemos agregar la siguiente configuración
```
...
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
	...
	optimization: {
    minimize: true,
    minimizer: [
      new CssMinimizerPlugin(),
      new TerserPlugin()
    ]
  }
}
```
Cuando nombremos en la configuración de webpack es importante usar `[contenthash]` para evitar problemas con la cache

## ¿Por qué es importante usar Hashes en nuestros archivos?
Los recursos que se guardan en memoria cache suceden cuando el navegador entra a un sitio por primera vez detecta los recursos y los guarda. Por ello la siguiente vez sera mucho más rápido porque estarán en memoria
* La desventaja esta cuando sacamos una nueva versión, porque tendrán un mismo nombre evitando que se descargue los nuevos cambios, por lo tanto, el usuario no recibirá los nuevos cambios
* Para que no haya conflictos con la cache una vez que tengamos nuestro proyecto en producción es importante darles un hash para cada nueva versión

# Webpack Alias

Alias ⇒ nos permiten otorgar nombres paths específicos evitando los paths largos

Para crear un alias debes agregar la siguiente configuración a webpack
```js
module.exports = {
	...
	resolve: {
		...
    alias: {
      '@nombreDeAlias': path.resolve(__dirname, 'src/<directorio>'),
    },
	}
}
```
Puedes usarlo en los imports de la siguiente manera
```js
import modulo from "@ejemplo/archivo.js";
```
# Variables de entorno
Es importante considerar las variables de entorno va a ser un espacio seguro donde podemos guardar datos sensibles
* Por ejemplo, subir llaves al repositorio no es buena idea cuando tienes un proyecto open source

Para instalar debemos correr el comando
NPM
```
npm install -D dotenv-webpack
```
YARN
```
yarn add -D dotenv-webpack
```
Posteriormente debemos crear un archivo `.env` donde estarán la clave para acceder a la misma y el valor que contendrán
```
# Ejemplo
API=https://randomuser.me/api/
```
Es buena idea tener un archivo de ejemplo donde, el mismo si se pueda subir al repositorio como muestra de que campos van a ir

Una vez creado el archivo `.env` debemos agregar la siguiente configuración en `webpack.config.js`
```js
...
const Dotenv = require('dotenv-webpack');
module.exports = {
	...
	plugins: [
		new Dotenv()
  ],
}
```
**dotenv-webpack** ⇒ Leera el archivo `.env` por defecto y lo agregar a nuestro proyecto
Para usarlas debes hacer lo siguiente
```js
const nombre = process.env.NOMBRE_VARIABLE;
```
Toda la configuración se podrá acceder desde `process.env`

# Webpack en modo desarrollo
Creamos un nuevo archivo:
webpack.config.dev.js
Copiamos todo lo de webpack.config.js a el archivo que acabamos de crear.
Borramos o comentamos el siguiente código, ya que no necesitamos optimizar para el modo de desarrollo (Queremos ver cuando funcionan las cosas).
```js
    optimization: {
        minimize: true,
        minimizer: [
            new CssMinimizerPlugin(),
            new TerserPlugin()
        ]
    }
```
También borramos o comentamos por la misma razón:
```js
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
const TerserPlugin = require('terser-webpack-plugin')
```
Seguido del atributo output añadimos:
```js
output: {
},
mode: 'development',
```
En package.json:
```js
"dev": "webpack --config webpack.config.dev.js" 
```
y ejecutamos npm run dev

# Webpack en modo producción

Actualmente tenemos el problema de tener varios archivos repetidos los cuales se fueron acumulando por compilaciones anteriores
Para ello puedes limpiar la carpeta cada vez que hacemos un build, usando clean-webpack-plugin
* Cabe recalcar que esta característica es mucho más util para la configuración de producción

Para instalarlo debes correr el siguiente comando:
NPM

```
npm install -D clean-webpack-plugin
```

YARN
```
yarn add -D clean-webpack-plugin
```
Para agregarlo a nuestra configuración de webpack agregamos los siguientes cambios a webpack.config.js
```
...
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
module.exports = {
	...
	plugins: [
		...
		new CleanWebpackPlugin()
	]
}
```
# Webpack Watch
El modo watch hace que nuestro proyecto se compile de forma automática
* Es decir que está atento a cambios

Para habilitarlo debemos agregar lo siguiente en la configuración de webpack
```
module.exports = {
	...
	watch: true
}
```
Cada vez que haya un cambio hara un build automático
Otra manera es mandar la opción mediante parámetros de consola en package.json
```
{
	"scripts": {
		"dev:watch": "webpack --config webpack.config.dev.js --watch"
	}
}
```
Vale la pena recordar que si aplicamos en modo producción se tomara más tiempo porque se optimizaran los recursos
* Por ello en modo desarrollo se salta ese paso y es más rápido la compilación

# Deploy a Netlify
creamos un archivo netlify.toml
.
y dentro de el creamos una configuracion
```
[build]

  publis = "dist"
  command = "npm run build"
```
.
despues vamos a crear un script que nos ayudara a crear las variables de entorno en nuestro servidor
.
primero creamos una carpeta que se llame scripts
y un archivo que se llamara create-env.js
y dentro de el colocamos el siguiente codigo
.

```js
const fs = require('fs');

	fs.writeFileSync('./.env',`API=${process.env.API}\n`)
```
despues vamos a la pagina de netlify a la seccion de build & deploy
.
vamos a la sección que dice enviroment, y le damos en edit variables, y alli colocamos las variables que en este caso solo es la variable API y con su valor que es https://randomuser.me/api/

# Webpack dev server
HTML5 History API permite la manipulación de session history del navegador, es decir las páginas visitadas en el tab o el frame en la cual la página está cargada.

**Recursos**
How To Optimize Your Site With GZIP Compression

**Apuntes**
Cuando trabajamos con webpack deseamos ver los cambios en tiempo real en un navegador
Para tener esta característica esta webpack-dev-server
Para ello debemos instalarlo
NPM
```
npm install -D webpack-dev-server
```
Yarn
```
yarn add -D webpack-dev-server
```
Posteriormente debemos agregar la siguiente configuración en webpack.config.dev.js
* Lo hacemos en la configuración de desarrollo debido a que esta característica solo nos ayudara a ver cambios al momento de desarrollar la aplicación
```js
module.exports = {
	...
	devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    historyApiFallback: true,
    port: 3000,
  }
}
```
En la configuración podemos observar lass siguientes propiedades
* **contentBase** ⇒ Le dice al servidor donde tiene que servir el contenido, solo es necesario si quieres servir archivos estáticos
* **compress** ⇒ Habilita la compresión gzip
* **historyApiFallback** ⇒ cuando estas usando HTML5 History API la página `index.html` sera mostrada en vez de una respuesta 404
* **Port** ⇒ es el puerto donde vamos a realizar las peticiones

Para comenzar a utilizarlo debes agregar el siguiente script a package.json
```js
{
	...
	"scripts": {
	...
	"start": "webpack serve --config webpack.config.dev.js"
	}
}
```
# Webpack Bundle Analyzer

Cuando tenemos un proyecto es buena idea poder revisar su impacto en tamaño por ese motivo webpack nos ofrece un paquete para poder verificar y analizar el tamaño del bundle final
Para instalar corremos el comando
NPM
```
npm install -D webpack-bundle-analyzer
```
YARN
```
yarn add -D webpack-bundle-analyzer
```
Si deseamos hacer un análisis debemos correr los siguientes comandos
```
npx webpack --profile --json > stats.json
npx webpack-bundle-analyzer stats.json
```

Probando un poco, actualmente implementar en el código el paquete no es necesario, ya que en la clase lo hacemos manualmente con los comandos, pero si deseamos automatizarlo podemos crear el siguiente script

Creamos el script en package.json de analyze
```js
{
	...
	"scripts": {
		"build:analyze": "webpack --mode production --config webpack.config.js --analyze",
	}
}
```
El flag --analyze le dice al paquete webpack-bundle-analyzer que haga esa tarea sobre el bundle de producción

Si deseas hacer la implementación mediante el código, y tener más control sobre este aspecto, en la documentación de NPM nos comenta que podemos personalizar
# Webpack DevTools
**Ideas/conceptos claves**
**source map** es un mapeo que se realiza entre el código original y el código transformado, tanto para archivos JavaScript como para archivos CSS. De esta forma podremos debuggear tranquilamente nuestro código.


Con las devtools de webpack te permite crear un mapa de tu proyecto y con el podemos
* Leer a detalle
* Analizar particularidades de lo que está compilando nuestro proyecto

Para comenzar debemos ir a `webpack.config.js` y agregar la propiedad `devtool: "source-map"`
* Esta opción genera un source map el cual posteriormente chrome lo lee y te permite depurar de una mejor forma

# Instalación y configuración de React
```
# Descargar el repositorio de Github
git clone git@github.com:platzi/curso-webpack-react.git
# Movernos a la carpeta
cd curso-webpack-react
# Abrir VS Code
code .
# Inicializar npm
npm init -y
# instalar dependencias
npm install react react-dom -s
```
# Configuración de Webpack 5 para React.js
.
Añadiremos webpack para poder preparar el proyecto y mandarlo a prod.

Vamos a repetir muchos de los pasos que hicimos anteriormente:

Instalaremos las dependencias:
```
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader -D
```
Vamos a ir creando nuestros recursos: configuraciones:
```js
//Creamos .babelrc y añadimos la estructura
{ //Para poder compilar
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
```
Instalamos webpack para el proyecto con:
```
npm install webpack webpack-cli webpack-dev-server -D
```
Creamos el archivo de configuración y añadimos las configuraciones correspondientes:
```
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },

  resolve: {
    //Extensiones que vamos a trabajar
    extensions: [".js", ".jsx"],
  },

  module: {
    //Reglas
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
    ],
  },

  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 3006,
  },
};
```
# configuracion de plugins y loaders para react
## NPM
```
npm install -D html-loader html-webpack-plugin
```
## YARN
```
yarn add -D html-loader html-webpack-plugin
```
# Configuración de Webpack para CSS en React
Instalación de dependencias
## NPM
```
npm install -D mini-css-extract-plugin css-loader style-loader sass sass-loader
```
## YARN
```
yarn add -D mini-css-extract-plugin css-loader style-loader sass sass-loader
```
## NPM
```
npm install -D css-minimizer-webpack-plugin terser-webpack-plugin clean-webpack-plugin
```
## YARN
```
yarn add -D css-minimizer-webpack-plugin terser-webpack-plugin clean-webpack-plugin
```