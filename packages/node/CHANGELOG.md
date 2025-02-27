# @pandacss/node

## 0.8.0

### Patch Changes

- 5d1d376b: Adding missing comma for generated panda config
- be0ad578: Fix parser issue with TS path mappings
- 78612d7f: Fix node evaluation in extractor process (can happen when using a BinaryExpression, simple CallExpression or
  conditions)
- Updated dependencies [3f1e7e32]
- Updated dependencies [fb449016]
- Updated dependencies [ac078416]
- Updated dependencies [e1f6318a]
- Updated dependencies [be0ad578]
- Updated dependencies [b75905d8]
- Updated dependencies [78612d7f]
- Updated dependencies [9ddf258b]
- Updated dependencies [0520ba83]
- Updated dependencies [156b6bde]
  - @pandacss/generator@0.8.0
  - @pandacss/core@0.8.0
  - @pandacss/extractor@0.8.0
  - @pandacss/parser@0.8.0
  - @pandacss/token-dictionary@0.8.0
  - @pandacss/config@0.8.0
  - @pandacss/types@0.8.0
  - @pandacss/error@0.8.0
  - @pandacss/is-valid-prop@0.8.0
  - @pandacss/logger@0.8.0
  - @pandacss/shared@0.8.0

## 0.7.0

### Patch Changes

- f4bb0576: Fix postcss issue where `@layer reset, base, tokens, recipes, utilities` check was too strict
- d8ebaf2f: Fix issue where hot module reloading is inconsistent in the PostCSS plugin when external files are changed
- 4ff7ddea: Fix issue where hot module reloading is inconsistent in the PostCSS plugin when another internal package is
  changed
- Updated dependencies [16cd3764]
- Updated dependencies [f2abf34d]
- Updated dependencies [f59154fb]
- Updated dependencies [a9c189b7]
- Updated dependencies [7bc69e4b]
- Updated dependencies [1a05c4bb]
  - @pandacss/parser@0.7.0
  - @pandacss/extractor@0.7.0
  - @pandacss/shared@0.7.0
  - @pandacss/generator@0.7.0
  - @pandacss/types@0.7.0
  - @pandacss/config@0.7.0
  - @pandacss/core@0.7.0
  - @pandacss/token-dictionary@0.7.0
  - @pandacss/error@0.7.0
  - @pandacss/is-valid-prop@0.7.0
  - @pandacss/logger@0.7.0

## 0.6.0

### Patch Changes

- 032c152a: Fix issue where `panda cssgen --outfile` doesn't extract files to chunks before bundling them into the css
  out file
- Updated dependencies [cd912f35]
- Updated dependencies [dc4e80f7]
- Updated dependencies [12c900ee]
- Updated dependencies [21295f2e]
- Updated dependencies [5bd88c41]
- Updated dependencies [ef1dd676]
- Updated dependencies [b50675ca]
  - @pandacss/generator@0.6.0
  - @pandacss/core@0.6.0
  - @pandacss/extractor@0.6.0
  - @pandacss/parser@0.6.0
  - @pandacss/config@0.6.0
  - @pandacss/types@0.6.0
  - @pandacss/token-dictionary@0.6.0
  - @pandacss/error@0.6.0
  - @pandacss/is-valid-prop@0.6.0
  - @pandacss/logger@0.6.0
  - @pandacss/shared@0.6.0

## 0.5.1

### Patch Changes

- 5b09ab3b: Add support for `--outfile` flag in the `cssgen` command.

  ```bash
  panda cssgen --outfile dist/styles.css
  ```

- 78ed6ed4: Fix issue where using a nested outdir like `src/styled-system` with a baseUrl like `./src` would result on
  parser NOT matching imports like `import { container } from "styled-system/patterns";` cause it would expect the full
  path `src/styled-system`
- e48b130a: - Remove `stack` from `box.toJSON()` so that generated JSON files have less noise, mostly useful to get make
  the `panda debug` command easier to read

  - Also use the `ParserResult.toJSON()` method on `panda debug` command for the same reason

  instead of:

  ```json
  [
    {
      "type": "map",
      "value": {
        "padding": {
          "type": "literal",
          "value": "25px",
          "node": "StringLiteral",
          "stack": [
            "CallExpression",
            "ObjectLiteralExpression",
            "PropertyAssignment",
            "Identifier",
            "Identifier",
            "VariableDeclaration",
            "StringLiteral"
          ],
          "line": 10,
          "column": 20
        },
        "fontSize": {
          "type": "literal",
          "value": "2xl",
          "node": "StringLiteral",
          "stack": [
            "CallExpression",
            "ObjectLiteralExpression",
            "PropertyAssignment",
            "ConditionalExpression"
          ],
          "line": 11,
          "column": 67
        }
      },
      "node": "CallExpression",
      "stack": [
        "CallExpression",
        "ObjectLiteralExpression"
      ],
      "line": 11,
      "column": 21
    },
  ```

  we now have:

  ```json
  {
    "css": [
      {
        "type": "object",
        "name": "css",
        "box": {
          "type": "map",
          "value": {},
          "node": "CallExpression",
          "line": 15,
          "column": 27
        },
        "data": [
          {
            "alignItems": "center",
            "backgroundColor": "white",
            "border": "1px solid black",
            "borderRadius": "8px",
            "display": "flex",
            "gap": "16px",
            "p": "8px",
            "pr": "16px"
          }
        ]
      }
    ],
    "cva": [],
    "recipe": {
      "checkboxRoot": [
        {
          "type": "recipe",
          "name": "checkboxRoot",
          "box": {
            "type": "map",
            "value": {},
            "node": "CallExpression",
            "line": 38,
            "column": 47
          },
          "data": [
            {}
          ]
        }
      ],
  ```

- 1a2c0e2b: Fix `panda.config.xxx` file dependencies detection when using the builder (= with PostCSS or with the VSCode
  extension). It will now also properly resolve tsconfig path aliases.
- Updated dependencies [6f03ead3]
- Updated dependencies [8c670d60]
- Updated dependencies [33198907]
- Updated dependencies [53fb0708]
- Updated dependencies [c0335cf4]
- Updated dependencies [762fd0c9]
- Updated dependencies [f9247e52]
- Updated dependencies [1ed239cd]
- Updated dependencies [09ebaf2e]
- Updated dependencies [78ed6ed4]
- Updated dependencies [e48b130a]
- Updated dependencies [1a2c0e2b]
- Updated dependencies [b8f8c2a6]
- Updated dependencies [a3d760ce]
- Updated dependencies [d9bc63e7]
  - @pandacss/extractor@0.5.1
  - @pandacss/types@0.5.1
  - @pandacss/config@0.5.1
  - @pandacss/generator@0.5.1
  - @pandacss/shared@0.5.1
  - @pandacss/logger@0.5.1
  - @pandacss/core@0.5.1
  - @pandacss/parser@0.5.1
  - @pandacss/token-dictionary@0.5.1
  - @pandacss/error@0.5.1
  - @pandacss/is-valid-prop@0.5.1

## 0.5.0

### Patch Changes

- Updated dependencies [60df9bd1]
- Updated dependencies [30f41e01]
- Updated dependencies [ead9eaa3]
  - @pandacss/shared@0.5.0
  - @pandacss/parser@0.5.0
  - @pandacss/extractor@0.5.0
  - @pandacss/generator@0.5.0
  - @pandacss/types@0.5.0
  - @pandacss/core@0.5.0
  - @pandacss/token-dictionary@0.5.0
  - @pandacss/config@0.5.0
  - @pandacss/error@0.5.0
  - @pandacss/is-valid-prop@0.5.0
  - @pandacss/logger@0.5.0

## 0.4.0

### Patch Changes

- Updated dependencies [8991b1e4]
- Updated dependencies [2a1e9386]
- Updated dependencies [54a8913c]
- Updated dependencies [c7b42325]
- Updated dependencies [a48e5b00]
- Updated dependencies [5b344b9c]
  - @pandacss/parser@0.4.0
  - @pandacss/core@0.4.0
  - @pandacss/is-valid-prop@0.4.0
  - @pandacss/generator@0.4.0
  - @pandacss/types@0.4.0
  - @pandacss/config@0.4.0
  - @pandacss/token-dictionary@0.4.0
  - @pandacss/error@0.4.0
  - @pandacss/extractor@0.4.0
  - @pandacss/logger@0.4.0
  - @pandacss/shared@0.4.0

## 0.3.2

### Patch Changes

- Updated dependencies [9822d79a]
  - @pandacss/config@0.3.2
  - @pandacss/core@0.3.2
  - @pandacss/error@0.3.2
  - @pandacss/extractor@0.3.2
  - @pandacss/generator@0.3.2
  - @pandacss/is-valid-prop@0.3.2
  - @pandacss/logger@0.3.2
  - @pandacss/parser@0.3.2
  - @pandacss/shared@0.3.2
  - @pandacss/token-dictionary@0.3.2
  - @pandacss/types@0.3.2

## 0.3.1

### Patch Changes

- efd79d83: Baseline release for the launch
- Updated dependencies [efd79d83]
  - @pandacss/config@0.3.1
  - @pandacss/core@0.3.1
  - @pandacss/error@0.3.1
  - @pandacss/extractor@0.3.1
  - @pandacss/generator@0.3.1
  - @pandacss/is-valid-prop@0.3.1
  - @pandacss/logger@0.3.1
  - @pandacss/parser@0.3.1
  - @pandacss/shared@0.3.1
  - @pandacss/token-dictionary@0.3.1
  - @pandacss/types@0.3.1

## 0.3.0

### Patch Changes

- b8ab0868: Fix white space when updating the `.gitignore` file
- Updated dependencies [6d81ee9e]
  - @pandacss/generator@0.3.0
  - @pandacss/parser@0.3.0
  - @pandacss/types@0.3.0
  - @pandacss/config@0.3.0
  - @pandacss/core@0.3.0
  - @pandacss/token-dictionary@0.3.0
  - @pandacss/error@0.3.0
  - @pandacss/extractor@0.3.0
  - @pandacss/is-valid-prop@0.3.0
  - @pandacss/logger@0.3.0
  - @pandacss/shared@0.3.0

## 0.0.2

### Patch Changes

- fb40fff2: Initial release of all packages

  - Internal AST parser for TS and TSX
  - Support for defining presets in config
  - Support for design tokens (core and semantic)
  - Add `outExtension` key to config to allow file extension options for generated javascript. `.js` or `.mjs`
  - Add `jsxElement` option to patterns, to allow specifying the jsx element rendered by the patterns.

- Updated dependencies [c308e8be]
- Updated dependencies [fb40fff2]
  - @pandacss/config@0.0.2
  - @pandacss/types@0.0.2
  - @pandacss/core@0.0.2
  - @pandacss/error@0.0.2
  - @pandacss/extractor@0.0.2
  - @pandacss/generator@0.0.2
  - @pandacss/is-valid-prop@0.0.2
  - @pandacss/logger@0.0.2
  - @pandacss/parser@0.0.2
  - @pandacss/shared@0.0.2
  - @pandacss/token-dictionary@0.0.2
