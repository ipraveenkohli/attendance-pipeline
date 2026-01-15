# attendance-pipeline

RealTech Attendance Pipeline
Purpose
Lightweight pipeline to ingest attendance events from RealTech devices, store them, and stream live updates to a web frontend.

Features
- Real‑time WebSocket/SSE broadcast of attendance events
- Durable ingestion with queueing and deduplication
- Persistent storage for audit and reporting
- Modular device connectors for different RealTech protocols

Quick Start
- Clone repo and set environment variables for DB, queue, and API.
- Install dependencies (npm install or pip install -r requirements.txt).
- Migrate DB (npm run migrate or alembic upgrade head).
- Run services: collector, worker, API, and frontend (or docker-compose up if provided).
Essential env vars
- DATABASE_URL
- REDIS_URL or Kafka config
- API_HOST, API_PORT, JWT_SECRET
- DEVICE_DISCOVERY_SUBNET, DEVICE_POLL_INTERVAL

API Endpoints
- GET /api/v1/events?limit=50 — recent events
- POST /api/v1/devices/:id/ack — acknowledge device
- Realtime: connect to wss://HOST/realtime with JWT to receive attendance_event messages

Data Model
- employees: id, employee_id, name, department
- devices: id, device_id, ip, model, location, last_seen
- attendance_events: id, employee_id, device_id, event_type, timestamp, raw_payload

Deployment Notes
- Ensure network access between devices and collector.
- Secure endpoints with TLS and JWT.
- Monitor device heartbeats, queue lag, and processing errors.
- Backup DB and set retention for raw payloads.
