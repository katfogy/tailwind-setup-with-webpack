# Webpack & Tailwind CSS Setup 

### Create your package.json
```
npm init -y
```

### Create your src folder
Create a folder called **src** and add an empty **index.js** file. The code that webpack compiles goes in here including any Javascript modules and the main Tailwind file.

### Install Tailwind
```
npm i -D tailwindcss
```

### Install Webpack & Loaders
```
npm i -D webpack webpack-cli webpack-dev-server style-loader css-loader postcss postcss-loader postcss-preset-env
```
### Create webpack.config.js in the root and add this to it...
```
const path = require('path')

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  devServer: {
    static: {
      directory: path.resolve(__dirname, 'dist'),
    },
    port: 3000,
    open: true,
    hot: true,
    compress: true,
    historyApiFallback: true,
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        include: path.resolve(__dirname, 'src'),
        use: ['style-loader', 'css-loader', 'postcss-loader'],
      },
    ],
  },
}

```

### Add Tailwind Directives
Create a **style.css** in your **src** folder and add these 3 lines
```
@tailwind base;
@tailwind components;
@tailwind utilities;

```

### Tailwind Config File
run the following command to generate your **tailwind.config.js** file and add this to it
npx tailwindcss init
```
module.exports = {
  content: ['./dist/*.html'],
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}

```

### PostCCSS Config File
Create a file in the root called **postcss.config.js** and add this
```
const tailwindcss = require('tailwindcss');
module.exports = {
  plugins: [
    'postcss-preset-env',
    tailwindcss
  ],
};
```

### Add this line to your src/index.js
```
import './style.css';
```

### Create a **dist/index.html** file and add this
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Webpack App</title>
  </head>
  <body>
    <h1 class="text-4xl text-blue-700">My Webpack + Tailwind App</h1>
    <script src="bundle.js"></script>
  </body>
</html>
```

### Add scripts to package.json

Add the following to your package.json file
```
"scripts": {
    "dev": "webpack serve",
    "build": "webpack"
  },
```

### Running your app
To build once and create your **dist/bundle.js** file, run
```
npm run build
```

To run your webpack server
```
npm run dev
```

You now have Webpack setup along with Tailwind CSS