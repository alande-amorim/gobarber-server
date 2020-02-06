- [Aula 1 - configurando estrutura](#aula-01---configurando-estrutura)
- [Aula 2 - Nodemon & Sucrase](#aula-02---nodemon-&-sucrase)
- Aula 3 - Conceitos do Docker
- Aula 4 - Configurando Docker
- [Aula 6 - Padronização de Código](#aula-06---eslint,-prettier-&-editorconfig)
- [Aula 7 - Configurando Sequelize](#aula-07---configurando-sequelize)

## Aula 01 - configurando estrutura

```bash
$ yarn add express
$ mkdir ./src
$ touch ./src/app.js
$ touch ./src/server.js
$ touch ./src/routes.js
```
### ```./src/app.js```:
Arquivo de configuração da aplicação

### ```./src/server.js```:
Inicializa o servidor

### ```./src/routes.js```:
Define as rotas da aplicação

## Executando a aplicação:
```bash
$ node ./src/server.js
```

## Aula 02 - Nodemon & Sucrase

Configurando Sucrase e Nodemon.

```bash
$ yarn add sucrase nodemon -D
```

- [Sucrase](https://www.npmjs.com/package/sucrase): biblioteca alternativa ao Babel. Permite utilizarmos sintaxes mais modernas de JS que ainda não são suportadas pelo NodeJS.

### Executando a aplicação:
```bash
$ yarn sucrase-node ./src/server.js
```

## Configurando Sucrase junto com o Nodemon

Crie ```./nodemon.json```:
```json
{
    "execMap" : {
        "js": "node -r sucrase/register"
    }
}
```
Esse arquivo registra junto ao Nodemon que o node deverá ser executado junto com o ```sucrase/register``` para arquivos JS.

Agora podemos inicializar a aplicação executando:

```bash
$ yarn nodemon src/server.js
```
## Depurando junto com o Sucrase e Nodemon

Criar arquivo de configuração de debug do Vscode (```./vscode/launch.json```):
```json
{
    "configurations": [
        {
            //...
            "request": "attach",
            "protocol": "inspector",
            "restart": true
            //...
        }
    ]
}
```

Para depurar a aplicação utilizando o Sucrase e Nodemon:
```bash
$ yarn nodemon --inspect src/server.js
```

Podemos criar scripts auxiliares agora dentro do ```./package.json```:
```json
    // ...
    "scripts": {
        "dev": "nodemon src/server.js",
        "dev:debug": "nodemon --inspect src/server.js",
    }
    // ...
```

## Aula 06 - ESLint, Prettier & EditorConfig

### 1. ESLint
- passo 1 - instalando o ESLint no projeto:

```bash
$ yarn add eslint -D
$ yarn eslint --init

  ? How would you like to use ESLint?
    To check syntax only
    To check syntax and find problems
  ❯ To check syntax, find problems, and enforce code style

  ? What type of modules does your project use? (Use arrow keys)
  ❯ JavaScript modules (import/export)
    CommonJS (require/exports)
    None of these

  ? Which framework does your project use?
    React
    Vue.js
  ❯ None of these

  ? Does your project use TypeScript? (y/N) N

  ? Where does your code run?
   ◯ Browser
  ❯◉ Node

  ? How would you like to define a style for your project? (Use arrow keys)
  ❯ Use a popular style guide
    Answer questions about your style
    Inspect your JavaScript file(s)

  ? Which style guide do you want to follow? (Use arrow keys)
  ❯ Airbnb: https://github.com/airbnb/javascript
    Standard: https://github.com/standard/standard
    Google: https://github.com/google/eslint-config-google

  ? What format do you want your config file to be in? (Use arrow keys)
  ❯ JavaScript
    YAML
    JSON

  ? Would you like to install them now with npm? (Y/n) Y

$ yarn
```

Ao final, vai ser criado um arquivo ```./.eslintrc.js```

- passo 2 - instalar plugin [ESLint no Vscode](https://github.com/Microsoft/vscode-eslint.git)

- passo 3 - configurar autofix do ESLint no Vscode:

Adicione essas linhas ao ```settings.json``` do vscode
```json
{
    // ...
    "[javascript]": {
        "editor.codeActionsOnSave": {
            "source.fixAll.eslint": true,
        }
    },
    "[javascriptreact]": {
        "editor.codeActionsOnSave": {
            "source.fixAll.eslint": true,
        }
    }
    // ...
}
```
Após essas configurações, ao salvarmos algum arquivo .js, problemas acusados pelo ESLint serão automaticamente corrigidos.

- passo 4 - customizações do ```./.eslintrc.js```:

```js
    // ...
    rules: {
        "class-methods-use-this": "off",
        "no-param-reassign": "off",
        "camel-case": "off",
        "no-unused-vars": ["error", {"argsIgnorePattern": "next"}],
    },
    // ...
```

Podemos executar o lint em todos arquivos de uma pasta específica pelo CLI:
```bash
$ yarn eslint --fix src --ext .js
```

### 2. Prettier

#### Instalação:
```bash
$ yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

#### Configuração:
```.eslintrc.js```:
```js
 //...
 extends: ['airbnb-base', 'prettier'],
 plugins: ['prettier'],
 //...
 rules: {
     "prettier/prettier": "error",
    // ...
 }
 //...
```

Para evitar que as regras no Prettier deem conflito com as do ESLint, podemos reescrever as regras do Prettier no arquivo ```.prettierrc```:
```json
{
    "singleQuote": true,
    "trailingComma: "es5"
}
```
### 3. Editorconfig

- Passo 1 - instalar plugin Editorconfig no Vscode
- Passo 2 - criar ```./.editorconfig```:
```
root true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

## Aula 07 - Configurando Sequelize

Estrutura final de pastas:
```
gobarber-server/
├── src
│   ├── app
│   │   ├── controllers
│   │   └── models
│   ├── config
│   │   └── database.js
│   ├── database
│   │   └── migrations
│   ├── app.js
│   ├── routes.js
│   └── server.js
├── .vscode
│   └── launch.json
├── .editorconfig
├── .eslintrc.js
├── .gitignore
├── nodemon.json
├── package.json
├── package-lock.json
├── .prettierrc
├── README.md
├── .sequelizerc
```
Instalação

```bash
$ mkdir src/config
$ touch src/config/database.js
$ mkdir src/database
$ mkdir src/database/migrations
$ mkdir src/database/seeds
$ mkdir src/app
$ mkdir src/app/controllers
$ mkdir src/app/models

$ yarn add sequelize pg pg-hstore
$ yarn add sequelize-cli -D
```

Crie o arquivo de configuração ```./.sequelizerc```:
```js
const { resolve } = require('path');

module.exports = {
  config: resolve(__dirname, 'src', 'config', 'database.js'),
  'models-path': resolve(__dirname, 'src', 'app', 'models'),
  'migrations-path': resolve(__dirname, 'src', 'database', 'migrations'),
  'seeders-path': resolve(__dirname, 'src', 'database', 'seeds'),
}
```

```./src/config/database.js```:
```js
module.exports = {
  dialect: 'postgres',
  host: 'localhost',
  port: 5433,
  username: 'postgres',
  password: 'docker',
  database: 'gobarber',
  define: {
    timestamps: true,
    underscored: true,
    underscoredAll: true,
  },
};
```
