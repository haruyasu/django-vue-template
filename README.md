# Django Vue.js Heroku Depkoy Template

![Vue Logo](/src/assets/logo-vue.png "Vue Logo")
![Django Logo](/src/assets/logo-django.png "Django Logo"　width=80%)
![Heroku Logo](/src/assets/logo-heroku.png "Heroku Logo")

## 説明

このテンプレートは、DjangoとVueを使用したアプリケーションの最小構成です。

このプロジェクトでは、バックグラウンドのDjangoとフロントエンドのVueが分かれています。

バックグラウンドのDjangoは、Web APIを管理し、Django REST Frameworkを使用します。  
createcreateproject


フロントエンドのVueは、npm、webpackを使用します。  
Vue CLI

### デモリンク

[Live Demo](https://django-vue-template-haru.herokuapp.com/)

### フレームワーク

* Django
* Django REST framework
* Django Whitenoise, CDN Ready
* Vue CLI 3
* Vue Router
* Vuex
* Gunicorn
* Configuration for Heroku Deployment

### 構成

| 場所             |  内容                                   |
|----------------------|--------------------------------------------|
| `/backend`           | Django Project & Backend Config            |
| `/backend/api`       | Django App (`/api`)                        |
| `/src`               | Vue App .                                  |
| `/src/main.js`       | JS Application Entry Point                 |
| `/public/index.html` | Html Application Entry Point (`/`)         |
| `/public/static`     | Static Assets                              |
| `/dist/`             | Bundled Assets Output (generated at `yarn build`) |

## Setup Template

```
$ git clone https://github.com/haruyasu/django-vue-template
$ cd django-vue-template
```

Setup  
```
$ pip3 install pipenv
$ npm install
$ pipenv install --dev && pipenv shell
$ python3 manage.py migrate
```

## Django

```
$ python3 manage.py runserver
```
URL  
[`localhost:8080`](http://localhost:8080/)

## Vue

```
$ npm run serve
```
URL  
[`localhost:8000`](http://localhost:8000/)

## ビルド
```
$ npm run build
$ python3 manage.py runserver
```

## デプロイ

* Set `ALLOWED_HOSTS` on [`backend.settings.prod`](/backend/settings/prod.py)

### Heroku Server

```
$ heroku apps:create django-vue-template-haru
$ heroku git:remote --app django-vue-template-haru
$ heroku buildpacks:add --index 1 heroku/nodejs
$ heroku buildpacks:add --index 2 heroku/python
$ heroku addons:create heroku-postgresql:hobby-dev
$ heroku config:set DJANGO_SETTINGS_MODULE=backend.settings.prod
$ heroku config:set DJANGO_SECRET_KEY='(your django SECRET_KEY value)'
$ git push heroku
```

Herokuのnodejsビルドパックは、package.jsonファイルからすべての依存関係のインストールを処理します。

そして、npm run buildでdistフォルダが作成されます。

Pythonビルドパックは、Procfileを検出し、すべてのPython依存関係をインストールします。

Procfileは、Djangoを実行してから、herokuが推奨するgunicornを使用してDjangoアプリを起動します。
