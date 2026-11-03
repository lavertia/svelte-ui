# @lavertia/svelte-ui

Production Svelte 5 renderer of Lavertia component protocol v1. This package owns the actual UI markup and interactivity; `lavertia/playground` is only a consumer.

Shared protocol utilities and validated theme tokens come from `@lavertia/ui`. PHP components, Eloquent scopes and authorization remain on the server in `lavertia/panels`.

## Development

```sh
npm install github:lavertia/svelte-ui#main
```

`src/page.svelte` imports the shared theme CSS, binds `themeStyle(lavertia.theme)` to its `lvt-root`, and delegates every component to this package's renderer.

Configure `lavertia.panels.admin.theme = \Lavertia\ThemeDefault\ClassicTheme::class` after installing `lavertia/theme-default`. This alpha package is not published to npm; pin dependencies by Git SHA for reproducibility.
