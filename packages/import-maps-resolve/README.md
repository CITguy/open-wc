# Resolve import-maps

[//]: # (AUTO INSERT HEADER PREPUBLISH)

This will allow you to parse and resolve urls by a given [import-map](https://github.com/WICG/import-maps).

## Usage

```bash
yarn add @import-maps/resolve
```

You may then override a resolve method in your build process.

```js
import { parseFromString, resolve } from '@import-maps/resolve';

// you probably want to cache the map processing and not redo it for every resolve
// a simple example
const mapCache = null;

function myResolve(specifier) {
  const currentDir = process.cwd();
  if (!mapCache) {
    const mapString = fs.readFileSync(path.join(currentDir, 'import-map.json'), 'utf-8');
    mapCache = parseFromString(mapString, currentDir);
  }

  return specifier => resolve(specifier, mapCache, path.join(`${currentDir}::`, 'index.html');
}
```

### Additional info

The 3rd parameter of `resolve` is the "baseUrl/basePath" and it's format is `/path/to/root::/subdir/foo`.
You can compare it with an url `http://example.com/subdir/foo`.
- Everything before the `::` is sort of the `domain` e.g. `http://example.com/`
- Everything after is the path/directory to your appliaction

Such a path is needed as import maps support relative pathes as values.

## Acknowledgments
This implementation is heavily based on the [import-maps reference implementation](https://github.com/WICG/import-maps/tree/master/reference-implementation).
Thanks to @domenic and @guybedford for sharing that prototype.

Some adjustments have been made
- Allow to process/resolve node pathes besides urls
- Use mocha/chai for testing (already available in our setup)

<script>
  export default {
    mounted() {
      const editLink = document.querySelector('.edit-link a');
      if (editLink) {
        const url = editLink.href;
        editLink.href = url.substr(0, url.indexOf('/master/')) + '/master/packages/import-maps-process/README.md';
      }
    }
  }
</script>
