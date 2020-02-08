# Sequelize

https://sequelize.readthedocs.io/en/latest/

```bash
$ yarn add sequelize pg pg-hstore
$ yarn add sequelize-cli -D
```
## Setup
Create a `.sequelizerc` file:
```js
const { resolve } = require('path');

module.exports = {
  config: resolve(__dirname, 'src', 'config', 'database.js'),
  'models-path': resolve(__dirname, 'src', 'app', 'models'),
  'migrations-path': resolve(__dirname, 'src', 'database', 'migrations'),
  'seeders-path': resolve(__dirname, 'src', 'database', 'seeds'),
}
```

## Usage
```bash
$ yarn sequelize help
$ yarn sequelize migration:create --name=create-users-table # creates a migration file inside the 'migrations-path' folder defined inside .sequelizerc
$ yarn sequelize db:migrate
$ yarn sequelize db:migrate:undo # rollbacks the last migration
$ yarn sequelize db:migrate:undo:all  # rollback all migrations
```
