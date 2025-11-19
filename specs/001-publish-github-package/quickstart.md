# Quickstart: Using the `jira-mcp-server` from GitHub Package Registry

This guide explains how to use the `jira-mcp-server` package from the GitHub Package Registry.

## Prerequisites

-   Node.js >= 16.0.0
-   An `.npmrc` file in your project's root or home directory.

## 1. Configure `.npmrc`

To download packages from the GitHub Package Registry, you need to authenticate. Add the following line to your `.npmrc` file:

```
@orengrinker:registry=https://npm.pkg.github.com/
```

You also need to provide an access token with `read:packages` scope. You can do this by setting the `NODE_AUTH_TOKEN` environment variable.

## 2. Using with `npx`

You can run the server directly using `npx`:

```bash
JIRA_BASE_URL=https://your-company.atlassian.net \
JIRA_EMAIL=your-email@company.com \
JIRA_API_TOKEN=your-jira-api-token \
NODE_AUTH_TOKEN=your-github-token \
npx @orengrinker/jira-mcp-server
```

## 3. Using with `npm`

You can install the package in your project:

```bash
# Set the auth token as an environment variable
export NODE_AUTH_TOKEN=your-github-token

# Install the package
npm install @orengrinker/jira-mcp-server
```

Then, you can run it from your `node_modules`:

```bash
./node_modules/.bin/jira-mcp-server
```

