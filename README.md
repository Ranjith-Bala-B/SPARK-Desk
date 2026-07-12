# SPARK Desk
# SPARK - Student Platform for Action, Resolve & Keep tracking.

A hostel complaint management system built for **SECE (Sri Eshwar College of Engineering)** students to report and track hostel issues, and for wardens/admins to manage and resolve them efficiently.

Live grievance portal → complaint submission → auto-prioritization → admin dashboard → resolution tracking.

---

## ✨ Features

**For Students**
- Sign in with official `@sece.ac.in` email (password login or Google OAuth)
- Submit complaints with category, room/block/floor details, description, and an optional photo
- Automatic priority tagging (Low / Medium / High) based on complaint description
- Track status of submitted complaints (Pending → In Progress → Resolved)
- View hostel notices relevant to their block
- Editable student profile

**For Admins/Wardens**
- Centralized dashboard with live stats (total, pending, in progress, resolved)
- Visual analytics — category breakdown, priority split, block-wise and hostel-wise (Boys/Girls) charts, monthly trends
- Update complaint status and add admin notes
- Manage warden contact details per block
- Post and manage hostel notices
- Generate and download filtered reports (by hostel, block, category, date range) as CSV
- Printable report view

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Database | SQLite (dev) / PostgreSQL (production, via `DATABASE_URL`) |
| ORM | Flask-SQLAlchemy |
| Auth | Session-based login + Google OAuth 2.0 (Authlib) |
| Frontend | Jinja2 templates, vanilla CSS/JS |
| Charts | Chart.js |
| Deployment | Render (Gunicorn WSGI) |

---

## 📂 Project Structure

```
Hostel/
├── app.py                # Main Flask application (routes, models, logic)
├── wsgi.py                # WSGI entry point for Gunicorn
├── render.yaml             # Render deployment config
├── requirements.txt
├── static/
│   ├── hostelimage.png
│   └── uploads/            # Complaint images
└── templates/
    ├── login.html
    ├── welcome.html         # Student/Admin dashboard
    ├── complaint.html
    ├── reports.html
    ├── report_print.html
    ├── wardens.html
    └── notices.html
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- pip

### Installation

```bash
git clone https://github.com/<your-username>/FixMyHostel.git
cd FixMyHostel/Hostel
pip install -r requirements.txt
```

### Environment Variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key
GOOGLE_CLIENT_ID=your-google-oauth-client-id
GOOGLE_CLIENT_SECRET=your-google-oauth-client-secret
ADMIN_PASSWORD=your-admin-password

# Optional — omit to use local SQLite
DATABASE_URL=postgresql://user:password@host/dbname
```

### Run Locally

```bash
python app.py
```

The app will be available at `http://localhost:5000`.

Default admin login:
```
Email: admin@sece.ac.in
Password: <ADMIN_PASSWORD from .env>
```

---

## ☁️ Deployment (Render)

This repo includes a `render.yaml` for one-click deployment:

1. Push the repo to GitHub
2. Create a new **Blueprint** on [Render](https://render.com) and point it to this repo
3. Render provisions a free PostgreSQL database and a web service automatically
4. Set `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, and `ADMIN_PASSWORD` as environment variables in the Render dashboard (do **not** commit real secrets to `render.yaml`)

---

## 🔐 Notes on Security

- Google OAuth is restricted to `@sece.ac.in` accounts
- Security headers (`X-Frame-Options`, `X-Content-Type-Options`, etc.) are set on every response
- Uploaded images are validated by extension and stored with randomized filenames

> This project is a hackathon prototype. Password hashing, CSRF protection, and rate limiting are on the roadmap before any production use with real student data.

---

## 🗺 Roadmap

- [ ] Password hashing (bcrypt/werkzeug)
- [ ] CSRF protection on all forms
- [ ] SMS/WhatsApp notifications on status change (Twilio)
- [ ] SLA-based auto-escalation for unresolved high-priority complaints
- [ ] Duplicate complaint clustering
- [ ] PDF report export
- [ ] QR-code room prefill for faster complaint submission

---

## 👥 Team

Built for Sri Eshwar College of Engineering (SECE) hostel grievance management.

---

## 📄 License

This project is for academic/hackathon use. Add a license of your choice (MIT recommended) if open-sourcing.
