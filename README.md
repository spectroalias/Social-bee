# Social Bee

Social Bee is a Twitter-style microblogging app. Users can register, log in, post short text/image updates, like posts, and repost ("share") content from others. The project is split into a Django REST API backend and a React single-page frontend.

## Features

- **Auth** — Email/password registration and login with JWT access & refresh tokens (`djangorestframework-simplejwt`).
- **Posts** — Create short text posts (up to 100 characters) with an optional image.
- **Feed** — View the global feed or filter posts by a specific user's username.
- **Likes** — Like / unlike any post.
- **Reposts** — Share another user's post to your own feed.
- **Delete** — Remove your own posts.

## Tech Stack

**Backend**
- Python / Django 3.2 + Django REST Framework
- `djangorestframework-simplejwt` for JWT authentication
- SQLite (default, via `db.sqlite3`)
- `django-cors-headers` for CORS
- Swagger API docs via `django-rest-swagger`

**Frontend**
- React 17 (Create React App)
- `react-router-dom` for routing
- `axios` for API calls

## Project Structure

```
Social-bee/
├── requirements.txt          # Python dependencies
└── social/
    ├── manage.py
    ├── social/                # Django project settings & root URLs
    ├── user/                  # User model, auth (login/register/logout) API
    ├── post/                  # Post model, feed, like/share API
    └── social-web/            # React frontend (Create React App)
```

## Getting Started

### Backend (Django API)

Requires Python 3.8+.

```bash
# from the repository root
pip install -r requirements.txt

cd social
python manage.py migrate
python manage.py runserver
```

The API will be available at `http://127.0.0.1:8000/`.

### Frontend (React)

Requires Node.js and npm.

```bash
cd social/social-web
npm install
npm start
```

The app will be available at `http://localhost:3000/` and will talk to the Django API.

## API Overview

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/user/register/` | Register a new user |
| POST | `/api/user/login/` | Log in, returns JWT access/refresh tokens |
| POST | `/api/user/logout/` | Blacklist a refresh token |
| POST | `/api/token/` | Obtain JWT token pair |
| POST | `/api/token/refresh/` | Refresh an access token |
| GET | `/api/feeds/` | List all posts |
| GET | `/api/feeds/<username>/` | List posts by a specific user |
| POST | `/api/post-create/` | Create a new post (auth required) |
| GET | `/api/post-detail/<post_id>/` | Get details of a single post |
| POST/DELETE | `/api/post-delete/<post_id>/` | Delete a post you own (auth required) |
| POST | `/api/post-action/` | Like/unlike or share a post (auth required) |
| GET | `/api/docs/` | Swagger API documentation |

## License

No license has been specified for this project yet.
