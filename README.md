Let's create a boilerplate NodeJS project with typescript and eslint support.

Step 1: Create a new project

Create a new directory for your project

```
mkdir nodejs-typescript-skeleton
cd nodejs-typescript-skeleton
```

Step 2: Initialize an npm project

Then run the following command to initialize the project with yarn. You can use npm if you want. That is not that different.

```
yarn init -y
```

Step 3: Create entry to our project

Then create a new folder named src and inside that create a new file named **index.js**

Paste the following code directly into that.

```
const name = 'faisal'
console.log('this is working');
```

Now run the project from console to see if it's working or not.

```sh
node src/index.js
```

It will print the message and our project is up and running.

Step 4: Let's introduce Typescript

Let's first convert our **index.js** file into **index.ts** . Then install typescript locally.

```
yarn add -D typescript
```

also create a typescript configuration file in the root folder named **tsconfig.json**. And paste the following code there.

```json
{
  "extends": "@tsconfig/node16/tsconfig.json",
  "compilerOptions": {
    "outDir": "dist"
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

A few things to notice here

1. We are extending a default configuration for nodejs 16 in the first line. So you have to install that as well.

```sh
yarn add -D @tsconfig/node16
```

The same configuration is also[ available for other nodejs versions](https://github.com/tsconfig/bases) like 14 and 12.

2. we are configuring _outDir_ as **"dist"** which means our bundled files will go into a new directory named _dist_
3. We are only specifying **"src"** folder to be compiled. So all our typescript files will go there.
4. We are excluding **node_modules** folder from compilation.

Lastly let's include the type definition for node by running the command

```sh
yarn add -D @types/node
```

Step 5: Let's compile

Now let's compile our project by running the following command.

```
yarn tsc
```

Now go to your **dist** folder to see the compiled files.

Step 6: Executing a Typescript file directly

It's not practical to run the tsc command to bundle the typescript files into javascript and then using them. So let's add a packages to solve that problem.

```sh
yarn add -D ts-node
```

Now **ts-node** is a package that can be used to run any typescript file directly. So let's' try first.

```sh
ts-node src/index.ts
```

it will directly execute the typescript nodejs file.

Step 7: Development Mode

Now we can run a typescript file directly without compiling to javascript. Let's take it a bit further.
We need hot reloading support for the project during development.

Let's add a popular package to solve that.

```sh
yarn add -D nodemon
```

**nodemon** is a package that can watch the file changes and compile them when you save them. So that you don't have to run the file again and again.

Let's try to run that

```sh
yarn nodemon src/index.ts
```

Now go ahead and make a change inside your **index.ts** file to see the changes realtime.

Bonus Step: Make development even more pleasant

There is another package that is specifically made for typescript project. its **ts-node-dev** package.
Let's add that to the project and see what we can do.

```sh
yarn remove nodemon ts-node // remove the previous ones
yarn add -D ts-node-dev
```

Now let's run the following command and see it that works as expected

```sh
yarn ts-node-dev --respawn src/index.ts
```

Note that the **--respawn** flag is given to ensure that the files are re-compiled when changed.
This is a better choice than nodemon and it's also faster.

Final Improvement: Add script

Now go to your **package.json** file and add the following script to make it easier.

```json
 "scripts": {
    "dev": "ts-node-dev --respawn src/index.ts",
    "build": "tsc"
  },
```

Then you can just run the following command to get it running in development mode

```sh
yarn dev
```

And to build the project just run the following command

```sh
yarn build
```

Now you have a working nodejs skeleton project! You can use this any way you like.

### Github Repo: https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton
