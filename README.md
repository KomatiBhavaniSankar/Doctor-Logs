# Doctor GenAI Simulation

- Doctor app:  http://localhost:8003/
- Admin portal: http://localhost:8003/admin   (password = ADMIN_PASSWORD in .env)

## Run
    pip install -r requirements.txt
    uvicorn main:app --reload

## Upgrading an existing database
Run `migrate.sql` once in Supabase > SQL Editor. Until you do, everything still works,
but device info and exact per-event timestamps are not stored.

## Admin portal
Overview (Busy vs Quiet, per-scenario and per-page stats), Doctors, Sessions (with full
event log per session), Activity log (filter/search everything), Records, and CSV export of
events / sessions / doctors / records for analysis.

## Docker (port 8003)
    cp .env.example .env      # then fill in SUPABASE_URL, SUPABASE_KEY, ADMIN_PASSWORD
    docker compose up -d --build

- Doctor app:   http://localhost:8003/
- Admin portal: http://localhost:8003/admin

Logs: `docker compose logs -f` | Stop: `docker compose down` | Update: `git pull && docker compose up -d --build`

Without compose:

    docker build -t doctor-sim .
    docker run -d --name doctor-sim -p 8003:8003 --env-file .env --restart unless-stopped doctor-sim

The `.env` file is not baked into the image (see `.dockerignore`); it is passed at runtime.
