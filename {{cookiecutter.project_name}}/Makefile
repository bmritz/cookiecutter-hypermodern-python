REQUIRED := python3
$(foreach bin,$(REQUIRED),\
    $(if $(shell command -v $(bin) 2> /dev/null),,$(error Please install `$(bin)`)))

REPOSITORY_ROOT := $(PWD)

help:           			## Show this help.
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'
 

.PHONY : install run-nox-all run-nox-session

install: .poetry/bin/poetry		## install all dependencies for development
	$< install
	NOXSESSION='pre-commit -- install' make run-nox-session

.poetry/bin/poetry:						## install poetry
	@curl -sSL https://install.python-poetry.org | POETRY_HOME=$(REPOSITORY_ROOT)/$(shell basename $(dir $(abspath $(dir $(@))))) python3 - --version=1.4.0

run-nox-all: .poetry/bin/poetry			## Run all nox sessions
	PATH=$$PATH:$(dir $<) $< run nox

run-nox-session: .poetry/bin/poetry guard-NOXSESSION			## Run a specific nox session. Call via something like NOXSESSION=tests-3.10 make run-nox-session
	PATH=$$PATH:$(dir $<) $< run nox -- -s $(NOXSESSION)

guard-%: .poetry/bin/poetry
	@if [ -z '${${*}}' ]; then echo 'Variable $* not set. You can set it with $*=VALUE make ...' && exit 1; fi