#!make

include .env

DOCKER_DIR = $(shell pwd)

network:
	${DOCKER_DIR}/network.sh

up-traefik:
	docker-compose --project-name my-traefik --file ${DOCKER_DIR}/docker-compose.traefik.yml up -d --build

stop-traefik:
	docker-compose --project-name my-traefik --file ${DOCKER_DIR}/docker-compose.traefik.yml stop

stop-traefik:
	docker-compose --project-name my-traefik --file ${DOCKER_DIR}/docker-compose.traefik.yml down

up-%: up-traefik
	@bash -c ' \
		set -o allexport; \
		source .${$(*)}.env; \
		set +o allexport; \
		docker-compose --project-name ${$(*)} --file ${DOCKER_DIR}/docker-compose.$${PROJECT_DRUPAL}.yml up -d --build; \
	'

stop-%: stop-traefik
	@bash -c ' \
		set -o allexport; \
		source .${$(*)}.env; \
		set +o allexport; \
		docker-compose --project-name ${$(*)} --file docker-compose.$${PROJECT_DRUPAL}.yml stop; \
         '

down-%: down-traefik
	@bash -c ' \
		set -o allexport; \
		source .${$(*)}.env; \
		set +o allexport; \
		docker-compose --project-name ${$(*)} --file docker-compose.$${PROJECT_DRUPAL}.yml down; \
         '
