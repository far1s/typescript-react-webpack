# React, Typescript, Webpack
Super fast copy and paste typescript, react and webpack tutorial

## Part 1: Typescript, Webpack
Create a folder and initialize npm
```shell
mkdir typescript-react-webpack
cd typescript-react-webpack
mkdir src build
npm init -y
```

Install typescript and webpack
```shell
npm install --save-dev typescript webpack
```

Create `webpack.config.js` and add configurations
```shell
touch webpack.config.js
```
Insert following
```javascript
var path = require('path');
var config = {
  entry: ['./src/App.tsx'],
  output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['*', '.ts', '.tsx', '.js']
  },
  module: {
    loaders: [
      {
        test: /\.tsx?$/,
        loader: 'ts-loader',
        exclude: /node_modules/
      }
    ]
  }
};
module.exports = config;
```

Install ts-loader
```shell
npm install --save-dev ts-loader
```

Create `index.html`
```shell
touch index.html
```
Insert following
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Getting Started with Typescript, ReactJS, and Webpack</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="build/bundle.js"></script>
  </body>
</html>
```

Add build script to package.json
```json
{
  "name": "typescript-react-webpack",
  "scripts": {
    "build": "webpack"
  },
  "devDependencies": {
    "ts-loader": "^2.0.2",
    "typescript": "^2.2.1",
    "webpack": "^2.2.1"
  }
}
````

## Part 2: ReactJS

Install react and react-dom
```shell
npm install --save-dev react react-dom
````
Since we’re using a 3rd party library with Typescript, we’re going to need to npm install Typings as well.
Install typings once globaly
```shell
npm install typings -g
````

Download the Definitely Typed files for React and ReactDOM.
```shell
typings install --save react
typings install --save react-dom
```

Notice that our directory now has a typings directory as well as a typings.json file. The typings.json file specifies all of the definition files we have installed, and the typings directory contains the actual definition files.

Now that we’re trying to use React with Typescript, we should create a Typescript configuration file in the root directory — be sure to name it `tsconfig.json`.
```shell
touch tsconfig.json
```
Insert following
```json
{
  "compilerOptions": {
    "jsx": "react",
    "module": "commonjs",
    "noImplicitAny": true,
    "outDir": "./build/",
    "preserveConstEnums": true,
    "removeComments": true,
    "target": "ES5"
  },
  "exclude": [
    "node_modules",
    "typings/browser.d.ts",
    "typings/browser"
  ]
}
```
Of particular importance to us is the “jsx” key which tells Typescript to accept React’s JSX syntax whenever we create a file with a “.tsx” extension.

Create the file `src/app.tsx`
```shell
touch src/App.tsx
```
Insert following
```jsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import Hello from "./Hello";

ReactDOM.render(
  <Hello name="Willson" />,
  document.getElementById("root")
);
```

Create the files `src/Hello.tsx`
```shell
touch src/Hello.tsx
```
Insert following
```jsx
import * as React from "react";

interface HelloProps {
	name: string;
}

export default class Hello extends React.Component<HelloProps, {}> {
  render() {
    return <div>Hello, {this.props.name}</div>;
  }
}
```

Folder structure
```
typescript-react-webpack
└───build
│   │   bundle.js
│   node_modules
└───src
│   │   App.tsx
│   │   Hello.tsx
│   typings
|   index.html
|   package.json
|   tsconfig.json
|   typings.json
|   webpack.config.js
```

## Part 3: Run the App

```shell
npm run build
```

Open index.html in browser
If you see "Hello, Willson" everything is ok
