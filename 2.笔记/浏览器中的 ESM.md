## 浏览器中的 ESM
1. Native Import: Import from URL
	通过 `script[type=module]`，可直接在浏览器中使用原生 `ESM`,只能进行url的引入
2. ImportMap
	通过`script[type=importmap]`，并在其中引入，即可使用esm
```
{
	"imports": {
	  "lodash": "https://cdn.skypack.dev/lodash",
	  "lodash/": "https://cdn.skypack.dev/lodash/"
	}
}
```
3. Import Assertion
	通过`script[type=module]`，可以引入 JSON/CSS
```
import data from "./data.json" assert { type: "json" };
```
	   