
REPOSITORY_ROOT := $(PWD)

.PHONY : install

install: .poetry/bin/poetry
	$< install

.poetry/bin/poetry:
	@curl -sSL https://install.python-poetry.org | POETRY_HOME=$(REPOSITORY_ROOT)/$(shell basename $(dir $(abspath $(dir $(@))))) python3 -