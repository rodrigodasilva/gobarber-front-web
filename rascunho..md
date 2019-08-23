## Utilizando root import

> yarn add customize-cra react-app-rewired -D

- Criamos um arquivo na raiz do projeto chamado 'config-overrides.js'

```js
const { addBabelPlugin, override } = require('customize-cra');

module.exports = override(
  addBabelPlugin([
    'babel-plugin-root-import',
    {
      rootPathSuffix: 'src',
    },
  ])
);
```

- Adicionamos o plugin ao babel

  > yarn add babel-plugin-root-import -D

- A partir dessas configurações, quando fomos importar um arquivo basta colocar um '~' na frente, que estaremos chamando a pasta 'src'

```js
import AuthLayout from '~/pages/_layouts/auth';
```

- Alteramos os 'scripts' em 'package.json'

```json
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
  },
```

- Configuramos o eslint para entender essa nova sintaxe

  > yarn add eslint-import-resolver-babel-plugin-root-import -D

  - Adicionamos ao arquivo '.eslintrc.js', logo abaixo das rules

  ```js
   settings: {
    'import/resolver': {
      'babel-plugin-root-import': {
        rootPathSuffix: 'src',
      },
    },
  },
  ```

- E configuramos, para que o vscode entenda o caminho, criando um arqui 'jsconfig.json' na raiz do projeto

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "~/*": ["*"]
    }
  }
}
```
