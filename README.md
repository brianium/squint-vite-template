# squint-vite-template

An example and starting point for building [squint](https://github.com/squint-cljs/squint) apps using [tailwindcss](https://tailwindcss.com/) and [vite](https://vite.dev/).

## Requirements

- [babashka](https://github.com/babashka/babashka) (development and building)
- [node + npm](https://nodejs.org/en/download/) (dependency management)

## Development

Run the `bb dev` task. Vite will provide the dev server. By default you just need to hit http://localhost:5173 to see the app.

```bash
$ bb dev
```

## Building

Run the `bb build` task. The default behavior of this repo is to build to a `dist` directory in the project root.

```bash
$ bb build
```

In addition to producing production css and js files, the build task will handle the particulars of converting vite's dev urls to their production equivalents. `app.js` and `app.css` are the assumed asset names.

See the `update-html` task in the `bb.edn` filefor more details

## Deploying

The `dist` directory is the production build and can be deployed to your favorite static site host. The repo includes a github actions configuration that supports deploying to github pages.
