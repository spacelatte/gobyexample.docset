#!/usr/bin/env make

INDEX := ./Resources/docSet.dsidx

index: $(INDEX)

update:
	git submodule foreach --recursive git pull

clean:
	rm -vf "$(INDEX)"

define DB_INIT
CREATE TABLE searchIndex(id INTEGER PRIMARY KEY, name TEXT, type TEXT, path TEXT);
CREATE UNIQUE INDEX anchor ON searchIndex (name, type, path);
endef

export DB_INIT

$(INDEX): ./Resources/gobyexample.git/examples.txt
	echo "$${DB_INIT}" | sqlite3 "$@"
	cat '$<' \
	| while read line; do \
		filtered="$$(echo "$$line" | tr -d '[:punct:]' | tr '[:upper:]' '[:lower:]' | tr '[:blank:]' '-' )"; \
		echo "INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES ('$${line//\'/''}', 'Guide', '$$filtered');"; \
	done \
	| sqlite3 "$@"

