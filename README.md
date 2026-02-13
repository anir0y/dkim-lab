# DKIM Replay Attack Lab

An interactive lab to understand email authentication, DKIM replay attacks, and defenses. Built for teaching freshers about email security vulnerabilities.

**Live:** [lab-dkim.anir0y.in](https://lab-dkim.anir0y.in)

## What It Does

1. **Generate a DKIM-signed email** -- simulates a legitimate mail server signing an outgoing message
2. **Launch a replay attack** -- resends the signed email to see if the receiving server accepts it
3. **Compare Vulnerable vs Secure modes** -- Secure mode enforces signature expiry (`t=` timestamp), blocking replayed messages after 5 seconds

## Stack

- **Runtime:** Cloudflare Workers
- **Crypto:** Web Crypto API (RSA-SHA256, 2048-bit)
- **Frontend:** Bootstrap 5.3, Font Awesome, Catppuccin-style dark theme
- **Single-file Worker** with base64-encoded HTML template

## Project Structure

```
src/index.js          # Cloudflare Worker (routes + inline HTML)
templates/index.html  # Source HTML template
wrangler.toml         # Cloudflare Workers config
```

## Routes

| Method | Path                  | Description                        |
|--------|-----------------------|------------------------------------|
| GET    | `/`                   | Serves the lab UI                  |
| POST   | `/sign`               | Generate a DKIM-signed email       |
| POST   | `/verify`             | Verify DKIM signature (replay check) |
| POST   | `/check_vulnerability`| Domain vulnerability scanner       |

## Local Development

```bash
npm install
npm start        # runs wrangler dev
```

## Deploy

```bash
npm run deploy   # runs wrangler deploy
```

## License

ISC
