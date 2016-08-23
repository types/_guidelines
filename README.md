# Guidelines

> Simple documentation for @types contributors.

## Repository

If you're creating a repository under `@types`, make sure to follow the existing naming guidelines. That is, `<source>-<lib name>`. The list of sources can be viewed in the [registry](https://github.com/typings/registry#structure).

### Structure

1. Make sure you have a descriptive README (at least link to the source repository)
2. Set up `tsconfig.json` using the minimum settings (see [`tsconfig.json` settings](#tsconfigjson))
3. Create `package.json` with test suite and dependencies defined (there should be no implicit dependencies)
4. Make sure the name in `package.json` is `@types/<lib name>` - this allows TypeScript 2.0 users to install using `npm` (E.g. `npm install types/<source>-<lib name>`)
5. Remember to set up `typings.json -> typings` and `package.json -> typings`
6. Licenses should be under MIT or similar, remember to add a license to your work
7. Make sure any typings dependencies are listed in both `package.json` (with `@types`) and `typings.json` (using the Typings registry)

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
