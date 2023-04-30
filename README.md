# Boilerplate NodeJS + Express + Typescript + ESLint + Prettier 

This is a personal template for build NodeJS + Express + Typescript + ESLint + Prettier projects.
It's my favorite configuration for NodeJS projects, and it's very basic, but it's very useful for me, I only need the initial configuration for start a project with this technologies.
Now I learn Hexagonal Architecture, and migrating my past boilerplate to this architecture, but I need a template for start a project with this technologies, and this is the reason for create this template.

But, I think that this template can be useful for other people, and I decided to share it.

I repeat this is a very basic template, a don't have a lot of configurations, but I think that is a good start point for start a project with this technologies. no MVC, no ORM, no database, no tests, no nothing, only the initial configuration for start a project with this technologies.

This boilerplate not use Nodemon, I prefer use ts-node-dev, because it's compile the typescript files and run the server, and it's very helpful for development.

## Table of contents
This is the table of contents for this template.

- [Boilerplate NodeJS + Express + Typescript + ESLint + Prettier](#boilerplate-nodejs--express--typescript--eslint--prettier)
  - [Table of contents](#table-of-contents)
  - [How to re create this template](#how-to-re-create-this-template)
  - [1.- Create the project](#1--create-the-project)
  - [2.- Install the dependencies and devDependencies](#2--install-the-dependencies-and-devdependencies)
  - [3.- Setup the TypeScript configuration file](#3--setup-the-typescript-configuration-file)
  - [4.- Configure TS-Standard](#4--configure-ts-standard)
  - [5.- Configure Prettier (Optional)](#5--configure-prettier-optional)
  - [6.- Configure commands for linter, dev server and build](#6--configure-commands-for-linter-dev-server-and-build)
  - [7. Run the server](#7-run-the-server)
  - [8.- Build the project](#8--build-the-project)
  - [9.- Run the server in production mode](#9--run-the-server-in-production-mode)
  - [10.- Deploy the project on Vercel](#10--deploy-the-project-on-vercel)


## How to re create this template

## 1.- Create the project

Open a terminal and run `yarn init -y` inside the folder you want to create the project.

## 2.- Install the dependencies and devDependencies

- Install the dependencies initials:

```bash
yarn add express
```

- Install the dependencies for development:

```bash
yarn add -D typescript @types/express ts-node-dev ts-standard
```

> typescript dependencias expose the `tsc` command for compile the typescript files, is very helpful for development and build product production.

> @types/express is a typescript definitions for express.

> ts-node-dev is a tool for development, it's compile the typescript files and run the server.

> ts-standard is a linter/formatting for typescript, it's based on standardjs.

## 3.- Setup the TypeScript configuration file

After install the dependencies, we need to create the typescript configuration file, for this run the next command:

```bash
 yarn tsc -- --init
```

(-- ) is a flag that is passed to the TypeScript compiler. It is not a flag for the yarn tsc command.

This command create a file called `tsconfig.json` with the default configuration for typescript, `modify with your requirements for development`.

to view my configuration file, go to the path: `tsconfig.json`, it's in the root of the project and my favorite configuration :D.

## 4.- Configure TS-Standard

After configure TSC and install TS-Standard dev dependence, add the following lines to the `package.json` file:

in the `scripts` section add the next line:

```json
....
"scripts": {
    ...
 "lint": "ts-standard src/**/*.ts",
    ...
  },
....
```

this configuration add a command for run the linter, and detect errors in the code, por this it's necessary indicate the path of the files to check, in this case `src/**/*.ts` indicate that check all files with extension `.ts` in the folder `src` and subfolders, now it's necessary indicate the config for fix the errors.

in the `scripts` section add the next line:

```json
"eslintConfig": {
    "parserOptions": {
      "project": "./tsconfig.json"
    },
    "extends": "./node_modules/ts-standard/eslintrc.json"
  }
```

## 5.- Configure Prettier (Optional)

if you using Prettier, add the following to package.json, it's personal this configuration, you can change it or omit it.

```json
"prettier": {
    "singleQuote": true,
    "trailingComma": "all",
    "semi": true
  }
```

## 6.- Configure commands for linter, dev server and build

In the `scripts` section add the next lines:

```json
    "lint": "ts-standard src/**/*.ts",
    "dev": "ts-node-dev src/index.ts",
    "start": "node build/index.js",
    "build": "rimraf ./build && tsc "
```

- lint: run the linter
- dev: run the server in development
- start: run the server in production mode with the compiled files
- build: delete a folder ./build and compile the typescript files

## 7. Run the server

In the folder src create a file called `index.ts` and add the next code:

```typescript
import express from 'express'; // import express

const app = express(); // create express app

app.use(express.json()); // middleware for parsing application/json

const PORT = 3000; // port for the server

// routes
app.get('/test', (_req, res) => {
  res.status(200).send({
    message: 'Hello World',
    ok: true
  });
});

// run the server
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

to execute this code its necessary run the next command:

```bash
yarn dev
```

this command run the server in development mode, and compile the typescript files.

## 8.- Build the project

In this point you can add more code to the project, when you finish, run the next command for build the project:

```bash
yarn build
```

this command delete the folder `build` and compile the typescript files, the result is a folder called `build` with the compiled files, this folder is ready for production.

## 9.- Run the server in production mode

After build the project, run the next command for run the server in production mode:

```bash
yarn start
```

this command run the server with the compiled files located in the folder `build`.

## 10.- Deploy the project on Vercel

Vercel is a platform for deploy projects, it's very easy to use, and it's free for personal projects.
