# recall-nodejs

A command-line note-taking app built with Node.js. This project was built to practise and recall core Node.js concepts.

## What I Learned

### Node.js Core Modules
- **`fs/promises`** – Reading and writing JSON files asynchronously using `fs.readFile` and `fs.writeFile` as a lightweight file-based database (`db.json`).
- **`http`** – Creating an HTTP server from scratch with `http.createServer`, setting response headers, and sending HTML responses.
- **`url` / `fileURLToPath`** – Resolving file paths relative to the current ES module using `import.meta.url` (the ES module equivalent of `__dirname`).

### ES Modules
- Using `"type": "module"` in `package.json` to enable ES module syntax (`import`/`export`) throughout the project.
- Using dynamic `import()` inside tests to support Jest module mocking with `jest.unstable_mockModule`.

### CLI Development with Yargs
- Defining sub-commands (`new`, `all`, `find`, `remove`, `web`, `clean`) with `.command()`.
- Accepting positional arguments and named options (e.g. `--tags` / `-t`).
- Making the CLI executable via the `bin` field in `package.json` and a `#!/usr/bin/env node` shebang.

### Async/Await
- Writing async helper functions for all database operations (`getDB`, `saveDB`, `insertDB`).
- Using `await` in command handlers so the process stays alive until I/O completes.

### HTML Templating (No Framework)
- Rendering HTML dynamically with a simple `interpolate` function that replaces `{{ placeholder }}` tokens in a static HTML template file.
- Building HTML strings from an array of note objects with `Array.map` and `Array.join`.

### Opening the Browser Programmatically
- Using the [`open`](https://github.com/sindresorhus/open) package to launch the default browser pointing at the local server after it starts.

### Testing with Jest
- Writing unit tests for pure business-logic functions (`newNote`, `getAllNotes`, `removeNote`).
- Mocking ES modules with `jest.unstable_mockModule` to isolate the notes module from the real file-system database.
- Configuring Jest to work with ES modules via `--experimental-vm-modules`.

---

## Project Structure

```
recall-nodejs/
├── src/
│   ├── command.js     # Yargs CLI command definitions
│   ├── notes.js       # Note CRUD logic
│   ├── db.js          # File-system database helpers
│   ├── server.js      # HTTP server & HTML rendering
│   └── template.html  # HTML template for the web view
├── tests/
│   └── notes.test.js  # Jest unit tests
├── basic-server.js    # Minimal "Hello World" HTTP server (learning example)
├── db.json            # JSON file used as the database
├── index.js           # CLI entry point
└── package.json
```

## Usage

### Install dependencies
```bash
npm install
```

### CLI commands

| Command | Description |
|---|---|
| `note new <note> [--tags tag1,tag2]` | Create a new note with optional tags |
| `note all` | List all notes |
| `note find <filter>` | Find notes whose content matches a filter |
| `note remove <id>` | Remove a note by its ID |
| `note web [port]` | Open notes in the browser (default port: 5000) |
| `note clean` | Delete all notes |

### Run the web interface
```bash
npm start
```

### Run tests
```bash
npm test
```
