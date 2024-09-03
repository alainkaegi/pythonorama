# Style Guide
This is the style guide for this repository.

- Use the second voice (“you”).
- Capitalize every word of titles except for conjunctions, articles, two-letter prepositions, and the word “for” (mnemonic: “CAP4”). Examples:
  - “Asymptotic Notation” (rather than “Asymptotic notation”)
  - ”Getters and Setters” (rather than “Getters and setters or “Getters And Setters”)
- Backtick Python expressions embedded in the text. Example:
  - The Python expression `(2 + 3) * 4` evaluates to `20`
- Avoid unnecessary empty lines and trailing spaces
- Let markdown applications autonumber items in ordered lists
- Code snippets
  - Add `python` next to the backticks in fenced python code blocks.
  - Follow [Python's style guide](https://peps.python.org/pep-0008/]). In particular:
    - Use 4 spaces per indentation level
  - Use single quotes (') as a delimiter for strings by default.
  - Backtick text-embedded names referring to symbols (e.g., class, variable, and function names) appearing in code snippets. Example:
    - Class `Foo` contains instance variable `bar`
  - Omit the parentheses when referring to a function. Example:
    - The class also defines function `baz`
- Application menus
  - Use a greater-than sign (“>”) to separate cascading menu elements. Example:
    - `File` > `New File...`
- Keyboard shortcuts
  - Use lowercase letters, dash as a separator
  - Enclose in backticks
  - Use conventional key designations (e.g., `ctrl`, `cmd`, `alt`, `shift`)
- Drawings
  - Use `draw.io`
  - Collect multiple, related drawings in one `.drawio` file
  - Select a given figure to export as an `.svg` file
    1. Select the figure
    2. `File` > `Export as` > `SVG...`
    3. `Selection Only`
    4. `Appearance:` “Light”
    5. `Do not include a copy of my diagram`
    6. `Export`
