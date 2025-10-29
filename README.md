Beautiful LM Studio Client

A single-file, modern web client for LM Studio with a clean, transparent, high‑contrast UI, streaming chat, image assist, autocomplete, and slash commands. Optimized for local use and static hosting (e.g., Vercel, GitHub Pages) with smart localhost connection handling.

Features
- Transparent, futuristic UI: glass‑like look without blur, with refined hover/press feedback and high-contrast text for readability over photos.
- Background-driven assistant name: the assistant label equals your background image file name (e.g., `lol.png` → “lol”).
- Streaming chat: renders partial responses smoothly; code highlight, Markdown, and MathJax supported.
- Image assist: attach or drag-and-drop images; prompts include image context.
- Autocomplete: recent prompt completions and slash-command suggestions with Tab and arrow-key navigation.
- Slash commands: power-user actions right from the input (see list below).
- Smart connect: normalizes input (`1234` → `http://127.0.0.1:1234`) and tries common localhost candidates (`127.0.0.1`/`localhost`, ports 1234/11434).
- Deployment-friendly: safe CORS/mixed-content fetch options and helpful guidance for https pages.

Quick Start
1) Run LM Studio server locally
   - Start the LM Studio HTTP server (ensure it listens on a known port, e.g., 1234).
   - If you’ll open this client over HTTPS (e.g., Vercel), make sure LM Studio allows CORS from your origin. Browsers allow HTTPS pages to call HTTP only for localhost targets.

2) Open the client
   - Option A: Open `index.html` directly in your browser.
   - Option B: Serve statically (e.g., `npx serve .`), or deploy to GitHub Pages/Vercel.

3) Connect
   - Enter your LM Studio URL or just a port (e.g., `1234`) and click Connect.
   - The client will normalize and try: `http://127.0.0.1:1234`, `http://localhost:1234`, etc.
   - Pick a model once connected; start chatting.

Slash Commands
- `/help` — List available commands
- `/clear` — Clear current chat messages
- `/clearall` — Delete all chats (confirm)
- `/rename New Name` (alias: `/title`) — Rename current chat
- `/bg pick` — Select a background image
- `/bg clear` — Remove background image
- `/dim 0.25` — Set background dim (0–0.8)
- `/export` — Download chats JSON
- `/import` — Import chats JSON
- `/model llama` — Switch to a model by substring
- `/connect` — Toggle connect
- `/disconnect` — Toggle disconnect
- `/eject` — Unload current model

Autocomplete & Keyboard
- Start with `/` to see command suggestions.
- Type normally for writing assistance: the last word autocompletes from recent user prompts.
- Keys: ArrowUp/Down to navigate suggestions; Tab to accept; Enter to run a slash command.

Background & Personalization
- Background image: click the image button in the header to pick an image. The assistant name auto-uses the image base name.
- Long-press the background button to:
  - Type `pick` to choose an image
  - Type `clear` to remove it
  - Type a number (e.g., `0.25`) to set dimming

Deployment Notes (Vercel / HTTPS)
- This client makes requests directly to your LM Studio server.
- If the page is HTTPS (e.g., Vercel), browsers block HTTP requests to non-local targets. You can:
  - Use localhost targets: `http://127.0.0.1:1234` (allowed from HTTPS pages)
  - Or expose LM Studio via HTTPS with CORS enabled (e.g., a tunnel like ngrok/Cloudflare Tunnel)
- The client sets safe fetch options (`mode: cors`, no credentials, `no-store`, no referrer) to minimize CORS friction. Your server must still send the appropriate `Access-Control-Allow-Origin` header.

Tech Stack
- Single-file app: `index.html`
  - Marked (Markdown), highlight.js (code), MathJax (LaTeX), Font Awesome, Inter font via CDN
  - No build step required

Project Structure
- `index.html` — UI, styles, and all client logic
- `LICENSE` — MIT License

Customization Tips
- Theme tokens are in CSS (`:root` variables) for colors, radii, shadows, and transitions.
- Effects (hover/press) and contrast can be tuned by adjusting the “Futuristic UI Enhancements”, “Transparent UI”, and “High Contrast Text” sections in the `<style>` block.

FAQ
Q: The app won’t connect from my deployed site.
A: If your deployed page uses HTTPS, only HTTP localhost targets are allowed by browsers. Otherwise host your API on HTTPS and enable CORS. The client will warn when the target is not allowed.

Q: Streaming fails with CORS errors.
A: Ensure your LM Studio server returns `Access-Control-Allow-Origin` for your site. Consider a simple HTTPS tunnel or a proxy if needed.

Q: Can I use images?
A: Yes. Attach via the paperclip button or drag-and-drop. The app will include the image context and label your chat accordingly.

License
This project is licensed under the MIT License — see `LICENSE`.
