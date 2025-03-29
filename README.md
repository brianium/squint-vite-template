# squint-vite-template

An example and starting point for building [squint](https://github.com/squint-cljs/squint) apps using [tailwindcss](https://tailwindcss.com/) and [vite](https://vite.dev/).

## Requirements

- [babashka](https://babashka.org/) (development and building)
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

In addition to producing production css and js files, the build task will handle the particulars of converting vite's dev urls to their production equivalents. This is done by replacing vite manifeset entries (`isEntry == true`) `src` fields with their corresponding `file` fields.

See the `update-html` task in the `bb.edn` filefor more details

### Caveats

Going from squint to vite creates some issues with CSS imports locally. To get around this, the vite config for this repo uses an alias:

```js
{
    resolve: {
        alias: {
            '@': '/src'
        }
    }
}
```

Then you can import your css in your squint cljs files like this:

```clojure
(ns app.lib
  (:require ["@/app/lib.css"]))
```

`bb build` will ensure all css is copied for the production build. This is not an issue for css files contained in `node_modules`. i.e this will be fine as is:

```clojure
(ns editor
  (:require ["@yaireo/tagify$default" :as Tagify]
            ["@yaireo/tagify/dist/tagify.css"]))
```


## Deploying

The `dist` directory is the production build and can be deployed to your favorite static site host. The repo includes a github actions configuration that supports deploying to github pages.
