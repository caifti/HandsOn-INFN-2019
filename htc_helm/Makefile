RELEASE = dodasts
CHART_NAME = helm-chart_htcondor
GH_PAGES = https://dodas-ts.github.io/helm-chart_htcondor
COMMIT_MSG = "v2.0.0-dodas-rc1"
CURRENT_BRANCH = "master"

.PHONY: help \
            helm-build

all: helm-build

helm-build:
	helm package ./ 
	helm repo index ./ --url ${GH_PAGES}
	mv ./index.yaml /tmp/
	mv ./${CHART_NAME}*.tgz /tmp/
	git checkout gh-pages
	cp /tmp/${CHART_NAME}*.tgz .
	cp /tmp/index.yaml .
	git add index.yaml *.tgz
	git commit -m ${COMMIT_MSG}
	git push origin gh-pages
	git checkout ${CURRENT_BRANCH}

help:
	@echo "Available commands:\n"
	@echo "- helm-build			: "
