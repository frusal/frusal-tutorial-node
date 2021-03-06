# Frusal Node.js Tutorial

🚧 *The project is in development and is not available for general public yet.*

Building a [Node.js] application to access [frusal.com] workspace.

There are tutorials for other environments available, see [Angular Tutorial] and [React Tutorial].

In this tutorial we are going to build a simple application using ECMAScript (aka JavaScript), which meant to be running under Node.js. The application would access [frusal.com] workspace, it would create a class (which is like a table in many ways) in the workspace and then write some data to it.

## Prerequisites

Please make sure you have the following installed:

- Either: Windows, Linux or macOS
- [Node.js], which is an open source JavaScript runtime environment
- [Visual Studio Code], which is a popular open source IDE among JavaScript developers

Run the following command in the terminal to make sure node is installed properly:

```txt
npm --version
```

Create a new NPM package, with the following commands. It would take you through a series of questions to complete.

```txt
mkdir frusal-tutorial-node
cd frusal-tutorial-node
npm create
```

<details><summary>See the console output</summary>

```txt
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (my-first-frusal-access-application)
version: (1.0.0)
description:
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to /Users/alex/temp/del-me/my-first-frusal-access-application/package.json:

{
  "name": "my-first-frusal-access-application",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
```

</details>

## Install frusal library

Run the following command to install frusal library dependency, configure `project.json` and create `frusal.json`. It would take you through a series of questions to complete.

*Note that this wizard is activated if `frusal.json` file does not yet exist.*

```text
npx frusal
```

<details><summary>See the console output</summary>

```txt
If you are using any source control system like git or svn, you might want to check in any outstanding changes to isolate the changes done by this installation.
Do you want to continue? [yes]: yes

Initialising my-first-frusal-access-application npm project for frusal library which allows to connect to frusal.com workspace.

Please choose library type:
  [1] @frusal/library-for-browser: Bundled library designed to run in a browser with no external dependencies.
  [2] @frusal/library-for-node: Bundled library designed to run under node.js with no external dependencies.
  [3] @frusal/library: Core library with "autobahn" and "rxjs" dependencies.
Library type [1]: 2

Please choose generated source code language:
  [1] ECMAScript (aka JavaScript)
  [2] TypeScript
Source code [1]: 1

Please choose generated source code module loader type:
  [1] ECMAScript 6 Modules (using import statements) *recommended*
  [2] RequireJS (using require() function)
Module loader [1]: 1

Source code model location [.]: .

Installing "frusal" npm dependency...

 * Frusal.com access library is successfully initialised for project my-first-frusal-access-application.
 * Next, please login and start updating your source code stabs and schema declarations.
 * You can use `npm run frusal login`, `npm run frusal update` or `npm run frusal watch` commands.

Please read the note above [ok]: ok
Thank you.
```

</details>

Now, lets login to [frusal.com] with the following command:

```text
npx frusal login
```

<details><summary>See the console output</summary>

```txt
Frusal login: fred@example.com
Password:
Please choose a workspace:
  [1] Unit Test
Workspace [1]: 1

CONNECTED to workspace 'Unit Test' (ws_001_unit_test) as 'unit.test@fruit-salad.tech'
```

</details>

## Workspace schema

Now, let's create persistent entity classes which is a part of our workspace schema. Usually, you would be doing it through frusal.com web UI, but for simplicity of this tutorial we are going to use a JavaScript to do that for us.

Copy **[deploy-my-schema.mjs]** file from [this example][Example Schema by Script] and run it:

```text
node --experimental-json-modules deploy-my-schema.mjs
```

<details><summary>See the console output</summary>

```text
Connecting to workspace "ws_001_unit_test"...
Creating classes at module "My Module"...
Schema changes deployed.
```

</details>

*Study this script if you want to manipulate schema objects (create persistent classes and fields) from within your application code.*

## Local declarations

Check the status of the connection and the workspace:

``` text
npx frusal status
```

<details><summary>See the console output</summary>

```txt
CLI script to install and configure frusal.com workspace access library with static type checking against live schema.

User preferences: /Users/alex/.npm-frusal (first in ancestry)
Base directory: /Users/alex/temp/del-me/my-first-frusal-access-application
Config file: frusal.json
Source code model location: .

CONNECTED to workspace 'Unit Test' (ws_001_unit_test) as 'unit.test@fruit-salad.tech'

Classes in 'My Module':
 - Book
```

</details>

Update (or create, in our case), the local model source code stubs and TypeScript declarations (TSD). The stubs are meant to be taken over by You for further development and maintenance. The TSDs are maintained by `npx frusal` script and used by [Visual Studio Code] IDE for source code static analysis, type validation and auto completion (IntelliSense).

```text
npx frusal update
```

<details><summary>See the console output</summary>

```txt
Updating schema changes for workspace 'Unit Test' (ws_001_unit_test), connected as 'unit.test@fruit-salad.tech'
Source code model location: .

Updating on 20/04/2020, 5:52:04 pm...
  my-module.rt.d.ts
  my-module.js
Done
```

</details>

*Have a look at  [`my-module.rt.d.ts`](./my-module.rt.d.ts) and [`my-module.js`](./my-module.js) created. The file names matching the module name as defined at frusal workspace. If there any classes defined at workspace module schema, they would be reflected there.*

We could run the script with `watch` flag to keep schema files up to date in real time:

```text
npx frusal watch
```

<details><summary>See the console output</summary>

```txt
Watching schema changes at workspace 'Unit Test' (ws_001_unit_test), connected as 'unit.test@fruit-salad.tech'...
Source code model location: .

Updating on 20/04/2020, 5:54:14 pm...
Done
```

</details>

*This could be useful during development. Use ^C to terminate the process.*

## Creating application

Create __`index.js`__ file with the content you can download from [here](./index.js).

Change the login call arguments in it.

## Running

Now, let's try to run it with the following command:

```text
node index.js
```

<details><summary>See the console output</summary>

```text
Login...
User name: Unit Test
Workspace: Unit Test
Module: My Module
Found the following books already exist: b0k3f0,b0k4f0,b0k5f0,b0k6f0,b0k7f0
New Book created: Bible
Done.
```

</details>

*We are not going into the details of how to use `session` object, `Stage` and `Transaction`, `Stage::query`, etc. It is out of scope for this tutorial. But you are encouraged to study the code in `index.js` as an example of library usage.*

[frusal.com]: https://frusal.com
[Node.js]: https://nodejs.org
[Visual Studio Code]: https://code.visualstudio.com/
[Angular Tutorial]: https://github.com/frusal/frusal-tutorial-angular
[React Tutorial]: https://github.com/frusal/frusal-tutorial-react
[Node.js Tutorial]: https://github.com/frusal/frusal-tutorial-node
[Example Schema by Script]: https://github.com/frusal/frusal-example-schema-by-javascript#readme
[deploy-my-schema.mjs]: https://github.com/frusal/frusal-example-schema-by-javascript/blob/master/deploy-my-schema.mjs