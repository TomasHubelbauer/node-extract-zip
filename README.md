# Node Extract Single-File ZIP Archive

The following snippet of code implements a function which will take a `Buffer`
of a ZIP archive file contents and find a single deflated file inside, which it
will then inflate and return the result as another `Buffer`.

It works by first looking for the EOCD (end of central directory) entry, from it
identifying the corresponding CD (central directory) entry and from it the data
size and offset of the DEFLATE stream.
The stream is then fed into `zlib` Node built-in module's function `inflateRaw`.

The implementation can be found in [`index.js`](index.js) or referenced via ESM
HTTP imports if you use the experimental `--experimental-https-modules` CLI
flag.

```javascript
import extract from 'https://tomashubelbauer.github.io/node-extract-zip/index.js';

const buffer = await extract(await fs.promises.readFile('archive.zip'));
const text = buffer.toString();
const data = JSON.parse(buffer);
```

This repository has an associated GitHub Pages site.
This is so that `index.js` can be accessed with a correct MIME type to be usable
with ESM.
Direct GitHub web UI URL access or the raw UI URL access won't work.
