---
name: coding-style
description: General code style advice. Use when writing any code, reviewing code for style consistency, or when the user asks to follow the coding style guide.
---

# Apply Coding Style

## General

- Use American English spelling for both code and user-facing text.
- Use sentence case for all user-facing text.
- Keep comments sparse and useful. Use them to explain why, not to narrate what the code already says.

## Code structure

- Functions should always be defined below where they are used in the same file, so control flow reads from top to bottom.
- Functions should contain roughly a single level of abstraction. For example, a function that fetches data from an API should not be dealing with low-level HTTP request details, and a function that handles low-level HTTP requests should not be concerned with how the data is used after it is fetched.
- Prefer method chaining (for example, `map`/`filter`) over explicit loops. However, do not use `reduce`/`aggregate`; use an explicit loop instead when a fold is needed.
- Lean on available native methods, helper methods, and library functions and their behavior, rather than writing custom implementations. For example, if a library function throws an argument error when given an invalid input, don't check for that invalid input and throw your own error. Instead, let the library function throw the error and handle it appropriately.
- Use blank lines to separate logical sections of code within functions for better readability.
- If a file grows over 500 lines, consider splitting it into multiple smaller files.

## Common code style

- Early returns should only appear at the top of functions, and should have simple conditions. Otherwise, avoid returns scattered at varying depths; structure the function with if/else branches so that all non-early returns occur at the same nesting depth (ideally as the final statement of each branch).
- Lean on structured programming, and avoid goto-like control flow like `break`, `continue`, and `return` statements in the middle of loops where possible.
- Constants should be named like regular variables, not in all caps.

## C# style

- Use immutable `record`s for data classes instead of `class` when possible.
- Prefer `{ get; init; }` properties in records with many properties or optional properties.

## TypeScript style

- Prefer `let` over `const`.
- Use double equals (`==`) for equality checks unless type coercion makes it necessary to use triple equals (`===`).

## StyleMap

This only applies when using the `stylemap` NPM package for styling.
- Put all `stylemap` `style`s at the end of the file.
- Avoid `Style` suffix in style names unless necessary for clarity or to avoid naming conflicts.
- Follow SMACSS naming conventions for names:
  - Styles for major page layout components are prefixed with `l-`.
  - Modules/Component names are camelCase and sub-components are separated with a single dash (`-`).
  - State styles that modify the appearance based on user interaction or other conditions are prefixed with `is-` and suffixed with `-state` in the form `is-componentName-state`.

## Tests
- Tests should focus on inputs and outputs rather than internal implementation details.
- Prefer real classes or fake implementations over mocks.
- When desired behavior changes, test for the new behavior, but avoid testing that the old behavior no longer exists.

## EasyAssertions

This applies to C# tests using the EasyAssertions library.
- Chain assertions with `.And` and `.And()` where possible.
- `.And` should always be used immediately for an assertion and never stored in a variable. It should be on the same line as the assertion it is chaining to.
- One assertion per line. e.g.
  ```csharp
  // Chained assertions over multiple lines
  _sut.GetTextCollectionProvider(_packageName, CancellationToken.None)
      .ShouldComplete()
      .And.ShouldBeA<DataSourceGeneratedSettingTextCollectionProvider>()
      .And.TextCollection(CultureInfo.GetCultureInfo("en-US")).Get("TestLabel").ShouldBe("Package label");
  
  // Single short assertion can be on one line
  _sut.Version.ShouldBe("1.0.0");
  ```