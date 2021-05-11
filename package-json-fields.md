---
title: Package.json fields for maintainer's happiness
author: Maciej Barelkowski
---

# Package.json fields for maintainer's happiness

_Maciej Barelkowski_

---

## What's this all about?

* Save time
* Save frustration
* Be happy and make others happy

---

## `private` for monorepo

```json
{
  "private": true
}
```

This prevents npm from publishing the package.

Pretty useful in a monorepo setup:

* Camunda Modeler
* dmn-js
* form-js

and in closed-source packages like Cloud Connect Plugin.

---

## `scripts#prepare` for installing from GitHub

Use this:

```json
"name": "my-package",
"scripts": {
  "prepare": "rollup -c"
}
```

and then you can `npm install owner/my-package`.

---

## `.npmignore` drawbacks

You have to remember to update it once you add new infra files:

```diff
.eslintrc
.babelrc
.vscode
- travis.yml
+ .github
```

...or secrets:

```diff
.eslintrc
.babelrc
.vscode
.github
+ .env
```

Cf. [diagram-js@3.0.0](https://unpkg.com/browse/diagram-js@3.0.0/)

---

## solution: `files`

Explicitly list files to be included in the package.

```json
"files": [
  "dist",
  "resources",
  "!resources/**/*.cmof" // supports negation and patterns!
]
```

* Explicit
* Easy to read
* No need to run `npm pack --dry-run` to know what's included

---

## Read more

:arrow_right: [Docs](https://docs.npmjs.com/cli/v6/configuring-npm/package-json)

---

## That's all Folks
