 ```markdown
# 🛍 ERD - Online Clothing Store (Django + HTMX + Alpine.js)

## 🌟 Project Features
- **Modern stack**: Django + HTMX + Alpine.js
- **Two payment systems**: Stripe and Heleket (crypto)
- **Docker containerization** with PostgreSQL
- **Custom user model**
- **Secured settings** (CSRF, HTTPS, Security Headers)

## 🚀 Project Launch

### 1. Local Launch (without Docker)

1. Install dependencies:
```bash
python -m pip install -r requirements.txt
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate    # Windows
```

3. Set up environment variables:
```
# Fill in your values in .env (example .env below)
```

4. Run migrations:
```bash
python manage.py migrate
```

5. Create a superuser:
```bash
python manage.py createsuperuser
```

6. Start the server:
```bash
python manage.py runserver
```

### 2. Server Launch (with SSL)

1. Prepare your domain:
   - Set the DNS record for `domen.com` to your IP

2. Configure `.env`:
```ini
SECRET_KEY='example'

POSTGRES_DB=enfdb
POSTGRES_USER=enfdb
POSTGRES_PASSWORD=enfdb
POSTGRES_HOST=localhost # use 'db' if running on VPS
POSTGRES_PORT=5432

STRIPE_SECRET_KEY='example'
STRIPE_WEBHOOK_SECRET='example'

HELEKET_API_KEY='example'
HELEKET_SECRET_KEY='example'
```

3. Obtain certificates (certbot):
```bash
sudo certbot --nginx -d domen.com -d www.domen.com
```

4. Build the container:
```bash
docker-compose up --build -d
```

5. Collect static files:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```

## 🔒 Security Settings
The project is pre-configured with:
- CSRF protection
- Secure cookies
- Security Headers
- HTTPS when running via Docker

## 🌍 Site Access
- Locally: [http://localhost:8000](http://localhost:8000)
- In Docker with SSL: [https://domen.com](https://domen.com)

## ⚙️ Important settings from settings.py
```python
# Security
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('POSTGRES_DB'),
        # ... other parameters
    }
}

# Payment systems
STRIPE_SECRET_KEY = os.getenv('STRIPE_SECRET_KEY')
HELEKET_API_KEY = os.getenv('HELEKET_API_KEY')
```

## 🛠 Deployment Guide
[https://github.com/s6ptember/for-deploy-guide.git]
```
