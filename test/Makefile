KUBE_CLUSTER_NAME=wallarm-sidecar-chart
KUBE_CONTEXT=kind-$(KUBE_CLUSTER_NAME)

all: lint create_cluster install_chart run_test

install: install_dependency

clean: delete_cluster

lint:
	@helm lint ../. --debug

create_cluster:
	@DOCKER_BUILDKIT=1 kind create cluster --name $(KUBE_CLUSTER_NAME) --config kind/kind.yaml -v 1

install_chart:
	@helm install wallarm-sidecar ../. -f ../test-values.yaml --kube-context $(KUBE_CONTEXT) --namespace wallarm-sidecar --create-namespace --debug

run_test:
	@pytest --kube_context $(KUBE_CONTEXT)

upgrade_chart:
	@helm upgrade wallarm-sidecar ../. -f ../test-values.yaml --kube-context $(KUBE_CONTEXT) --namespace wallarm-sidecar --debug

delete_cluster:
	@kind delete cluster --name $(KUBE_CLUSTER_NAME)

install_dependency:
	@python3 -m pip install -r requirements.txt
	#@brew install kind

.PHONY: create_cluster install_chart run_test upgrade_chart delete_cluster lint