.PHONY: test install example

test:
	LANGWATCH_API_KEY="testkey" PYTHONPATH=$$PYTHONPATH:. uv run pytest -s -vv -m "not integration" $(filter-out $@,$(MAKECMDGOALS))

test-examples:
	uv pip install crewai==0.60.0 openinference-instrumentation-crewai duckduckgo_search; \
	uv run pytest tests/test_examples.py -p no:warnings -s $(filter-out $@,$(MAKECMDGOALS))

install:
	@if ! command -v uv &> /dev/null; then \
		curl -LsSf https://astral.sh/uv/install.sh | sh; \
	fi
	uv sync --all-extras

example:
	@args="$(filter-out $@,$(MAKECMDGOALS))"; \
	if [[ $$args =~ "fastapi" ]]; then \
		uv run python $$args; \
	elif [[ $$args =~ "streamlit" ]]; then \
		uv run streamlit run $$args; \
	else \
		uv run chainlit run -w --port 9000 $$args; \
	fi

batch-evaluation-example:
	uv run python $(filter-out $@,$(MAKECMDGOALS))

%:
	@: