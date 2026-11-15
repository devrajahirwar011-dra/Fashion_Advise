# StyleMate AI

## Deploy to Vercel

Import the repository into Vercel and set the **Root Directory** to the repository root (the folder containing `vercel.json`). The root Vercel configuration builds the Vite app from `frontend` and routes `/api/*` and `/uploads/*` to the FastAPI function in `api/index.py`.

Configure these Vercel environment variables before deploying:

- `SECRET_KEY`: a long, random secret used to sign authentication tokens.
- `DATABASE_URL`: a PostgreSQL connection URL from a hosted provider such as Neon or Supabase. Use a URL with SSL enabled (for example `postgresql://...?...sslmode=require`).

The app falls back to SQLite in `/tmp` if `DATABASE_URL` is omitted on Vercel. That fallback is only for a quick deployment check: serverless temporary storage is not durable, so user accounts and wardrobe data can disappear. Set a hosted PostgreSQL URL for a usable multi-user deployment.

Uploads are stored in the function's temporary directory on Vercel and are not durable across deployments or function instances. Use persistent object storage for production wardrobe images.

## Local development

- Frontend: `cd frontend; npm install; npm run dev`
- Backend: `cd backend; ..\\.venv\\Scripts\\python.exe -m uvicorn app.main:app --reload --port 8000`

The frontend uses `/api` by default; Vite proxies it to the local API at `http://localhost:8000`.
