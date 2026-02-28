# LAB07 & Assignment 07: Full-Stack Web Application with Docker Compose

## Student Information
| Field | Value |
|---|---|
| **Student ID** | 1660702778 |
| **Full Name** | Thitipat Chueayarerom |
| **Username** | thitipatpleng |
| **Email** | thitipat.chue@bumail.net |

---

## Project Structure
```
assignment-07/
├── compose.yaml              # Docker Compose configuration
├── .env                      # Environment variables
├── nginx/
│   └── my-nginx.conf         # Nginx config (Docker Configs)
├── secret/
│   ├── .db_root_pass.txt     # MySQL root password (Docker Secrets)
│   └── .db_user_pass.txt     # MySQL user password (Docker Secrets)
├── seed-data.sql             # SQL seed data for phpMyAdmin
├── app/
│   └── index.php             # PHP application file
└── README.md
```

---

## Services
| Service | Image | Container Name | Port |
|---|---|---|---|
| db-server | mysql:8.0 | thitipatpleng-db | - |
| backend-php | bitnami/php-fpm:latest | thitipatpleng-php | - |
| web-proxy | nginx:latest | thitipatpleng-web | 8080:80 |
| db-management | phpmyadmin:latest | thitipatpleng-pma | 8888:80 |

## Networks
| Network | Services | Purpose |
|---|---|---|
| frontend-zone | web-proxy, db-management | User-facing access |
| backend-zone | db-server, backend-php, web-proxy, db-management | Internal communication |

---

## How to Run

### 1. Start all services
```bash
docker compose up -d
```

### 2. Verify containers are running
```bash
docker compose ps -a
```

### 3. Access the applications
- **Web Application:** http://localhost:8080
- **phpMyAdmin:** http://localhost:8888

### 4. Seed the database
1. Open phpMyAdmin at http://localhost:8888
2. Login with username `root` and the root password
3. Select the `my_app_db` database
4. Go to the **SQL** tab
5. Paste the contents of `seed-data.sql` and execute

### 5. View the result
- Refresh http://localhost:8080 to see the student data table

### 6. Stop all services
```bash
docker compose down
```

### 7. Stop and remove volumes
```bash
docker compose down -v
```
