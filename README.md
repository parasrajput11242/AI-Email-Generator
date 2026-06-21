# AI Email Generator – Chrome Extension

An AI-powered Chrome extension that generates smart email replies directly inside Gmail. Built with a Spring Boot backend and Google's Gemini API, it lets you draft professional, casual, or friendly responses in one click — no more staring at a blank reply box.

## Features

- **One-click AI replies** generated directly inside the Gmail compose window
- **Tone selection** — choose between Professional, Casual, or Friendly before generating
- **Spring Boot backend** that securely handles requests to the Gemini API
- **Lightweight Chrome Extension** built with the Chrome Extension API, injecting seamlessly into Gmail's UI

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Spring Boot (Java) |
| AI Model | Google Gemini API |
| Frontend / Extension | Chrome Extension API (JavaScript, HTML, CSS) |
| Integration | Gmail Web UI (DOM injection) |

## How It Works

1. The Chrome extension injects a **"Generate Reply"** button into Gmail's compose/reply toolbar.
2. When clicked, it reads the relevant email thread content and sends it to the Spring Boot backend.
3. The backend forwards the content to the **Gemini API**, along with the selected tone.
4. Gemini generates a reply, which the backend returns to the extension.
5. The extension inserts the generated reply directly into the Gmail compose box for you to review, edit, and send.

## Project Structure

```
AI-Email-Generator/
├── email-writer-sb/        # Spring Boot backend
│   ├── src/
│   ├── pom.xml
│   └── mvnw / mvnw.cmd
└── extension/               # Chrome extension (frontend)
    ├── manifest.json
    ├── content.js
    └── popup/ (if applicable)
```

> Update the structure above to match your actual folder names if they differ.

## Prerequisites

Before you begin, make sure you have:

- **Java 17+** and **Maven** (or use the included `mvnw` wrapper)
- **Google Chrome** browser
- A **Gemini API key** ([get one here](https://ai.google.dev/))

## Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/parasrajput11242/AI-Email-Generator.git
cd AI-Email-Generator
```

### 2. Backend Setup (Spring Boot)

```bash
cd email-writer-sb
```

Add your Gemini API key to `src/main/resources/application.properties`:

```properties
gemini.api.key=YOUR_GEMINI_API_KEY
gemini.api.url=https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent
```

Run the backend:

```bash
./mvnw spring-boot:run
```

By default, the backend will start on `http://localhost:8080`.

### 3. Chrome Extension Setup

1. Open Chrome and go to `chrome://extensions/`
2. Enable **Developer mode** (toggle, top-right corner)
3. Click **Load unpacked**
4. Select the `extension/` folder from this project
5. The extension icon should now appear in your Chrome toolbar

### 4. Using the Extension

1. Open **Gmail** in Chrome
2. Open any email and click **Reply**
3. You'll see a new **"AI Reply"** button (or similar) added near the send button
4. Select your preferred tone — **Professional**, **Casual**, or **Friendly**
5. Click **Generate** — the AI-written reply will populate the compose box
6. Review, edit if needed, and hit **Send**

## Configuration Notes

- Make sure the Spring Boot backend is **running locally** before using the extension, since the extension calls it for every generation request.
- If you deploy the backend elsewhere (e.g., a cloud server), update the API endpoint URL inside the extension's JavaScript (likely in `content.js` or a config file) to point to your deployed backend instead of `localhost:8080`.

## Troubleshooting

| Issue | Likely Cause |
|---|---|
| Extension button doesn't appear in Gmail | Gmail's DOM structure may have changed, or extension wasn't reloaded after install — try refreshing Gmail |
| "Failed to generate reply" error | Backend isn't running, or Gemini API key is missing/invalid |
| CORS errors in console | Backend CORS config doesn't allow requests from the Chrome extension origin |

## Future Improvements

- [ ] Support for additional tones (e.g., formal, persuasive)
- [ ] Multi-language reply generation
- [ ] Deploy backend to a cloud provider for public use
- [ ] Add unit tests for backend endpoints

## License

This project is open source. Feel free to use, modify, and distribute it.

## Author

**Paras Rajput**
GitHub: [@parasrajput11242](https://github.com/parasrajput11242)
