# Continuous Integration and Deployment

## Heroku

- [Install CLI tool](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

### Setup for NodeJS

#### Init a NodeJS project

```
npm init -y
```

#### Init a Github repository

```
git init
```

#### Init a Github repository

```
git init
```

#### Init an Heroku project

```
heroku login
heroku create
```

#### Specify the Node engine version

Get the current system version `node --version`

In `package.json`:

```json
"engines": {
  "node": "9.2.0"
}
```

#### Specify start script

In `package.json`:

```json
"main": "server.js",
"scripts": {
  "start": "node server.js"
}
```

#### Use a dynamic port for the server


```js
app.listen(process.env.PORT || 8000);
```

#### Commit and deploy

```
git add .
git commit -m "initial commit"
git push heroku master
```

## CircleCI

### Setup Github

Create a new repository in Github.

```
git remote add origin https://github.com/user/repo.git
git push -u origin master
```

### Setup CircleCI

```
mkdir .circleci
touch .circle/config.yml
```

Configure `config.yml` according to [docs](https://circleci.com/docs/2.0/).

### Setup Heroku on CircleCI

See [documentation](https://circleci.com/docs/2.0/deployment-integrations/#heroku)

- Add your [Heroku API key](https://dashboard.heroku.com/account) into CircleCI as `HEROKU_API_KEY` env variable.
- Add your Heroku App name (e.g. foo-bar-123) as `HEROKU_APP_NAME`
- Add deployment settings to `config.yml`

```yml
jobs:
  deploy:
    docker:
      - image: circleci/node:9.2.0
    steps:
      - checkout
      - run:
          name: Deploy Master to Heroku
          command: |
            git push https://heroku:$HEROKU_API_KEY@git.heroku.com/$HEROKU_APP_NAME.git master
```

### Setup a CircleCI Workflow

Read the [docs](https://circleci.com/docs/2.0/workflows/).

Example:

```yml
workflows:
  version: 2
  build_and_test:
    jobs:
      - build
      - deploy:
          requires:
            - build
jobs:
  ...
```

### Sample `config.yml`

```yml
version: 2
workflows:
  version: 2
  build_and_test:
    jobs:
      - build
      - deploy:
          requires:
            - build
jobs:
  deploy:
    docker:
      - image: circleci/node:9.2.0
    steps:
      - checkout
      - run:
          name: Deploy Master to Heroku
          command: |
            git push https://heroku:$HEROKU_API_KEY@git.heroku.com/$HEROKU_APP_NAME.git master
  build:
    working_directory: ~/repo
    docker:
      - image: circleci/node:9.2.0
      # - image: circleci/mongo:3.4.4
    steps:
      - checkout
      - restore_cache:
          key: deps-cache-{{ checksum "package.json" }}
      - run:
          name: 'install deps'
          command: 'npm install'
      - save_cache:
          key: deps-cache-{{ checksum "package.json" }}
          paths:
            - node_modules
      - run:
          name: 'test'
          command: 'npm test'
```