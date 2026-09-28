# Third-party files

These files are copied unchanged from their npm packages so the app works without a CDN.

| File                            | Package                                                                    | License                                               |
| ------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------- |
| `qpdf.js`, `qpdf.wasm`          | [`@neslinesli93/qpdf-wasm@0.3.0`](https://github.com/neslinesli93/qpdf-wasm) (qpdf 12.2.0 built for WebAssembly) | ISC (wrapper); qpdf itself is Apache-2.0, see `qpdf.LICENSE.txt` |
| `pdf-lib.min.js`                | [`@cantoo/pdf-lib@2.11.1`](https://github.com/cantoo-scribe/pdf-lib)       | MIT, see `pdf-lib.LICENSE.md`                         |

To update, run `npm pack <package>@<version>` and copy the files from its `dist/` folder.
