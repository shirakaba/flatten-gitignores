# flatten-gitignores

A simple Node.js tool for flattening nested `.gitignore` files into a single file.

## Usage

Run the script with Node, passing optional flags to customize input, output, additions, and excludes.

```
node index.js [--input <path>] [--output <file>] [--additions <filename>] [--exclude <glob> ...] [--help]
```

### Flags

- `--input <path>`: Root directory to search for `.gitignore` files. Defaults to the current working directory.
- `--output <file>`: Output file path for the flattened ignore. Defaults to `.flattened-ignore` in the input path.
- `--additions <filename>`: Optional additions file name to include (e.g., `.prettierignore-additions`). If not provided, no additions file is searched.
- `--exclude <glob>`: Glob pattern(s) to exclude from the search. Can be passed multiple times. Defaults to `**/node_modules/**`.
- `--help`: Show help and exit.

### Examples

- Default behavior (current dir, output to `.flattened-ignore`, default excludes):
	```sh
	node index.js
	```

- Specify input folder and output file:
	```sh
	node index.js --input ./packages/app --output ./packages/app/.flattened-ignore
	```

- Include a custom additions file and multiple excludes:
	```sh
	node index.js --additions .prettierignore-additions --exclude "**/dist/**" --exclude "**/build/**"
	```
