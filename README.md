# Blog with user blocking (Django)

A small blogging platform built for the *Human-Computer Interaction* course at FINKI. Users write posts with attachments, comment, and can **block** other users, which hides their content in both directions.

## Features

- **Posts feed:** every post except those by users you've blocked
- **Profile page:** your details (profession, skills, interests) and your own posts
- **Write a post** with optional file attachments
- **Block list:** block users and see whom you've blocked
- **Admin panel** with per-object permissions:
  - you can only edit or delete your own profile, posts and comments
  - if an author blocked you, you can't see their posts, comments or files
  - the post author or the comment author can delete a comment
  - superusers can see and manage everything

## Data model

```
User (Django auth) ── BlogUser ──< Post ──< Comment
                          │            └──< File (attachment)
                          └── Block (blocker → blocked)
```

## Tech stack

Python, Django 4.2 (models, function-based views, ModelForms, admin customisation), SQLite, Bootstrap 5 templates.

## Running locally

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Log in at `/admin/` and create a **BlogUser** profile for your account. Then open:

| URL | Page |
|---|---|
| `/posts/` | Feed |
| `/profile/` | Your profile and posts |
| `/add/post/` | Write a post |
| `/blockedUsers/` | Block users / see blocked users |

Settings come from environment variables with safe local defaults: `DJANGO_SECRET_KEY`, `DJANGO_DEBUG` (`1`/`0`) and `DJANGO_ALLOWED_HOSTS`.
