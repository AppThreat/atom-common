# atom-common

A lightweight Node.js utility library providing file system traversal helpers and runtime environment detectors.

## Installation

```bash
npm install @appthreat/atom-common
# or
yarn add @appthreat/atom-common
```

## Usage

```javascript
import { getAllFiles, detectJava, detectRuby } from "@appthreat/atom-common";

// 1. Recursively get all .js files in a directory
const jsFiles = getAllFiles("./src", ".js");
console.log(jsFiles);

// 2. Check if runtimes are available
if (detectJava()) {
  console.log("Java is installed!");
}

if (detectRuby("3.4.x")) {
  console.log("Ruby 3.4.x is installed!");
}
```

## API Reference

### File System Utilities

#### `getAllFiles(dir, extn, ...args)`

Recursively scans a directory for files with a specific extension. It automatically ignores `node_modules`, dotfiles (hidden files), and specific directories defined in the configuration.

- **dir** `(string)`: The root directory to start scanning.
- **extn** `(string)`: The file extension to look for (e.g., `.js`, `.ts`).
- **ignore_node_modules** `(boolean)`: Defaults to `true`.

**Returns:** An array of file paths.

### Runtime Detection Utilities

These functions spawn a child process to check version flags. They return `true` if the runtime is found and exits successfully, otherwise `false`.

- **`detectJava()`**: Checks for `java`.
- **`detectPhp()`**: Checks for `php`.
- **`detectScala()`**: Checks for `scala`.
- **`detectScalac()`**: Checks for the Scala compiler `scalac`.
- **`detectRuby(versionNeeded)`**: Checks for `ruby`.
  - _versionNeeded_ (optional): A string (e.g., `"3.4.7"`, `"3.4.x"`, `"4.0.x"`). If provided, verifies the installed version matches.

## Configuration

You can configure the behavior of the utilities using Environment Variables.

### File Ignoring

| Variable                     | Description                                          | Default                                               |
| :--------------------------- | :--------------------------------------------------- | :---------------------------------------------------- |
| `ASTGEN_IGNORE_DIRS`         | CSV string of directory names to ignore during scan. | `venv, docs, e2e, cypress, node_modules` (and others) |
| `ASTGEN_IGNORE_FILE_PATTERN` | Regex string for files to ignore.                    | `(three\|\.d)\.(js\|ts\|jsx\|tsx)$`                   |

### Custom Binary Paths

If your binaries are not in the global system PATH, you can override the commands used for detection:

| Variable     | Description           | Default  |
| :----------- | :-------------------- | :------- |
| `JAVA_CMD`   | Command to run Java   | `java`   |
| `PHP_CMD`    | Command to run PHP    | `php`    |
| `RUBY_CMD`   | Command to run Ruby   | `ruby`   |
| `SCALA_CMD`  | Command to run Scala  | `scala`  |
| `SCALAC_CMD` | Command to run Scalac | `scalac` |

## License

MIT
