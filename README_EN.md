# Safe Paste

[繁體中文](README.zh-TW.md)

A privacy-first browser tool that automatically redacts passwords, API keys, tokens, and other secrets before you share logs or terminal output.

## Why Safe Paste?

When copying terminal output, Docker logs, configuration files, or debugging information into ChatGPT, coding agents, issue trackers, or team chats, it is easy to accidentally include credentials.

Safe Paste provides a simple local-first checkpoint before sharing that text.

## Features

- Automatically redacts common passwords, API keys, secrets, and tokens with `***`
- Detects common Authorization Bearer and Basic credentials
- Redacts credentials embedded in connection URLs
- Recognizes common credential formats including OpenAI, GitHub, GitLab, Slack, Google, AWS, Stripe, JWTs, and private keys
- Warns about high-entropy strings that may be unknown secrets without automatically destroying useful debugging data
- Optional aggressive field detection
- One-click copy of sanitized output
- Responsive layout designed for desktop and mobile browsers
- Automatic light and dark mode support
- No backend required

## Privacy

Safe Paste performs processing entirely inside your browser.

The current implementation does not intentionally send pasted text to a server or store it in `localStorage`, cookies, or IndexedDB. The application is a static HTML page and does not require an API or backend service.

For highly sensitive material, review the source and deployment environment yourself before use.

## Usage

1. Open Safe Paste in your browser.
2. Paste terminal output, logs, configuration, or other text into the input field.
3. Safe Paste automatically scans and redacts recognized secrets.
4. Review any yellow warnings for suspicious strings that could not be classified safely.
5. Click the copy button and paste the sanitized result wherever you need it.

Example input:

```text
password="hello123"
OPENAI_API_KEY=sk-example-secret-value
Authorization: Bearer example-token-value
DATABASE_URL=postgresql://user:password@localhost/db
```

Example output:

```text
password="***"
OPENAI_API_KEY=***
Authorization: Bearer ***
DATABASE_URL=postgresql://user:***@localhost/db
```

## Run locally

No build process or dependencies are required. Clone the repository and open `index.html` in a modern browser.

```bash
git clone https://github.com/nkhs9412235/safe-paste.git
cd safe-paste
open index.html
```

Clipboard APIs may have additional browser security requirements depending on how the page is opened. Serving the directory through a local HTTP server can provide more consistent clipboard behavior.

## Important limitation

Secret detection is heuristic. No regular-expression or entropy-based scanner can guarantee detection of every custom credential format. Safe Paste should be treated as an additional safety layer, not as a complete DLP or secret-management system.

## License

No license has been specified yet.
