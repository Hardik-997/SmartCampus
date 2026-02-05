# Deployment Guide for Vercel

Your full-stack application is now ready to be deployed to Vercel! I have configured the project to serve the Frontend as the main site and the Backend as Serverless Functions under `/api`.

## Changes Made:
1.  **`vercel.json`**: Created to configure routing. All requests to `/api/*` are routed to the backend, while other requests serve the frontend.
2.  **`api/index.js`**: Created an entry point for Vercel to load your Express app.
3.  **`backend/server.js`**: Modified to ensure it doesn't try to start a persistent server when running in the serverless environment.
4.  **`package.json`**: Merged backend dependencies into the root `package.json` so Vercel can install them.

## How to Deploy

### Option 1: Using GitHub (Recommended)
1.  Push your code to a GitHub repository.
2.  Log in to [Vercel](https://vercel.com).
3.  Click "Add New..." -> "Project".
4.  Import your GitHub repository.
5.  Vercel should automatically detect the `vercel.json` configuration.
6.  **Important**: Before clicking "Deploy", go to the **Environment Variables** section and add your secrets:
    *   `MONGO_URI`
    *   `JWT_SECRET`
    *   `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, etc.
7.  Click **Deploy**.

### Option 2: Using CLI
1.  Run the following command in your terminal:
    ```bash
    npx vercel
    ```
2.  Follow the prompts:
    *   Set up and deploy? **Y**
    *   Which scope? (Select your account)
    *   Link to existing project? **N**
    *   Project name? (Press Enter)
    *   In which directory is your code located? **./** (Press Enter)
    *   Want to modify these settings? **N** (Our `vercel.json` handles it)
3.  After the build setup, it will ask for Environment Variables? You might need to add them via the dashboard or CLI using `npx vercel env add`.

## Post-Deployment
Once deployed, your frontend will be at `https://your-project.vercel.app` and your API will be accessible at `https://your-project.vercel.app/api/...`.
