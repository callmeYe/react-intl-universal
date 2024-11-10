# react-intl-universal-extract
Extract [react-intl-universal](https://fe-tool.com/react-intl-universal)'s default messages in source code to locale files.

<img width="600" alt="image" src="https://img.alicdn.com/imgextra/i1/O1CN01WB2wMe1g5GiHzMAls_!!6000000004090-2-tps-2308-1090.png">

For example, suppose you have a file:
```jsx
  render() {
    const name = 'Tony';
    return (<>
      {intl.get('hello1').d('Hello World')}
      {intl.get('hello2', {name} ).d(`Hello ${name}`)}
    </>);
  }  
```

This tool will generate a json file which contains the extracted messages.

```json
{
  "hello1": "Hello World",
  "hello2": "Hello {name}",
}
```

Note that if the default message contains variables in ES6 template strings format (`Hello ${name}`), it will be transformed to ICU format (`Hello {name}`).

## Install
```sh
npm install --save-dev react-intl-universal-extract
```

## Usage

### CLI

In `package.json`, add a script:
```json
"scripts": {
  "intl:extract": "npx react-intl-universal-extract --cmd extract --source-path ./src --output-path ./src/locales/en_US.json --verbose",
}
```
Then run `npm run intl:extract`.

Parameters:
- `cmd`: only "extract" is supported currently.
- `source-path`: The source code directory path such as "./src"
- `output-path`: The extracted json file path such as "./src/locales/en_US.json"

### Programmable
```js
const intlTool = require('react-intl-universal-extract');
const result = intlTool.extract({
  sourcePath: './test-files',
});
console.log(result); 
/** result:
[{
  key: 'hello2',
  path: 'test-files/App.js',
  originalDefaultMessage: 'Hello ${name}',
  transformedDefaultMessage: 'Hello {name}'
}]
*/
```

## License
This software is free to use under the BSD license.

## Contributing
See "develop.md"
