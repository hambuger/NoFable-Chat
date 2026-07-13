# NoFable Chat

[中文](README.zh-CN.md) | English

NoFable Chat is a single-file, client-side multi-model aggregation chat page. It can call multiple OpenAI-compatible Chat Completions APIs in parallel, then ask an aggregator model to synthesize the final answer. It can also optionally use Firecrawl for web search.

## Features

- Parallel reference answers from multiple models
- Aggregated final answer
- Streaming output
- Toggleable intermediate reference layers
- `reasoning_content` display for reasoning models
- Optional Firecrawl web search tools
- Browser-local chat history
- Automatic Chinese / English UI switching

## Usage

Open `index.html` directly, or deploy it to GitHub Pages and visit the site homepage.

On first use, configure each model row in the left settings panel:

- `baseUrl`: an OpenAI-compatible Chat Completions endpoint, usually ending with `/chat/completions`
- `apiKey`: the API key for that provider
- `model`: model name
- `think`: enable reasoning output display for compatible models
- `search`: allow this model to call Firecrawl search tools
- `aggregator`: choose the model used to synthesize the final answer

Delete unused rows if you only want to use a subset of models. Every remaining row must be complete before sending.

## GitHub Pages Deployment

1. Commit `index.html`, `README.md`, and `README.zh-CN.md` to your GitHub repository.
2. Open repository `Settings` -> `Pages`.
3. Set `Build and deployment` to `Deploy from a branch`.
4. Choose the branch and root directory, for example `main` / `/ (root)`.
5. Save and wait for GitHub Pages to publish the site URL.

## Security Notes

There are no hardcoded real API keys in this repository. For convenience after page refreshes, the page saves user-entered model API keys and the Firecrawl key to the current browser's `localStorage`.

Because this is a purely client-side app, API keys are stored locally in the browser and sent directly from the browser to model providers. Any same-origin script, browser extension, compromised third-party dependency, XSS issue, or person with access to your browser data could read these keys. For shared or production deployments, use a backend proxy and do not place shared secrets in the frontend. To remove saved keys, clear them in the settings panel and trigger a save, or clear this site's browser data.

The page loads `marked` and `DOMPurify` from jsDelivr with pinned versions and SRI checks. For stricter supply-chain control, vendor these dependencies into the repository and reference local files.

## Limitations

- GitHub Pages can only host static files and cannot hide server-side secrets.
- Model providers must allow browser CORS requests, otherwise calls will fail.
- API keys and chat history are stored in the current browser's `localStorage` and are not synced.
- Web search requires your own Firecrawl API key.

## License

Add a license file before publishing if you plan to distribute this project.
