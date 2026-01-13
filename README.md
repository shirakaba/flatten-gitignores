# `flatten-gitignores`

A simple Node.js tool for flattening nested `.gitignore` files into a single file.

Useful for supporting tools that expect a single ignore file and don't resolve nested ignore files (e.g. EAS expects `.easignore` and Prettier expects `.prettierignore`).

## Usage

Run the script with Node, passing optional flags to customize input, output, additions, and excludes.

```sh
npx flatten-gitignores [--ignore-file] [--cwd <path>] [--output <file>] [--prepend <path>] [--append <path>] [--exclude <glob> ...] [--no-default-excludes] [--help]
```

### Flags

- `--ignore-file <file>`: The ignore file name to search for. Defaults to `.gitignore`.
- `--cwd <path>`: The search root / working directory; defaults to current CWD (`.`).
- `--output <file>`: Output file path; defaults to `<cwd>/.gitignore-collated`.
- `--prepend <path>`: Path to an additional ignore file to prepend. Resolved relative to CWD.
- `--append <path>`: Path to an additional ignore file to append. Resolved relative to CWD.
- `--exclude <glob>`: Glob pattern(s) to exclude from the search for ignore files. Defaults to `**/node_modules/**`. Pass one or more `--exclude` flags to add more. To omit the defaults, pass `--no-default-excludes`.
- `--no-default-excludes`: Omit the default excludes (`**/node_modules/**`).
- `--help`: Show help and exit.

### Examples

- Default behavior:
	```sh
	npx flatten-gitignores
	```
  - Collates all `.gitignore` files found into a `.gitignore-collated` file in the current directory.

- Specify output file (`--output`):
	```sh
	npx flatten-gitignores --output ./.easignore
	```
  - Collates all `.gitignore` files found into a `.easignore` file in the current directory.

- Exclude certain files from the search for ignore files (`--exclude`):
	```sh
	npx flatten-gitignores --exclude **/dist/** --exclude **/build/**
	```
  - Collates all `.gitignore` files found into a `.easignore` file in the current directory.
  - `--exclude`: Excludes `**/dist/**` and `**/build/**` from the search. Useful for reducing needless search time.

- Stop excluding `node_modules` from the search (`--no-default-excludes`):
	```sh
	npx flatten-gitignores --no-default-excludes
	```
  - Collates all `.gitignore` files found into a `.easignore` file in the current directory.
  - `--no-default-excludes`: Stops excluding `**/node_modules/**` (I can't think of a practical use-case for this, but just in case you need it!).

- Prepend (`--prepend`) or append (`--append`) extra rules:
	```sh
	npx flatten-gitignores --output ./.easignore --prepend .easignore-prepend --append .easignore-append
	```
  - Collates all `.gitignore` files found into a `.easignore` file in the current directory.
  - `--prepend`: Prepends the contents of `.easignore-prepend` into that `.easignore` file.
  - `--append`: Appends the contents of `.easignore-append` into that `.easignore` file.

- Collate a file other than `.gitignore` (`--ignore-file`):
	```sh
	npx flatten-gitignores --ignore-file _gitignore
	```
  - Collates all `_gitignore` files found into a `.gitignore-collated` file in the current directory (possibly useful for ecosystems like npm, which do not support bundling a `.gitignore` file into your npm package, so people have to work around it with a `_gitignore` file or similar that they rename to `.gitignore` after unpacking).
