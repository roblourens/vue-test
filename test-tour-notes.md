- No out-of-the-box support
  - Extensions contribute multiple language definitions, how are they working together?
  - Syntax highlighting for .vue components (Microsoft/vscode#24295).
  - Extension recommendations (Microsoft/vscode#24538).

- Configure build task
  - Could not configure problem matcher for vue-starter-kit (Microsoft/vscode#24260).
  - Works AS-IS with template from the vue-cli.

- Debugging
  - Needs source map override to work with Webpack (Microsoft/vscode-chrome-debug#315).
  - Breakpoints not enabled for .vue files by Vetur extension (octref/vetur#116).

- IntelliSense
  - Working for non-JavaScript parts in .vue components.
  - No IntelliSense for JavaScript parts that use implied types, like components.
    - Work around with type declared in comment failed (Microsoft/vscode#24285).
    - Maybe extension could supply type to TS server (Microsoft/vscode#24536)
