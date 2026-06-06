# Project ELLE: Full-Stack Deployment Guide

Now that your code is securely on GitHub, we're ready to deploy! We will split this into two parts:
1. **Frontend**: Deployed to Vercel (extremely fast, great for React/Vite apps).
2. **Backend**: Deployed to Render (great for Python/Flask APIs).

---

## Part 1: Deploying the Backend to Render.com

We deploy the backend first because your frontend needs to know the **live backend URL** to communicate with it.

1. Go to [Render.com](https://render.com/) and sign up/log in with your GitHub account.
2. At the top right, click **New** and select **Web Service**.
3. Select **"Build and deploy from a Git repository"** and click **Next**.
4. Connect your new `elle-microplastic-detector` GitHub repository and select it.
5. Fill out the configuration for the Web Service:
   - **Name**: `elle-backend` (or similar)
   - **Branch**: `main`
   - **Root Directory**: `backend` *(⚠️ VERY IMPORTANT: Render must know your backend is inside the `backend/` folder!)*
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt` (Render should auto-detect this, but double check).
   - **Start Command**: `gunicorn app:app` (Render reads this from your `Procfile`, so this should be automatic).
6. Under **Environment Variables**, you must add your secret keys (since we ignored the `.env` file):
   - **Key:** `GEMINI_API_KEY` | **Value:** *(paste your Gemini API key)*
   - **Key:** `MONGO_URI` | **Value:** *(paste your MongoDB connection string)*
7. Scroll down to the bottom and click **Create Web Service**.

> [!NOTE]
> Render will now start building your Python backend. This can take 5-10 minutes. Once it completes, Render will give you a live URL at the top left (e.g., `https://elle-backend-xyz.onrender.com`). **Copy this URL**, you'll need it for the frontend!

---

## Part 2: Deploying the Frontend to Vercel

1. Go to [Vercel.com](https://vercel.com/) and sign up/log in with your GitHub account.
2. On your dashboard, click **Add New** > **Project**.
3. Under "Import Git Repository", find your `elle-microplastic-detector` repo and click **Import**.
4. In the **Configure Project** screen:
   - **Framework Preset**: Vercel should automatically detect `Vite`.
   - **Root Directory**: Click the "Edit" button and select the `frontend` folder! *(⚠️ VERY IMPORTANT!)*
5. Open the **Environment Variables** dropdown and add:
   - **Key:** `VITE_API_URL`
   - **Value:** *(Paste your LIVE Render backend URL here. Make sure there is NO trailing slash at the end. Example: `https://elle-backend-xyz.onrender.com`)*
6. Click **Deploy**.

> [!TIP]
> Vercel is extremely fast and should finish building in under 1-2 minutes. Once done, Vercel will give you a live `.vercel.app` domain for your frontend!

---

## Part 3: Final Verification

1. Go to your new live Vercel frontend link.
2. Try logging in or testing the application.
3. Make sure the dashboard/analysis pages correctly connect to the Render backend and the MongoDB database.

If anything fails, check the **Logs** tab on Render (for backend errors) or the Vercel logs/browser developer console (for frontend errors). Let me know if you hit any roadblocks!
