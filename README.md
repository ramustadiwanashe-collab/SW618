# WODASHTECH Public Website

Render-ready Flask version of the WODASHTECH application.

## Render deployment

### Option A: Render Blueprint

1. Push this folder to GitHub.
2. In Render, choose **New > Blueprint** and select the repository.
3. Render reads `render.yaml`, creates the Flask web service and PostgreSQL database, and supplies `DATABASE_URL` automatically.
4. Confirm the generated `SECRET_KEY` environment variable.
5. Deploy.

### Option B: Manual Web Service

Build command:

```text
pip install -r requirements.txt
```

Start command:

```text
gunicorn app:app
```

Set these environment variables:

```text
SECRET_KEY=<long-random-secret>
DATABASE_URL=<Render Postgres connection string>
PYTHON_VERSION=3.13.5
```

## Local development

If `DATABASE_URL` is not set, the app uses SQLite locally.

```bash
pip install -r requirements.txt
python app.py
```

Open `http://127.0.0.1:5000`.

## Important production note

The account/document metadata is stored in PostgreSQL when `DATABASE_URL` is present. Uploaded document files are currently stored on the service filesystem. Render web service filesystems are ephemeral by default, so production document storage should be moved to object storage or another persistent storage service before relying on uploads. See Render's filesystem documentation for persistent-storage options.

Password reset email delivery is also a placeholder until an email provider is configured.
