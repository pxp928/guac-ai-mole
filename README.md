# 🥑 Guac-AI-Mole

Guac-AI-Mole is a [large language model (LLM)](https://en.wikipedia.org/wiki/Large_language_model) powered tool to inspect and understand an organization's software supply chain. It uses LLM models, such as OpenAI GPT-4, and [GUAC](https://docs.guac.sh/) to query and analyze the secure supply chain artifacts, such as [Software Bill of Materials (SBOM)](https://www.cisa.gov/sbom), to make actionable decisions.

> 🧪 This is a hackathon project. Do not use in production.

## Demo

[Demo](https://guac-ai-mole.streamlit.app/) will provide samples questions and answers generated by Guac-AI-Mole!

> These answers are pre-generated and cached for faster response times and to avoid needing API access. You can try out your own questions and answers by [setting up the app locally](#development-setup).

## Development Setup

### Pre-requisites

- Install and run [GUAC](https://docs.guac.sh/setup/)
- Install [Steamlit](https://docs.streamlit.io/library/get-started/installation)
- [OpenAI](https://platform.openai.com/), [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service), or [LocalAI](https://localai.io/) API access (tested and recommended to use with `gpt-4-32k-0613` and later models)

### Generate SBOMs and populate the registry

- Download and copy [ORAS](https://oras.land/docs/installation) and [Syft](https://github.com/anchore/syft) to your `PATH`
- Login to your registry (make sure to have push access) and run `export REGISTRY=<registry name i.e., myregistry.io>` to set your registry
- Run `scripts/populate-registry.sh` to populate the registry with sample images and attached SBOMs as OCI referrers artifacts

### Run the app

- Install python dependencies with `pip install -r requirements.txt`
- Run `streamlit run app.py` to start the Streamlit app (add `--logger.level=debug` for debug logs)
- Navigate to app URL (default: http://localhost:8501)
- Set up Open AI API-compatible ([OpenAI](https://platform.openai.com/), [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service), [LocalAI](https://localai.io/)) API Key, endpoint and deployment name in the sidebar on the left
  - Alternatively, set `OPENAI_API_KEY`, `OPENAI_API_ENDPOINT` and `OPENAI_API_MODEL` environment variables
- Set up GUAC GraphQL endpoint in the sidebar on the left (default: http://localhost:8080/query). This URL must be accessible from the app.
  - Alternatively, set `GUAC_GRAPHQL_ENDPOINT` environment variable
