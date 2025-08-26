# RealRoll

RealRoll is a Flask-based short-form video app (Reels/TikTok style) where users can upload, browse, and manage videos. It includes creator/consumer modes, profiles, and notifications. Storage is backed by Supabase, and data is stored in Azure SQL via SQLAlchemy.

## Features

- User authentication and registration
- Video upload to Supabase Storage
- Consumer feed browsing
- Creator dashboard for content management
- Profiles with bio and avatar
- Likes, comments, ratings, notifications
- Responsive HTML/CSS frontend

## Tech Stack

- Backend: Flask
- ORM/Migrations: SQLAlchemy + Flask-Migrate
- Database: Azure SQL (via `pyodbc`)
- Storage: Supabase buckets (`RealRoll`, `avatars`)
- Sessions: Flask-Session (filesystem)
- CI/CD: GitHub Actions → Azure Web App

## Getting Started

1) Clone and enter the project
```bash
git clone <your-repo-ssh-or-https-url>
cd realroll
```

2) Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

3) Install dependencies
```bash
pip install -r requirements.txt
```

4) Environment variables
Create a `.env` file in the project root with at least:
```
Please request the secrets from the owner.
```

5) Initialize the database
```bash
export FLASK_APP=app.py  # Windows PowerShell: setx FLASK_APP app.py (then reopen shell)
flask db upgrade
```

6) Run the app
```bash
python app.py
```
Visit http://localhost:5000

## Project Structure

```
realroll/
├── app.py                # Flask application
├── requirements.txt      # Dependencies
├── migrations/           # Alembic migrations
├── static/               # CSS and assets
├── templates/            # Jinja2 templates
├── .github/workflows/    # CI/CD (Azure deploy)
└── README.md
```

## Deployment (GitHub Actions → Azure Web App)

This repo includes a workflow at `.github/workflows/main_realroll.yml`.

1) In your GitHub repo, add the following Actions secrets (Settings → Secrets and variables → Actions):
   - `AZUREAPPSERVICE_CLIENTID_9E738BEB976D428594193AE4C6207B99`
   - `AZUREAPPSERVICE_TENANTID_A5F6051A946E423487A6EB4062487D2D`
   - `AZUREAPPSERVICE_SUBSCRIPTIONID_B23C360DF64E41FC81DDA66EC8E23A32`

2) Ensure `app-name` in the workflow matches your Azure Web App name.

3) Push to `main`. The workflow will build and deploy.

## Notes

- Requirements: If you use environment loading or Supabase, ensure `python-dotenv` and `supabase` are installed. Add them to `requirements.txt` if missing:
  ```
  python-dotenv
  supabase
  ```
- SSH pushing to GitHub is supported. Make sure your SSH key is added to your GitHub account and that the remote is set to `git@github.com:<you>/RealRoll.git`.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a pull request

## License

MIT
