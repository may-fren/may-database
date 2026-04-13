# Project Context

## 1. Genel Proje Tanımı & Amaç

**may-database**, MAY platformunun PostgreSQL veritabanını Docker Compose ile ayaklandırmak için kullanılan projedir. Kod barındırmaz, yalnızca veritabanı container konfigürasyonunu içerir.

- **Repo:** `may-database`
- **Veritabanı:** PostgreSQL 17
- **Container Orchestration:** Docker Compose

**Kardeş projeler:**
- `may-flyway` — Veritabanı migration (Flyway 10)

---

## 2. Mimari Kararlar & Prensipler

- **Persistent volume** — `may-postgres-data` named volume ile veri kalıcılığı sağlanır
- **Port mapping** — `5432:5432` ile host üzerinden erişim
- **Flyway ile ayrık yapı** — Migration işlemi ayrı bir proje (`may-flyway`) tarafından `host.docker.internal` üzerinden yapılır

---

## 3. Docker Compose Konfigürasyonu

```yaml
services:
  postgres:
    image: postgres:17
    container_name: may-database
    environment:
      POSTGRES_PASSWORD: 123456789
    ports:
      - "5432:5432"
    volumes:
      - may-postgres-data:/var/lib/postgresql/data

volumes:
  may-postgres-data:
```

---

## 4. Bağlantı Bilgileri

| Parametre | Değer |
|---|---|
| Host | localhost |
| Port | 5432 |
| User | postgres |
| Password | 123456789 |
| Schema | MAY (flyway tarafından oluşturulur) |

---

## 5. Dosya Yapısı

```
may-database/
├── .gitignore
├── docker-compose.yml
├── project-context.md
└── README.md
```
