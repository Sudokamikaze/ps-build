LIST = $(wildcard *.yml)
targets =$(patsubst %.yml, %, $(LIST))
test-targets =$(addprefix percona-server-5.7-, $(filter-out view, $(targets)))

all: $(targets)

$(targets):
	jenkins-jobs -s ps.cd update $@.yml
	@echo

test: $(test-targets)

$(test-targets):
	@mkdir -p result/$@
	jenkins-jobs -s ps.cd test $(patsubst percona-server-5.7-%,%, $@).yml -o result/$@
	@mv result/$@/percona-server-* result/$@/config.xml
	@echo
