# Twitter Clone

A full-stack Twitter/X-style social media application built with the MERN stack.

## Overview

This app lets users sign up, share posts, and interact with a feed, much like Twitter/X.

Features:

- 🔐 **Authentication** — sign up, log in, and log out with JWTs stored in secure, `httpOnly` cookies; passwords hashed with bcrypt
- ✍️ **Posts** — create posts with text and/or an image
- ❤️ **Likes** — like and unlike posts
- 💬 **Comments** — comment on posts
- 🗑️ **Delete** — delete your own posts
- 👥 **Follows** — follow and unfollow other users
- 🧑‍🤝‍🧑 **Suggested users** — discover people to follow
- 📰 **Feeds** — view all posts or a following-only feed
- 📝 **Profiles** — edit your profile info, bio, and link
- 🖼️ **Images** — upload profile and cover images (stored on Cloudinary)
- 🔔 **Notifications** — receive notifications for new follows and likes
- ⚡ **React Query** — client-side data fetching and caching

## Tech stack

- **Frontend:** React (Vite), React Router, TanStack React Query, Tailwind CSS, daisyUI, react-hot-toast, react-icons
- **Backend:** Node.js, Express
- **Database:** MongoDB with Mongoose
- **Auth:** JSON Web Tokens (JWT) via `httpOnly` cookies, bcrypt for password hashing
- **Media:** Cloudinary for image uploads

## Getting started

### Prerequisites

- Node.js (v18+ recommended)
- A MongoDB database (e.g. MongoDB Atlas)
- A Cloudinary account (for image uploads)

### 1. Clone and install

```shell
git clone https://github.com/komalboyo/twitter-clone.git
cd twitter-clone

# install backend (root) dependencies
npm install

# install frontend dependencies
npm install --prefix frontend
```

### 2. Configure environment variables

Create a `.env` file in the project root. See `.env-sample` for the full list. The required variable **names** are:

```shell
MONGO_URI=
PORT=
JWT_SECRET=
NODE_ENV=
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
```

> Never commit your `.env` file or any real secret values. The `.env` file is already listed in `.gitignore`.

### 3. Run in development

The backend serves the API on `PORT` (default `5000`); the Vite dev server runs on port `3000` and proxies `/api` requests to the backend.

```shell
# terminal 1 — backend (with auto-reload)
npm run dev

# terminal 2 — frontend dev server
npm run dev --prefix frontend
```

Then open http://localhost:3000.

### 4. Build and run in production

In production, Express serves the built frontend from `frontend/dist`.

```shell
# build the frontend (also installs deps)
npm run build

# start the server
npm start
```

## Project structure

```
twitter-clone/
├── backend/
│   ├── controllers/      # auth, post, user, notification request handlers
│   ├── db/               # connectMongoDB.js — Mongoose connection
│   ├── lib/utils/        # generateToken.js — JWT cookie helper
│   ├── middleware/       # protectRoute.js — JWT auth guard
│   ├── models/           # User, Post, Notification Mongoose schemas
│   ├── routes/           # /api/auth, /api/users, /api/posts, /api/notifications
│   └── server.js         # Express app entry point
├── frontend/
│   ├── src/
│   │   ├── components/    # common, skeletons, svgs
│   │   ├── hooks/         # useFollow, useUpdateUserProfile
│   │   ├── pages/         # auth, home, profile, notification
│   │   └── utils/         # date + dummy data helpers
│   ├── public/
│   └── vite.config.js     # dev server + /api proxy config
├── .env-sample            # template of required env var names
├── package.json           # backend deps + dev/build/start scripts
└── README.md
```

### API routes

| Resource       | Base path             | Examples                                                       |
| -------------- | --------------------- | -------------------------------------------------------------- |
| Auth           | `/api/auth`           | `POST /signup`, `POST /login`, `POST /logout`, `GET /me`       |
| Users          | `/api/users`          | `GET /profile/:username`, `GET /suggested`, `POST /follow/:id`, `POST /update` |
| Posts          | `/api/posts`          | `GET /all`, `GET /following`, `POST /create`, `POST /like/:id`, `POST /comment/:id`, `DELETE /:id` |
| Notifications  | `/api/notifications`  | `GET /`, `DELETE /`                                            |

All routes except signup/login/logout are protected by JWT auth middleware.

## Status

This is a **student/learning project** — a functional, feature-complete clone built to practice the MERN stack. The code covers the full auth-to-feed flow and works locally when the required environment variables are provided. There is no automated test suite, and it is not actively maintained.
