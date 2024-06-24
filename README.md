# django-tutorial

- [Django ドキュメント](https://docs.djangoproject.com/ja/5.0/contents/) のチュートリアルログ

### Writing your first Django app, part 1

```sh
python manage.py runserver
```

_http://127.0.0.1:8000/polls/_

### Writing your first Django app, part 2

```sh
python manage.py migrate
  # Operations to perform:
  #   Apply all migrations: admin, auth, contenttypes, sessions
  # Running migrations:
  #   Applying contenttypes.0001_initial... OK
  #   Applying auth.0001_initial... OK
  #   Applying admin.0001_initial... OK
  #   Applying admin.0002_logentry_remove_auto_add... OK
  #   Applying admin.0003_logentry_add_action_flag_choices... OK
  #   Applying contenttypes.0002_remove_content_type_name... OK
  #   Applying auth.0002_alter_permission_name_max_length... OK
  #   Applying auth.0003_alter_user_email_max_length... OK
  #   Applying auth.0004_alter_user_username_opts... OK
  #   Applying auth.0005_alter_user_last_login_null... OK
  #   Applying auth.0006_require_contenttypes_0002... OK
  #   Applying auth.0007_alter_validators_add_error_messages... OK
  #   Applying auth.0008_alter_user_username_max_length... OK
  #   Applying auth.0009_alter_user_last_name_max_length... OK
  #   Applying auth.0010_alter_group_name_max_length... OK
  #   Applying auth.0011_update_proxy_permissions... OK
  #   Applying auth.0012_alter_user_first_name_max_length... OK
  #   Applying sessions.0001_initial... OK
```

マイグレーションファイルの作成

```sh
python manage.py makemigrations polls
  # Migrations for 'polls':
  #   polls/migrations/0001_initial.py
  #     - Create model Question
  #     - Create model Choice
```

マイグレーション SQL の確認

```sh
python manage.py sqlmigrate polls 0001
  # --
  # -- Create model Question
  # --
  # CREATE TABLE `polls_question` (`id` bigint AUTO_INCREMENT NOT NULL PRIMARY KEY, `question_text` varchar(200) NOT NULL, `pub_date` datetime(6) NOT NULL);
  # --
  # -- Create model Choice
  # --
  # CREATE TABLE `polls_choice` (`id` bigint AUTO_INCREMENT NOT NULL PRIMARY KEY, `choice_text` varchar(200) NOT NULL, `votes` integer NOT NULL, `question_id` bigint NOT NULL);
  # ALTER TABLE `polls_choice` ADD CONSTRAINT `polls_choice_question_id_c5b4b260_fk_polls_question_id` FOREIGN KEY (`question_id`) REFERENCES `polls_question` (`id`);
```

プロジェクトに問題がないかを確認

```sh
python manage.py check
  # System check identified no issues (0 silenced).
```

マイグレートを実行

```sh
python manage.py migrate
  # Operations to perform:
  #   Apply all migrations: admin, auth, contenttypes, polls, sessions
  # Running migrations:
  #   Applying polls.0001_initial... OK
```

インタラクティブ起動

```sh
python manage.py shell
```

管理ユーザー作成

```sh
python manage.py createsuperuser
  # Username (leave blank to use 'vscode'):
  # Email address:
  # Password:
  # Password (again):
  # Superuser created successfully.
```

_http://127.0.0.1:8000/admin/_

### Writing your first Django app, part 5

テスト実行

```sh
python manage.py test polls
```

カバレッジ取得

```sh
coverage run --source='.' manage.py test polls

# Report
coverage report
  # Name                               Stmts   Miss  Cover
  # ------------------------------------------------------
  # manage.py                             11      2    82%
  # mysite/__init__.py                     0      0   100%
  # mysite/asgi.py                         4      4     0%
  # mysite/settings.py                    18      0   100%
  # mysite/urls.py                         3      0   100%
  # mysite/wsgi.py                         4      4     0%
  # polls/__init__.py                      0      0   100%
  # polls/admin.py                         3      0   100%
  # polls/apps.py                          4      0   100%
  # polls/migrations/0001_initial.py       6      0   100%
  # polls/migrations/__init__.py           0      0   100%
  # polls/models.py                       17      2    88%
  # polls/tests.py                        57      0   100%
  # polls/urls.py                          4      0   100%
  # polls/views.py                        29      8    72%
  # ------------------------------------------------------
  # TOTAL                                160     20    88%

# HTML report
coverage html
  # Wrote HTML report to htmlcov/index.html
```

### Writing your first Django app, part 8

**django-debug-toolbar**

_settings.py_

```python
INSTALLED_APPS = [
    ...
    'debug_toolbar',
]

MIDDLEWARE = [
    ...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]

INTERNAL_IPS = [
    '127.0.0.1',
]
```

_urls.py_

```python
from django.urls import path, include

urlpatterns = [
    ...
    path('__debug__/', include('debug_toolbar.urls')),
]
```
