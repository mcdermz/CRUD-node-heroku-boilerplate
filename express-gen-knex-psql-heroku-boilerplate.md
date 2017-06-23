*** from project root directory ****

# express and knex

`$ express --hbs --git`

`$ npm install`
  * installs boilerplate dependencies

`$ npm install --save pg knex method-override`

`$ npm install --save-dev nodemon `
  * adds nodemon start script in package.json

`$ git init`

`$ touch knexfile.js `
  * setup knexfile.js config
  ```
  const path = require('path');

  module.exports = {
    development: {
      client: 'pg',
      connection: 'postgres://localhost/cookies_crud',
      migrations: {
        directory: path.join(__dirname, 'db', 'migrations')
      },
      seeds: {
        directory: path.join(__dirname, 'db', 'seeds')
      }
    },
    production: {
      client: 'pg',
      connection: process.env.DATABASE_URL,
      migrations: {
        directory: path.join(__dirname, 'db', 'migrations')
      },
      seeds: {
        directory: path.join(__dirname, 'db', 'seeds')
      }
    }
  };
  ```
`$ mkdir db`

`$ touch db/knex.js`
  * add knex start script in package.json
  * setup knex.js config

  ```
  const env = process.env.NODE_ENV || 'development';
  const config = require('../knexfile.js')[env];
  const knex = require('knex')(config);

  module.exports = knex;
  ```

`$ createdb [database name]`

`$ psql [database name]`
  * in new shell tab to confirm database creation


# knex migrations

`$ npm run knex migrate:make [table name]`
  * edit migration file to create table

`$ npm run knex migrate:latest`
  * creates the table in the database

`$ npm run knex seed:make 1_[table name]`
  * edit the seed file to insert data, make sure to delete the data before inserting data

`$ npm run knex seed:run`
  * seeds the table with your data


# setting routes

* set route with a method and attach a named function

* code function to return a simple message
  - test

* build html template to render and have function render that template
  - test

* hard-code variables in function to pass through to template
  - test

* refactor function to include logic and dynamic variables
  - test


# HEROKU deployment

* Add a production key to `knexfile.js`
  - set connection: `process.env.DATABASE_URL`
  - everything else should be the same as development

* Set a ternary in `db/knex.js`
  - `const env = process.env.NODE_ENV || 'development';`

`$ heroku create [app name]`
  * To rename: `$ heroku apps:rename [new name] `

`$ git commit -m 'prep for deployment'`

`$ git push heroku master`

`$ heroku open` *opens your heroku-deployed app*

`$ heroku logs` *for finding errors*

`$ heroku config`
  * use `heroku config:set VAR_NAME=value` to add environment variables to deployed site

`$ heroku addons:create heroku-postgresql`
  * creates a postgres server on heroku

`$ heroku run bash`
  * opens up a console on heroku server for your app  
  * run migrations and seed your db as you would locally
