
# IMAGE_TAG := $(shell whoami | tr -d " ")-local
IMAGE_TAG = latest
NAMESPACE = temporal

NAME_REGULAR ?= benchtest-regular
NAME_SEPARATE_TQ ?= benchtest-separate-tq

REPLICAS_REGULAR ?= 10
REPLICAS_SEPARATE_TQ ?= 10


install-all: install-regular install-separate-tq
	kubectl get pods -n $(NAMESPACE) | grep $(NAME_REGULAR)
	kubectl get pods -n $(NAMESPACE) | grep $(NAME_SEPARATE_TQ)

uninstall-all: uninstall-regular uninstall-separate-tq
	kubectl get pods -n $(NAMESPACE) | grep $(NAME_REGULAR)
	kubectl get pods -n $(NAMESPACE) | grep $(NAME_SEPARATE_TQ)


install-regular:
	helm install $(NAME_REGULAR) . --set replicaCount=$(REPLICAS_REGULAR) --set image.tag=$(IMAGE_TAG) --set image.pullPolicy=Always --wait --timeout 60s --namespace $(NAMESPACE)

uninstall-regular:
	helm delete $(NAME_REGULAR) --namespace $(NAMESPACE) || true


install-separate-tq:
	helm install $(NAME_SEPARATE_TQ) . --set replicaCount=$(REPLICAS_SEPARATE_TQ) --set image.tag=$(IMAGE_TAG) --set image.pullPolicy=Always --wait --timeout 60s --namespace $(NAMESPACE)


uninstall-separate-tq:
	helm delete $(NAME_SEPARATE_TQ) --namespace $(NAMESPACE) || true

