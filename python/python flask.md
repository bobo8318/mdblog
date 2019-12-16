### 1.install & require

> conda install flask
>
> conda install -r requires.txt



>  requires.txt contents:
>
>  alembic
>
>  amqp
>
>  billiard
>
>  celery
>
>  certifi
>
>  chardet
>
>  Flask
>
>  Flask-Migrate
>
>  Flask-Script # 插入脚本
>
>  Flask-Session
>
>  Flask-SQLAlchemy # 操作数据库
>
>  Flask-WTF #表单
>
>  Flask-markdown
>
>  Jinja2
>
>  kombu
>
>  Mako
>
>  virtualenv #版本控制



* 2.create project

  * 目录结构

    > ./
    >
    > ----readme.md
    >
    > ----app/
    >
    > ----|----  __ init __.py
    >
    > ----|----models.py
    >
    > ----|----static/
    >
    > ----|----templates/
    >
    > ----|----views.py
    >
    > ----config.py
    >
    > ----manage.py
    >
    > requirements.txt

  * app/__ init __.py

    > from flask import Flask
    >
    > app = Flask(__ name __)
    >
    > app.config.from_object("config")
    >
    > from app import  views, models

  * app/views.py 主逻辑

    > from app import app
    >
    > from flask import render_template
    >
    > @app.route('/')
    >
    > def index():
    >
    > ​	#return "hello world"
    >
    > ​	return render_template('index.html')

  * manage.py

    > from flask.ext.script import Manager, Server
    >
    > from app import app
    >
    > manager = Manager(app)
    >
    > manager.add_command("runserver", Server(host="127.0.0.1", port=5000, use_debugger=True))
    >
    > if  __ name __ == '__ main __':
    >
    > ​	manager.run()

* run app

  > python manage.py flask