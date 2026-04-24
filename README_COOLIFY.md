# Hosting 9Router on Coolify

To host 9Router on Coolify, follow these steps:

## 1. Prerequisites
- A running Coolify instance.
- Your 9Router repository pushed to GitHub/GitLab (or any Git provider).

## 2. Setup in Coolify

1. **Create a New Project/Service**:
   - In Coolify, go to **Projects** and select or create a project.
   - Click **+ New Resource**.
   - Select **Docker Compose**.

2. **Configure the Repository**:
   - Choose your Git source (e.g., GitHub).
   - Select the `9router` repository.
   - Select the branch you want to deploy.

3. **Docker Compose Configuration**:
   - Coolify should automatically detect the `docker-compose.yml` file I just created.
   - If it doesn't, paste the content of `docker-compose.yml` into the configuration area.

4. **Environment Variables** (Optional):
   - `JWT_SECRET`: A secret string for signing authentication tokens.
   - `INITIAL_PASSWORD`: The initial password for the dashboard (default: `123456`).
   - `AUTH_COOKIE_SECURE`: Set to `true` if you are using HTTPS (which Coolify usually provides).
   - `DATA_DIR`: Set to `/app/data` (already set in `docker-compose.yml`).

5. **Networking**:
   - Coolify will automatically detect port `20128`.
   - You can set up your custom domain in the **Domains** section of the service settings. Coolify will handle the SSL certificate (via Let's Encrypt) and reverse proxy automatically.

6. **Persistent Storage**:
   - The `9router-data` volume defined in `docker-compose.yml` will be managed by Coolify. This ensures your settings and database are preserved across deployments.

7. **Deploy**:
   - Click **Deploy**.

## 3. Post-Deployment
Once deployed, you can access your 9Router dashboard at the domain you configured.

---

### Troubleshooting: Submodule Clone Failure
If your deployment fails with a `fatal: could not read Username for 'https://github.com'` error during the clone stage, it is likely due to the private `src/mitm/dev` submodule.

**Solution:**
1. Go to your Service settings in Coolify.
2. In the **General** settings, find the **Install Submodules** toggle.
3. Turn it **OFF**.
4. Redeploy.

The `src/mitm/dev` directory is optional and used for local development overrides; it is not required for the production application to function.
