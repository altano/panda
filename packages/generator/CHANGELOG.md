# @pandacss/generator

## 0.8.0

### Minor Changes

- 9ddf258b: Introduce the new `{fn}.raw` method that allows for a super flexible usage and extraction :tada: :

  ```tsx
  <Button rootProps={css.raw({ bg: "red.400" })} />

  // recipe in storybook
  export const Funky: Story = {
  	args: button.raw({
  		visual: "funky",
  		shape: "circle",
  		size: "sm",
  	}),
  };

  // mixed with pattern
  const stackProps = {
    sm: stack.raw({ direction: "column" }),
    md: stack.raw({ direction: "row" })
  }

  stack(stackProps[props.size]))
  ```

### Patch Changes

- 3f1e7e32: Adds the `{recipe}.raw()` in generated runtime
- ac078416: Fix issue with extracting nested tokens as color-palette. Fix issue with extracting shadow array as a
  separate unnamed block for the custom dark condition.
- be0ad578: Fix parser issue with TS path mappings
- b75905d8: Improve generated react jsx types to remove legacy ref. This fixes type composition issues.
- 0520ba83: Refactor generated recipe js code
- 156b6bde: Fix issue where generated package json does not respect `outExtension` when `emitPackage` is `true`
- Updated dependencies [fb449016]
- Updated dependencies [ac078416]
- Updated dependencies [be0ad578]
  - @pandacss/core@0.8.0
  - @pandacss/token-dictionary@0.8.0
  - @pandacss/types@0.8.0
  - @pandacss/is-valid-prop@0.8.0
  - @pandacss/logger@0.8.0
  - @pandacss/shared@0.8.0

## 0.7.0

### Patch Changes

- a9c189b7: Fix issue where `splitVariantProps` in cva doesn't resolve the correct types
- Updated dependencies [f59154fb]
- Updated dependencies [a9c189b7]
  - @pandacss/shared@0.7.0
  - @pandacss/types@0.7.0
  - @pandacss/core@0.7.0
  - @pandacss/token-dictionary@0.7.0
  - @pandacss/is-valid-prop@0.7.0
  - @pandacss/logger@0.7.0

## 0.6.0

### Patch Changes

- cd912f35: Fix `definePattern` module overriden type, was missing an `extends` constraint which lead to a type error:

  ```
  styled-system/types/global.d.ts:14:58 - error TS2344: Type 'T' does not satisfy the constraint 'PatternProperties'.

  14   export function definePattern<T>(config: PatternConfig<T>): PatternConfig
                                                              ~

    styled-system/types/global.d.ts:14:33
      14   export function definePattern<T>(config: PatternConfig<T>): PatternConfig
                                         ~
      This type parameter might need an `extends PatternProperties` constraint.

  ```

- dc4e80f7: Export `isCssProperty` helper function from styled-system/jsx
- 5bd88c41: Fix JSX recipe extraction when multiple recipes were used on the same component, ex:

  ```tsx
  const ComponentWithMultipleRecipes = ({ variant }) => {
    return (
      <button className={cx(pinkRecipe({ variant }), greenRecipe({ variant }), blueRecipe({ variant }))}>Hello</button>
    )
  }
  ```

  Given a `panda.config.ts` with recipes each including a common `jsx` tag name, such as:

  ```ts
  recipes: {
      pinkRecipe: {
          name: 'pinkRecipe',
          jsx: ['ComponentWithMultipleRecipes'],
          base: { color: 'pink.100' },
          variants: {
              variant: {
              small: { fontSize: 'sm' },
              },
          },
      },
      greenRecipe: {
          name: 'greenRecipe',
          jsx: ['ComponentWithMultipleRecipes'],
          base: { color: 'green.100' },
          variants: {
              variant: {
              small: { fontSize: 'sm' },
              },
          },
      },
      blueRecipe: {
          name: 'blueRecipe',
          jsx: ['ComponentWithMultipleRecipes'],
          base: { color: 'blue.100' },
          variants: {
              variant: {
              small: { fontSize: 'sm' },
              },
          },
      },
  },
  ```

  Only the first matching recipe would be noticed and have its CSS generated, now this will properly generate the CSS
  for each of them

- ef1dd676: Fix issue where `staticCss` did not generate all variants in the array of `css` rules
- b50675ca: Refactor parser to support extracting `css` prop in JSX elements correctly.
- Updated dependencies [12c900ee]
- Updated dependencies [5bd88c41]
- Updated dependencies [ef1dd676]
- Updated dependencies [b50675ca]
  - @pandacss/core@0.6.0
  - @pandacss/types@0.6.0
  - @pandacss/token-dictionary@0.6.0
  - @pandacss/is-valid-prop@0.6.0
  - @pandacss/logger@0.6.0
  - @pandacss/shared@0.6.0

## 0.5.1

### Patch Changes

- 53fb0708: Fix `config.staticCss` by filtering types on getPropertyKeys

  It used to throw because of them:

  ```bash
  <css input>:33:21: Missed semicolon
   ELIFECYCLE  Command failed with exit code 1.
  ```

  ```css
  @layer utilities {
      .m_type\:Tokens\[\"spacing\"\] {
          margin: type:Tokens["spacing"]
      }
  }
  ```

- 1ed239cd: Add feature where `config.staticCss.recipes` can now use [`*`] to generate all variants of a recipe.

  before:

  ```ts
  staticCss: {
    recipes: {
      button: [{ size: ['*'], shape: ['*'] }]
    }
  }
  ```

  now:

  ```ts
  staticCss: {
    recipes: {
      button: ['*']
    }
  }
  ```

- 78ed6ed4: Fix issue where using a nested outdir like `src/styled-system` with a baseUrl like `./src` would result on
  parser NOT matching imports like `import { container } from "styled-system/patterns";` cause it would expect the full
  path `src/styled-system`
- b8f8c2a6: Fix reset.css (generated when config has `preflight: true`) import order, always place it first so that it
  can be easily overriden
- Updated dependencies [8c670d60]
- Updated dependencies [c0335cf4]
- Updated dependencies [762fd0c9]
- Updated dependencies [f9247e52]
- Updated dependencies [1ed239cd]
- Updated dependencies [78ed6ed4]
  - @pandacss/types@0.5.1
  - @pandacss/shared@0.5.1
  - @pandacss/logger@0.5.1
  - @pandacss/core@0.5.1
  - @pandacss/token-dictionary@0.5.1
  - @pandacss/is-valid-prop@0.5.1

## 0.5.0

### Minor Changes

- ead9eaa3: Add support for tagged template literal version.

  This features is pure css approach to writing styles, and can be a great way to migrate from styled-components and
  emotion.

  Set the `syntax` option to `template-literal` in the panda config to enable this feature.

  ```js
  // panda.config.ts
  export default defineConfig({
    //...
    syntax: 'template-literal',
  })
  ```

  > For existing projects, you might need to run the `panda codegen --clean`

  You can also use the `--syntax` option to specify the syntax type when using the CLI.

  ```sh
  panda init -p --syntax template-literal
  ```

  To get autocomplete for token variables, consider using the
  [CSS Var Autocomplete](https://marketplace.visualstudio.com/items?itemName=phoenisx.cssvar) extension.

### Patch Changes

- Updated dependencies [60df9bd1]
- Updated dependencies [ead9eaa3]
  - @pandacss/shared@0.5.0
  - @pandacss/types@0.5.0
  - @pandacss/core@0.5.0
  - @pandacss/token-dictionary@0.5.0
  - @pandacss/is-valid-prop@0.5.0
  - @pandacss/logger@0.5.0

## 0.4.0

### Minor Changes

- 5b344b9c: Add support for disabling shorthand props

  ```ts
  import { defineConfig } from '@pandacss/dev'

  export default defineConfig({
    // ...
    shorthands: false,
  })
  ```

### Patch Changes

- 54a8913c: Fix issue where patterns that include css selectors doesn't work in JSX
- a48e5b00: Add support for watch mode in codegen command via the `--watch` or `-w` flag.

  ```bash
  panda codegen --watch
  ```

- Updated dependencies [2a1e9386]
- Updated dependencies [54a8913c]
- Updated dependencies [c7b42325]
- Updated dependencies [5b344b9c]
  - @pandacss/core@0.4.0
  - @pandacss/is-valid-prop@0.4.0
  - @pandacss/types@0.4.0
  - @pandacss/token-dictionary@0.4.0
  - @pandacss/logger@0.4.0
  - @pandacss/shared@0.4.0

## 0.3.2

### Patch Changes

- @pandacss/core@0.3.2
- @pandacss/is-valid-prop@0.3.2
- @pandacss/logger@0.3.2
- @pandacss/shared@0.3.2
- @pandacss/token-dictionary@0.3.2
- @pandacss/types@0.3.2

## 0.3.1

### Patch Changes

- efd79d83: Baseline release for the launch
- Updated dependencies [efd79d83]
  - @pandacss/core@0.3.1
  - @pandacss/is-valid-prop@0.3.1
  - @pandacss/logger@0.3.1
  - @pandacss/shared@0.3.1
  - @pandacss/token-dictionary@0.3.1
  - @pandacss/types@0.3.1

## 0.3.0

### Minor Changes

- 6d81ee9e: - Set default jsx factory to 'styled'
  - Fix issue where pattern JSX was not being generated correctly when properties are not defined

### Patch Changes

- Updated dependencies [6d81ee9e]
  - @pandacss/types@0.3.0
  - @pandacss/core@0.3.0
  - @pandacss/token-dictionary@0.3.0
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
  - @pandacss/types@0.0.2
  - @pandacss/core@0.0.2
  - @pandacss/is-valid-prop@0.0.2
  - @pandacss/logger@0.0.2
  - @pandacss/shared@0.0.2
  - @pandacss/token-dictionary@0.0.2
