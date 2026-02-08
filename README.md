# Valentine site – host on Ubuntu

One file: **index.html** (HTML, CSS, and JS inline).

## Quick serve (testing)

```bash
cd /path/to/valentine
python3 -m http.server 8080
```

Then open `http://VM_IP:8080`. Your reverse proxy can point to `http://127.0.0.1:8080` and handle HTTPS.

## Production (nginx behind your reverse proxy)

1. Copy the `valentine` folder to the VM (e.g. `/var/www/valentine`).
2. Example nginx site:

```nginx
server {
    listen 80;
    server_name your-domain-or-ip;
    root /var/www/valentine;
    index index.html;
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

3. Your reverse proxy terminates HTTPS and forwards to this nginx (or directly to a backend). No cert needed in this app.

## Mobile

The page uses `viewport` and responsive units (`clamp`, `vw`, etc.) so it works on phones. The “No” button runs away on both click and touch.
