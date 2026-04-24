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

### Important Notes
- **Port**: The application runs on port `20128` inside the container.
- **Storage**: All data is stored in `/app/data` inside the container, which is mapped to a persistent volume.
