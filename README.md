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

[Sucrase](https://www.npmjs.com/package/sucrase): biblioteca alternativa ao Babel. Permite utilizarmos sintaxes mais modernas de JS que ainda não são suportadas pelo NodeJS.

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