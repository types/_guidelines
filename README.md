# Guidelines

[![Gitter][gitter-image]][gitter-url]

> Simple documentation for @types contributors.

## Repository

If you're creating a repository under `@types`, make sure to follow the existing naming guidelines. That is, `<source>-<lib name>`. The list of sources can be viewed in the [registry](https://github.com/typings/registry#structure).

### Structure

Using [`npm-quickly-copy-file`](https://github.com/types/npm-quickly-copy-file) as an example, make sure you have the following set up to ease contributing.

1. Make sure you have a descriptive README with, at least, a link to the source repository ([`README.md`](https://github.com/types/npm-quickly-copy-file/blob/master/README.md))
2. Set up `tsconfig.json` using the minimum required settings (see [`tsconfig.json` settings](#tsconfigjson)) ([`tsconfig.json`](https://github.com/types/npm-quickly-copy-file/blob/master/tsconfig.json))
3. The work should be licensed under MIT, or similar, to enable redistribution ([`LICENSE`](https://github.com/types/npm-quickly-copy-file/blob/master/LICENSE))
4. Create a `package.json` with the `@types/<pkg>` name, testing scripts, `typings` field and development dependencies - there should be no implicit dependencies ([`package.json`](https://github.com/types/npm-quickly-copy-file/blob/master/package.json))
5. Create the `typings.json` version with original package name ([`typings.json`](https://github.com/types/npm-quickly-copy-file/blob/master/typings.json))
6. I recommend checking in an `.editorconfig` file for people to follow ([`.editorconfig`](https://github.com/types/npm-quickly-copy-file/blob/master/.editorconfig))
7. Make sure all generated assets are `.gitignore`'d ([`.gitignore`](https://github.com/types/npm-quickly-copy-file/blob/master/.gitignore))
8. Add the `tslint.json` configuration extending `tslint-config-standard` ([`tslint.json`](https://github.com/types/npm-quickly-copy-file/blob/master/tslint.json))
9. Write the definition, mirroring the original JavaScript source code with types ([`index.d.ts`](https://github.com/types/npm-quickly-copy-file/blob/master/index.d.ts))
10. Make sure you include some tests for future contributors ([`test.ts`](https://github.com/types/npm-quickly-copy-file/blob/master/test.ts))
11. Set up `.travis.yml` for CI ([`.travis.yml`](https://github.com/types/npm-quickly-copy-file/blob/master/.travis.yml))
12. Enable [Greenkeeper](https://greenkeeper.io/) and [Travis CI](http://travis-ci.org/)

### Quickly Enable Travis CI and Greenkeeper

```sh
gem install travis
npm install -g greenkeeper

travis enable
greenkeeper enable
```

**P.S.** You should have the JavaScript source of the typings as a [`devDependency`](https://github.com/types/npm-quickly-copy-file/blob/c744cbbed03e43f6f3fba890ac677c903c666897/package.json#L30), using the `~` or `1.0.x` version ranges. If Greenkeeper detects a new version, you'll have a chance to review the changes in a Pull Request.

### `.travis.yml`

```yml
sudo: false
language: node_js

notifications:
  email:
    on_success: never
    on_failure: change

script:
  - npm run lint
  - npm run bundle
  - npm rm tslint
  - npm install $TYPESCRIPT --force
  - npm run exec

env:
  - TYPESCRIPT=typescript@1.8
  - TYPESCRIPT=typescript@latest
  - TYPESCRIPT=typescript@next

node_js:
  - "stable"
```

### Branching Vs Folder Versions

The current practice for typing multiple versions in folders vs branches is undecided. The most obvious reason to target multiple branches over folders is supporting `npm` natively. NPM can not install using folders.

### `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "moduleResolution": "node",
    "noImplicitAny": true
  }
}
```

For environmental typings, it also makes sense to enable `noLib` and **only** rely on `lib.core.d.ts`. This enables people to do things like disable browser typings under node.js.

[gitter-image]: https://badges.gitter.im/types/guidelines.svg
[gitter-url]: https://gitter.im/types/Lobby
