# Safe-Stay 🏡

A full-stack property listing platform where users can browse stays, post their own listings with photos, and leave reviews — kind of like a lightweight Airbnb clone, built from scratch.

**→ Live demo:** https://mern-project-jupb.onrender.com/listings

---

## What it does

Safe-Stay lets you:

- **Browse listings** — scroll through properties with images, prices, and locations
- **Post your own** — create a listing with a title, description, price, location, and a photo upload
- **Manage your listings** — edit or delete anything you've posted (nobody else can touch yours)
- **Leave reviews** — once you're logged in, you can rate and comment on any listing
- **Stay signed in** — sessions persist across page refreshes thanks to MongoDB-backed session storage

---

## Tech stack

| Layer | What I used |
|---|---|
| Runtime | Node.js 20.x |
| Server | Express 4 |
| Database | MongoDB + Mongoose 8 |
| Views | EJS + ejs-mate layouts |
| Auth | Passport, passport-local, passport-local-mongoose |
| Sessions | express-session + connect-mongo |
| Image uploads | Multer + multer-storage-cloudinary |
| Validation | Joi |

---

## Project structure

```
├── app.js            # Entry point — sets up Express, DB, sessions, Passport, routes
├── cloudconfig.js    # Cloudinary + Multer config
├── middleware.js     # Auth guards, owner checks, flash redirect helpers
├── schema.js         # Joi schemas for listings and reviews
├── models/           # Mongoose models: listing, review, user
├── routes/           # Route handlers split by feature
├── views/            # EJS templates
├── public/           # Static assets (CSS, JS, images)
└── util/             # Async wrapper, custom error class
```

---

## Running it locally

You'll need:
- **Node.js 20.x**
- A **MongoDB Atlas** cluster (or any MongoDB connection string)
- A **Cloudinary** account for image storage

**1. Clone and install**

```bash
git clone https://github.com/<your-username>/Safe-Stay.git
cd Safe-Stay
npm install
```

**2. Set up environment variables**

Create a `.env` file in the root — don't commit this:

```
ATLASDB_URL=your_mongodb_connection_string
SECRET=your_session_secret
CLOUD_NAME=your_cloudinary_cloud_name
CLOUD_API_KEY=your_cloudinary_api_key
CLOUD_API_SECRET=your_cloudinary_api_secret
```

**3. Start the server**

```bash
node app.js
```

Open http://localhost:8080/listings and you're good to go.

> Quick note: there's no `start` script in `package.json` yet, so use `node app.js` directly — or add `"start": "node app.js"` yourself if you prefer `npm start`.

---

## Routes

| Path | What it does |
|---|---|
| `GET /listings` | Browse all listings |
| `POST /listings` | Create a new listing (must be logged in) |
| `GET /listings/new` | New listing form |
| `GET /listings/:id` | View a single listing with its reviews |
| `GET /listings/:id/edit` | Edit form (owner only) |
| `POST /listings/:id/reviews` | Submit a review (must be logged in) |
| `/signup` `/login` `/logout` | Account management |

---

## Deploying

The live demo runs on **Render**. If you're deploying elsewhere, set the same environment variables on your host and make sure your MongoDB Atlas cluster allows connections from your deployment IP. For quick testing you can open access to `0.0.0.0/0` in Atlas, but lock that down before anything goes public.

Set `NODE_ENV=production` in your host environment — the app skips loading `.env` via dotenv in that mode and expects variables to be configured at the platform level.

---

## Contributing

Found a bug or want to add something? Fork the repo, create a branch, and open a PR with a short description of what you changed and why. Issues are open too if you just want to flag something.

---

## License

ISC
