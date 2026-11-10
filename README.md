# Brahma User Management — User Management Portal

A full-stack user management application with JWT authentication and role-based permissions. Admins and managers can create, update, search and delete users. Users can register, log in, reset their password by email and upload a profile picture.

**Tech stack:** Java · Spring Boot · Spring Security · JWT · Spring Data JPA · MySQL · JavaMail · Guava · Angular · Bootstrap

---

## Features

- **Registration and login** with JWT. The token is returned in the `Jwt-Token` response header.
- **Roles and authorities:** `ROLE_USER`, `ROLE_HR`, `ROLE_MANAGER`, `ROLE_ADMIN` and `ROLE_SUPER_ADMIN`, each with its own set of authorities (`user:read`, `user:create`, `user:update`, `user:delete`)
- **Brute-force protection:** accounts lock after repeated failed logins, using a Guava cache-based login-attempt tracker
- **Password reset by email:** a new random password is generated and emailed through Gmail SMTP
- **Profile images:** upload, store on the file system and serve; a default avatar is generated for new users
- **User administration:** add, update, delete, list and search users; activate/deactivate and lock/unlock accounts
- **Centralised exception handling** returning consistent JSON error responses
- **Angular client** with an auth guard, an HTTP interceptor that attaches the JWT, and notifications

---

## API endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/user/register` | Register a new user |
| POST | `/user/login` | Log in and receive a JWT |
| POST | `/user/add` | Add a user (admin) |
| POST | `/user/update` | Update a user |
| GET | `/user/find/{username}` | Find a user |
| GET | `/user/list` | List all users |
| GET | `/user/resetpassword/{email}` | Email a new password |
| DELETE | `/user/delete/{username}` | Delete a user (requires `user:delete`) |
| POST | `/user/updateProfileImage` | Upload a profile image |
| GET | `/user/image/{username}/{fileName}` | Get a profile image |

---

## Project structure

```
brahma-user-management/
├── backend/    Spring Boot REST API (com.brahma.usermanagement)
│   ├── configuration   Spring Security configuration
│   ├── filter          JWT authorization filter, entry point, access-denied handler
│   ├── utility         JWT token provider
│   ├── listener        login success / failure listeners
│   ├── service         user, email and login-attempt services
│   ├── resource        REST controller
│   └── exception       global exception handling
└── frontend/   Angular client
```

---

## Running the project

**Backend**
1. Create a MySQL database named `usermanagement`.
2. Add the variables from `.env.example` to your IntelliJ Run Configuration → Environment variables.
3. Run `UserManagementApplication`. The API starts on port `8081`.

**Frontend**
```bash
cd frontend
npm install
ng serve
```
Open `http://localhost:4200`.

### Environment variables

| Variable | Purpose |
|---|---|
| `DB_URL`, `DB_USERNAME`, `DB_PASSWORD` | MySQL connection |
| `JWT_SECRET` | JWT signing secret |
| `MAIL_USERNAME`, `MAIL_PASSWORD` | Gmail account and app password for sending reset emails |
| `MAIL_FROM` | Sender address (defaults to `MAIL_USERNAME`) |

---

## Author

**Brahmananda S** — Java Full Stack Developer, Bangalore
[LinkedIn](https://www.linkedin.com/in/brahmananda) · brahmananda.a.s@gmail.com
