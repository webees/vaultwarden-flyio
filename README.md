# fly.toml
```toml
app = "vaultwarden"
primary_region = "hkg"
kill_signal = "SIGINT"
kill_timeout = 10
processes = []

[build]
image = "vaultwarden/server:latest"

[env]
DOMAIN="https://pass.dev.run"
SROCKET_WORKERS=1
WEBSOCKET_ENABLED=true
SIGNUPS_ALLOWED=false
SHOW_PASSWORD_HINT=false
# - ADMIN_TOKEN="88888888"
SMTP_HOST="smtp.gmail.com"
SMTP_PORT=587
SMTP_FROM="xxxxxxxx@gmail.com"
SMTP_USERNAME="xxxxxxxx@gmail.com"
SMTP_PASSWORD="xxxxxxxxxxxxxxxx"
DATABASE_URL="postgresql://xxxxxxxx:xxxxxxxx@db.bit.io:5432/xxxxxxxx.vaultwarden"

[mounts]
source="vaultwarden_data"
destination="/data"

[experimental]
allowed_public_ports = []
auto_rollback = true

[[services]]
internal_port = 80
protocol = "tcp"
auto_stop_machines = true
auto_start_machines = true
processes = ["app"]

[services.concurrency]
hard_limit = 25
soft_limit = 20
type = "connections"

[[services.ports]]
force_https = true
handlers = ["http"]
port = 80

[[services.ports]]
handlers = ["tls", "http"]
port = 443

[[services.tcp_checks]]
grace_period = "1s"
interval = "15s"
restart_limit = 0
timeout = "2s"
```
