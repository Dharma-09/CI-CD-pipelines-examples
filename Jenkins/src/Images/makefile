SHELL := /bin/bash
CURRENT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

.PHONY: *
default: test clean
	@:

test:
	@# script is in DevOps Bash tools repo, clone whole repo for dependency lib and put it in the $PATH
	check_groovyc.sh

push:
	git push

clean:
	@#echo "Removing .class files"
	find . -name '*.class' -exec rm {} \;

wc:
	git ls-files Jenkinsfile vars/ | xargs wc -l

sync:
	. .envrc; github_repo_fork_sync.sh
