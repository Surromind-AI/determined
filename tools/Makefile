.PHONY: clean
clean:
	rm -rf build/

.PHONY: start-db
start-db: stop-db
	docker-compose up -d

.PHONY: stop-db
stop-db:
	docker-compose down

.PHONY: psql
psql:
	docker exec -it \
		tools_determined-db_1 \
		psql determined -U postgres

.PHONY: prep-root
prep-root:
	@rm -rf build
	@mkdir -p build/webui/docs
	@mkdir -p build/webui/elm
	@mkdir -p build/webui/react
	@mkdir -p build/wheels/
	@ln -s $(abspath ../master/static) build/
	@ln -s $(abspath ../proto/build/swagger) build/swagger
	@ln -s $(abspath ../docs/site/html/*) build/webui/docs
	@ln -s $(abspath ../webui/react/build/*) build/webui/react
	@ln -s $(abspath ../webui/elm/public) build/webui/elm
	@ln -s $(abspath ../common/dist/*.whl) build/wheels/
	@ln -s $(abspath ../cli/dist/*.whl) build/wheels/
	@ln -s $(abspath ../harness/dist/*.whl) build/wheels/

.PHONY: run
run: prep-root
	@python3 run-server.py
