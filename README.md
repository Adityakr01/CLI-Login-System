# CLI Login System with 2FA

A simple command line login system made with Go and SQLite. You can register, login, and protect your account with Google Authenticator.

---

## Requirements

- Go 1.22
- Docker (optional)
- GCC / C compiler (needed for SQLite)

---

## How to Run

### Option 1 - Run Locally

```bash
go mod tidy
go run ./cmd/clilogin
```

### Option 2 - Run with Docker

```bash
docker compose run --rm clilogin
```

Your data will be saved automatically and will not be deleted even if you restart the container.

---

## Commands

**Before login:**

| Command | What it does |
|---|---|
| `register` | Create a new account |
| `login` | Login with your username and password |
| `help` | Show available commands |
| `exit` | Close the app |

**After login:**

| Command | What it does |
|---|---|
| `whoami` | Show your account details |
| `enable-2fa` | Turn on 2FA using Google Authenticator |
| `disable-2fa` | Turn off 2FA |
| `logout` | End your session |
| `help` | Show available commands |

---

## How to Setup 2FA

1. Login to your account
2. Type `enable-2fa`
3. A secret key and a URL will be shown
4. Open **Google Authenticator** on your phone
5. Tap **+** then tap **Enter a setup key**
6. Paste the secret key shown in the terminal
7. Enter the 6 digit code from the app to confirm
8. Done — 2FA is now active on your account

Next time you login, it will ask for the 6 digit code after your password.

---

## Security

- Passwords are never saved as plain text — they are hashed using bcrypt
- Account gets locked for 5 minutes after 5 wrong password attempts
- Login session expires automatically after 15 minutes
- 2FA uses the TOTP standard so it works with any authenticator app

---

## Project Structure

```
cmd/clilogin/main.go   - app entry point
internal/auth/         - password hashing, 2FA, session tokens
internal/cli/          - commands and shell logic
internal/db/           - database connection and schema
internal/models/       - user and session data types
internal/repo/         - database queries
Dockerfile             - docker build config
docker-compose.yml     - docker run config
```

---

## Run Tests

```bash
go test ./...
```
