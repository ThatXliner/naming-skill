---
name: naming-cheatsheet
description: Rules for naming variables and functions, based on kettanaito's naming cheatsheet (S-I-D, the A/HC/LC pattern, standard action verbs and boolean prefixes). Use when writing new code, choosing or reviewing identifier names, renaming during a refactor, or when the user asks for a better name or says a name is unclear.
---

# Naming cheatsheet

Apply these rules whenever you name a variable, function, method, or field, and when you review names in a diff. The examples use JavaScript, but the rules apply to any language. For the full text with more examples, read [references/cheatsheet.md](references/cheatsheet.md).

## General rules

1. **Use English.** `firstName`, not `primerNombre`.
2. **Follow one naming convention.** Use the convention the codebase and language already use (`camelCase`, `snake_case`, ...). Do not mix them.
3. **Make names S-I-D:**
   - **Short**: quick to type and remember.
   - **Intuitive**: reads like normal speech. Avoid invented words like `isPaginatable` or `shouldPaginatize`.
   - **Descriptive**: says what it does or holds. Avoid `a`, `data`, `temp` for meaningful values.
4. **Do not use contractions.** `onItemClick`, not `onItmClk`.
5. **Do not repeat the context.** Inside `class MenuItem`, write `handleClick`, not `handleMenuItemClick`.
6. **Reflect the expected result.** Name the value for how it is used. Prefer `isDisabled = itemCount <= 3` passed to `disabled={isDisabled}` over `disabled={!isEnabled}`.
7. **Match singular and plural to the value.** `friend = 'Bob'`, `friends = ['Bob', 'Tony']`.

## Function names: the A/HC/LC pattern

```
prefix? + action (A) + high context (HC) + low context? (LC)
```

| Name                   | Prefix   | Action    | High context | Low context |
| ---------------------- | -------- | --------- | ------------ | ----------- |
| `getUser`              |          | `get`     | `User`       |             |
| `getUserMessages`      |          | `get`     | `User`       | `Messages`  |
| `handleClickOutside`   |          | `handle`  | `Click`      | `Outside`   |
| `shouldDisplayMessage` | `should` | `Display` | `Message`    |             |

Context order changes meaning. The high context is what the name is about: `shouldUpdateComponent` means *you* update the component; `shouldComponentUpdate` means the *component* updates itself and you control when.

State the domain a function operates on (`getRecentPosts(posts)`), unless the language makes it obvious (a JavaScript `filter` works on arrays, so `filterArray` is redundant).

## Actions (verbs)

| Verb      | Meaning                                                                                  | Example                         |
| --------- | ---------------------------------------------------------------------------------------- | ------------------------------- |
| `get`     | Access data, immediately or asynchronously.                                              | `getFruitCount()`, `getUser(id)` |
| `set`     | Assign a value declaratively, from `A` to `B`.                                           | `setFruits(5)`                  |
| `reset`   | Return a value to its initial state.                                                     | `resetFruits()`                 |
| `remove`  | Take something *from* somewhere. The thing still exists. Opposite of `add`.              | `removeFilter('price', filters)` |
| `delete`  | Erase something completely. Opposite of `create`.                                        | `deletePost(id)`                |
| `compose` | Create new data from existing data (strings, objects, functions).                        | `composePageUrl(name, id)`      |
| `handle`  | Respond to an action. Use for callbacks and event handlers.                              | `handleLinkClick`               |

To choose between `remove` and `delete`, look at the opposite: you `add` to a destination and `create` with no destination. Pair `remove` with `add`, and `delete` with `create`.

## Prefixes

| Prefix          | Meaning                                                              | Example                                  |
| --------------- | -------------------------------------------------------------------- | ---------------------------------------- |
| `is`            | A characteristic or state of the context (boolean).                  | `isBlue`, `isPresent`                    |
| `has`           | Whether the context has a value or state (boolean).                  | `hasProducts`, not `isProductsExist` or `areProductsPresent` |
| `should`        | A positive condition tied to an action (boolean).                    | `shouldUpdateUrl(url, expectedUrl)`      |
| `min` / `max`   | A lower or upper bound.                                              | `minPosts`, `maxPosts`                   |
| `prev` / `next` | The previous or next value in a state transition.                    | `prevPosts`, `nextPosts`                 |

## When you review names

For each name you choose or review, check:

- Can a reader tell what it holds or does without reading its body?
- Does a boolean start with `is`, `has`, or `should`, and is it phrased positively?
- Does a function name start with a verb from the table above, used with its exact meaning?
- Does the name repeat its enclosing class, module, or file?
- Is it plural if and only if it holds a collection?

When you rename, say what the old name got wrong in one short phrase (for example, "`data` → `unpaidInvoices`: says what the list holds").
