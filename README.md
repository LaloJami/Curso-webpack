
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