## WhyAI Notes 

A local-first, AI-powered note-taking application and Evernote (.enex) explorer built entirely in a single HTML file.

WhyAI Notes allows you to import your Evernote backups, organize your thoughts, and interact with your personal knowledge base using Google's Gemini AI, all while keeping your data strictly local and secure.

<img width="925" height="512" alt="Why AI Notes screenshot" src="https://github.com/user-attachments/assets/d066e7e7-d7c4-4766-b7e0-664c76ba991e" />


### Features

- Local-First Architecture: Your notes, images, PDFs, and chat histories are stored entirely offline in your browser's IndexedDB. No backend servers, no cloud databases, zero latency.

- Evernote (.enex) Import: Seamlessly import your Evernote exports. WhyAI Notes parses titles, HTML content, dates, and base64-encoded attachments (images and PDFs) locally.

- AI Assistant (Gemini 2.5 Flash): Chat directly with your documents. The app intelligently injects the active note's text, images, and PDFs into the AI context, allowing you to ask questions, summarize, and analyze your data.

- Secure Web Crypto Backups: Export your entire database (or specific notebooks) as a .enc file using robust AES-GCM 256-bit encryption. Restore your data on any device with your secure password.

- Note Creation & Organization: Create new notes, organize them into a collapsible Notebook hierarchy, and attach files or capture photos directly from your device's native camera.

- Fully Responsive UI: A modern, Tailwind-powered interface that works beautifully on desktop, tablet, and mobile devices.

### Getting Started

Because WhyAI Notes is a zero-dependency, single-file web application, setup is instant.

You can use the App directly from your browser and all state is stored on your loccal browser - nothing server-side: https://jimliddle.github.io/WhyAInotes/

Download: Clone this repository or simply download the index.html file.

Open: Double-click index.html to open it in any modern web browser.

Connect AI: * Get a free API key from Google AI Studio.

Click the Settings (gear icon) in the app and paste your API key. (Note: Your key is saved locally in your browser's localStorage and only ever communicates directly with Google's API endpoints).

Import Data: Click the Import .enex button to load your Evernote backups, or click New Note to start from scratch.

### Technology Stack

Frontend: HTML5, Vanilla JavaScript (ES6+)

Styling: Tailwind CSS (via CDN)

Icons: Lucide Icons

Storage: IndexedDB (Native browser storage)

Cryptography: Native Web Crypto API (crypto.subtle)

AI Integration: Google Generative AI REST API (gemini-2.5-flash)

### How the AI Context Works

To preserve API tokens and optimize response times, WhyAI Notes uses a smart context-injection strategy:

When you ask your first question about a note, the app automatically bundles the note's parsed HTML text, alongside any supported attachments (Images and PDFs).

This bundle is injected behind the scenes into the first user message payload sent to the Gemini API.

Subsequent messages in the same chat thread rely on the AI's conversation history, ensuring rapid back-and-forth interactions without re-uploading the same attachments.

### Security & Privacy

Zero Tracking: There is no tracking, analytics, or telemetry.

Data Ownership: You own your data. Unless you query the AI assistant, your data never leaves your device.

Encrypted Backups: The "Secure Backup" feature uses PBKDF2 for key derivation (100,000 iterations) and AES-GCM for encryption, ensuring your exported data is safe at rest.

Encryption Password: When you enable the "Local App Lock" in the Settings, the app generates a master key (using PBKDF2 and a secure salt) and encrypts every single note, image, and chat history stored inside the  browser's IndexedDB using AES-GCM. When you close the tab, the key is destroyed from memory. The next time you open the app, it will display a Lock Screen. Until the correct password is provided, Data remains completely unreadable cipher-text—even if someone physically opens the  browser's Developer Tools to inspect the database.

### Scale

Whereas technically there are no restraints other than disk space in how large IndexedDB can grow, practically this is good for a few thousand notes ie. not tens or hundreds of thousands of notes

### License

This project is open-source and available under the MIT License.
