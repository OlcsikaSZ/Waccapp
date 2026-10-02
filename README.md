# WaccApp — WhatsApp Business Messaging & Questionnaire Platform

WaccApp is a web-based messaging and questionnaire automation platform built around the **WhatsApp Business / Meta Graph API**. It provides a single interface for sending text, template and media messages, scheduling communication, processing incoming replies through webhooks, and managing questionnaire flows.

The project was built with a **Node.js / Express** backend and **SQLite** persistence, with a lightweight multi-page frontend using native **HTML, CSS and JavaScript**.

## Main Features

- Send WhatsApp **text messages** to one or multiple recipients
- Send approved **WhatsApp template messages** with parameters
- Send **images and documents** through the Meta Graph API
- Receive and process incoming messages through a **webhook**
- Respect the WhatsApp **24-hour customer service window** for free-form messages
- Schedule text, template, questionnaire and media messages
- Manage **button-based template questionnaire flows**
- Manage **text-based branching questionnaires**
- Track questionnaire state and continue flows automatically after a reply
- View incoming and outgoing conversations in a chat-style interface
- Filter and analyse communication by recipient, type, date and questionnaire/theme
- Store message metadata and media references for later review
- Role-based administration and user management
- Audit logging and consent-related data handling
- Email-based account verification and account management

## Tech Stack

### Backend
- Node.js
- Express
- Meta Graph API / WhatsApp Business API
- Axios
- SQLite3
- Express Session + connect-sqlite3
- bcryptjs
- node-cron
- Multer
- Nodemailer

### Frontend
- HTML
- CSS
- JavaScript

### Security & Reliability
- Session-based authentication
- Password hashing with bcrypt
- Role-based access control
- Login / account-action rate limiting
- Webhook signature verification support
- Input validation
- Audit logging
- Environment-based configuration

## Application Modules

The frontend is split into several focused pages under `public/`:

- `index.html` — main messaging interface
- `conv.html` — conversation / chat view
- `filter.html` — filtering and analysis
- `template.html` — template-based questionnaire editor
- `questionnaire.html` — text-questionnaire editor
- `sent-messages.html` — outgoing-message history
- `admin.html` — administration and user management
- `account.html` — account settings
- `login.html` — authentication
- `privacy.html` — privacy information

## Project Structure

```text
project/
├── app.js                  # Express server, API endpoints, webhook and business logic
├── questionnaire.js        # Questionnaire definitions and branching logic
├── package.json            # Dependencies and start script
├── .env.example            # Example environment configuration
├── database/
│   └── whatsapp_messages_teszt.db
├── kerdoivek/              # Questionnaire data
└── public/                 # Frontend pages and static files
```

## How It Works

A typical workflow looks like this:

1. An operator chooses a message type and recipient.
2. The message is sent immediately or stored for scheduled delivery.
3. Incoming WhatsApp events are received through the webhook.
4. The application stores the incoming message and related metadata.
5. If a questionnaire is active, the backend determines the next step from the user's response.
6. The next question or template is sent automatically.
7. The full conversation remains available for later review and analysis.

## Installation

### 1. Requirements

- Node.js
- npm
- A Meta Developer / WhatsApp Business configuration
- A public HTTPS URL for webhook callbacks during integration testing

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Copy the example configuration:

```bash
cp .env.example .env
```

Then configure the required values in `.env`, including:

```env
PORT=3000
PUBLIC_BASE_URL=https://your-public-url.example

VERIFY_TOKEN=your_webhook_verify_token
APP_SECRET=your_meta_app_secret
ACCESS_TOKEN=your_meta_access_token
WHATSAPP_BUSINESS_ACCOUNT_ID=your_business_account_id
PHONE_NUMBER_ID=your_phone_number_id

SESSION_SECRET=your_random_session_secret
ADMIN_SETUP_TOKEN=your_owner_setup_token
```

Additional SMTP, database, scheduling and security options are documented in `.env.example`.

> Never commit real access tokens, passwords, API secrets or production credentials to the repository.

### 4. Start the application

```bash
npm start
```

By default the application is available at:

```text
http://localhost:3000
```

## WhatsApp / Meta Integration

The application uses the Meta Graph API for sending messages and a webhook endpoint for incoming WhatsApp events.

Typical integration steps:

1. Create or configure a Meta Developer application.
2. Add the WhatsApp product.
3. Configure the phone number and WhatsApp Business Account IDs.
4. Set the webhook callback to the application's public `/webhook` endpoint.
5. Use the same verification token in Meta and the local environment configuration.
6. Subscribe to the required WhatsApp webhook events.

For local development, a temporary HTTPS tunnel such as **ngrok** can be used to expose the application to Meta's webhook service.

## Screenshots

Recommended screenshots for the repository:

- Main message-sending interface
- Conversation view
- Questionnaire editor
- Message filtering / analytics view
- Admin or user-management interface

A simple structure can be used:

```text
docs/
└── screenshots/
    ├── messaging.png
    ├── conversations.png
    ├── questionnaire.png
    ├── filters.png
    └── admin.png
```

Then embed them in this README, for example:

```md
![Messaging interface](docs/screenshots/messaging.png)
```

## Data & Logging

SQLite is used to persist application data, including items such as:

- contacts
- incoming messages
- sent messages
- message metadata
- scheduled messages
- users
- audit logs
- consent records

The application also stores session data separately and can keep local copies of sent media for later review.

## Security Notes

The project contains several security-focused mechanisms, including:

- hashed passwords
- role-based authorization
- rate limiting for authentication and account operations
- protected administrative pages
- environment-based secret management
- webhook verification support
- audit logging

For real production deployment, HTTPS, a reverse proxy, strict secret management, regular backups and process supervision are recommended.

## Project Context

WaccApp was developed as a practical full-stack project focused on **API integration, webhook processing, messaging automation, stateful questionnaire workflows, persistence and administration**.

It demonstrates experience with third-party APIs, backend business logic, database-backed workflows, authentication, scheduling and user-facing web interfaces.
