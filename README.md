# babel-plugin-transform-promise-to-any-promise

This plugin transforms `Promise` to [`any-promise`](https://www.npmjs.com/package/any-promise).

## Example
```javascript
export default function main() {
	const taskA = getResultAsync(1337);
	const taskB = new Promise((resolve, reject) =>
		nodeCallbackFunc(42, (err, res) => err ? reject(err) : resolve(res))
	);
	return Promise.all([taskA, taskB]).then(([resA, resB]) => resA + resB);
}
```
Gets converted to:
```javascript
import {all, default as Promise} from 'any-promise';

export default function main() {
	const taskA = getResultAsync(1337);
	const taskB = new Promise((resolve, reject) =>
		nodeCallbackFunc(42, (err, res) => err ? reject(err) : resolve(res))
	);
	return all([taskA, taskB]).then(([resA, resB]) => resA + resB);
}
```

## Usage

1. Install *any-promise*: `npm install --save any-promise`
2. Install the *promise-to-any-promise* plugin: `npm install --save-dev babel-plugin-transform-promise-to-any-promise`
3. Add *transform-promise-to-any-promise* to your *.babelrc* file:
```json
{
	"plugins": ["transform-promise-to-any-promise"]
}
```
If you'r using the *transform-runtime* plugin add *transform-promise-to-any-promise* before
*transform-runtime*:
```json
{
	"plugins": [
		"transform-promise-to-any-promise",
		"transform-runtime"
	]
}
```
