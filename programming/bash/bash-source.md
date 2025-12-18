# Bash Source

## What is it?
`source`is reading and running another file in the same shell process.
- Variables are shared
- Functions are shared
- No new shell is started

## Examples
```bash
source ./logging.sh

# or

. ./logging.sh
``` 

## Example structure

project/ <br>
├── bin/ -> executable binaries/scripts<br>
│   └── tool -> Entry point<br> 
├── lib/ <br>
├── tests/ <br>
│   └── tool.bats <br>
├── Makefile <br>
└── README.md
 

## Tool example

Use tool without file extention so we can call it tool<br>
`project/bin/tool`

```bash
#!/bin/bash
set -euo pipefail

BASE_DIR="$(cd "$(dirname "$0")" && pwd)"

source "$BASE_DIR/lib/logging.sh"
source "$BASE_DIR/lib/args.sh"
source "$BASE_DIR/lib/filesystem.sh"

main() {
    parseArgs "$@"
    info "Tool started"
    processFiles
}

main "$@"
```


`$0` is the name of the current script. 

## Makefile

```Makefile
.PHONY: test lint install

lint:
	shellcheck bin/tool lib/*.sh

test:
	bats tests

install:
	install -m 0755 bin/tool /usr/local/bin/tool
```






