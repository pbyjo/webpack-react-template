# Webpack con React

### M6 - Integración básica de React.js

#### Instalación y configuración de React

 >Clase 22

Clonamos repo
`git@github.com:platzi/curso-webpack-react.git`

iniciamos npm
`npm init -y`

instalamos react
`npm install react react-dom -S` <!-- save / dependencia --> 

creamos los recursos del proyecto
``` js
src -> index.js | components -> App.js
public -> index.html
dist
```

#### Configuración de webpack 5 para react.js

 >Clase 23

Instalamos babel
`npm install @babel/core @babel/preset-env @babel/preset-react babel-loader -D`

configuramos `.babelrc`

Instalamos webpack
`npm install webpack webpack-cli webpack-dev-server -D`

Configuramos nuestro `webpack.config.js`

``` js
    const path = require('path');

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        },

        resolve: {
            extensions: ['.js', '.jsx']
        },

        module: {
            rules: [
                {
                    test: /\.(js|jsx)$/,
                    exclude: /node_modules/,
                    use : {
                        loader: 'babel-loader',
                    }
                }
            ]
        },
        
        devServer: {
            contentBase: path.join(__dirname, 'dist'),
            compress: true,
            port: 3006
        }
    }
```

#### Configuración de plugins y loaders para React

 >Clase 24

Instalamos 
`npm install html-loader html-webpack-plugin -D`

configuramos 
``` js
const HtmlWebpackPlugin = require('html-webpack-plugin');
    ...
        {
            test: /\.html$/,
            use: [
                {loader: 'html-loader'}
            ]
        }
    
    plugins: [
        new HtmlWebpackPlugin({
            template: './public/index.html',
            filename: './index.html'
        })
    ]
```

Script:
``` js
    "build" : "webpack --mode production",
    "server:start": "webpack serve"
```

nota: Si agregamos un runtime automatico para babel no necesitamos importar react en los componentes .jsx.

``` js
    {
	"presets": [
			"@babel/preset-env",
			["@babel/preset-react", {
				"runtime": "automatic"
			}]
	]
}
```

#### Configuración de Webpack para CSS en React

 > Clase 25

Instalamos:
`npm i mini-css-extract-plugin css-loader style-loader sass sass-loader -D`

configuramos webpack.config.js
``` js
    const MiniCssExtractPlugin = require('mini-css-extract-plugin');

    module: {
        rules: [
            {
                test: /\.s[ac]ss$/,
                use: [
                    'style-loader',
                    'css-loader',
                    'sass-loader'
                ]
            }
        ]
    }

    plugins: [
        new MiniCssExtractPlugin({
            filename: '[name].css'
        })
    ]
```

