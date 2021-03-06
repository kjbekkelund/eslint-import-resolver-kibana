# @elastic/eslint-import-resolver-kibana

Resolver for Kibana imports, meant to be used with [eslint-plugin-import](https://github.com/benmosher/eslint-plugin-import).

## Usage

Specify this resolver with the `import/resolver` setting in your eslint config file:

```yml
# .eslintrc.yml
settings:
  import/resolver: "@elastic/eslint-import-resolver-kibana"
```

## Settings

***NOTE:*** All relative paths are resolved as relative to the project root, which is determined by walking up from the first linted file and looking for a `package.json` file. If your project has multiple `package.json` files then make sure to specify the `rootPackageName` setting.

Property | Default | Description
-------- | ------- | -----------
rootPackageName | `null` | The `"name"` property of the root `package.json` file. If your project has multiple `package.json` files then specify this setting to tell the resolver which `package.json` file sits at the root of your project.
pluginPaths | `[]` if `rootPackageName` is set, otherwise `[.]` | Array of relative paths which contain a Kibana plugin. Plugins must contain a `package.json` file to be valid.
pluginDirs | `[]` | Array of relative paths pointing to directories which contain Kibana plugins. Plugins must contain a `package.json` file to be valid.

## Settings Usage
To specify additional config add a `:` after the resolver name and specify the argument as key-value pairs:

```yml
# .eslintrc.yml
settings:
  import/resolver:
    "@elastic/eslint-import-resolver-kibana":
      # if your project has multiple package.json files
      rootPackageName: my-project
      
      # if your project stores plugin source in sub directories you can specify
      # those directories via `pluginPaths`.
      pluginPaths:
        - ./plugin-one
        - ./plugin-two
        
      # if all of your plugins have the same parent directory you can specify
      # that directory and we will look for plugins there
      pluginDirs:
        - ./kibana-plugins
```

See [the resolvers docs](https://github.com/benmosher/eslint-plugin-import#resolvers) or the [resolver spec](https://github.com/benmosher/eslint-plugin-import/blob/master/resolvers/README.md#resolvesource-file-config---found-boolean-path-string-) for more details.

## Debugging

For debugging output from this resolver, run your linter with `DEBUG=eslint-plugin-import:resolver:kibana`.

This resolver defers to [*eslint-import-resolver-node*](https://www.npmjs.com/package/eslint-import-resolver-node) and [*eslint-import-resolver-webpack*](https://www.npmjs.com/package/eslint-import-resolver-webpack) for all of it's actual resolution logic. To get debugging output from all resolvers use `DEBUG=eslint-plugin-import:resolver:*`.
