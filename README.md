# AuraLite — AI Content Scorer

**A lightweight, single-file AI Content Quality Scorer. No backend. No API key. No install required.**

Open the file in any browser and instantly get a "Brand Readiness Score" for any text content you paste in.

---

## What It Does

1. You paste any text content (a marketing tagline, a blog post, a product description, a social media caption, etc.) into the input field.
2. You click **"Analyze Content"**.
3. After a 1.5-second simulated analysis, it returns:
    - A **Brand Readiness Score** (0–100).
    - A **status label** (e.g., "Brand Ready").
    - A short **summary** explaining the result.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | HTML5 + Vanilla JavaScript |
| Styling | Inline CSS (no framework) |
| Font | Inter (loaded from Google Fonts CDN) |
| Backend | None |
| API Keys | None required |
| Dependencies | None — single HTML file |

---

## Prerequisites

**None.** You only need a web browser (Chrome, Firefox, Safari, Edge — any modern browser works).

---

## Clone the Repository

```bash
git clone https://github.com/stephen3123/AuraLite.git
cd AuraLite
```

---

## Run the Application

Since AuraLite is a single HTML file with no server or build step, you just open it:

### Option 1: Double-click (Easiest)
Double-click the `index.html` file. It opens directly in your default browser.

### Option 2: From the Terminal
```bash
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

### Option 3: Local Server (Optional, for development)
If you want to run it on a local server (e.g., to avoid CORS issues in future versions):
```bash
# Using Python (comes pre-installed on macOS/Linux)
python3 -m http.server 8000
# Then visit: http://localhost:8000
```

---

## How to Use

1. **Open `index.html`** in your browser.
2. In the **"Paste Content to Analyze"** text area, type or paste any content.
3. Click the **"Analyze Content"** button.
4. Wait ~1.5 seconds while the loading animation plays.
5. The result panel appears showing:
    - A circular **score indicator** (e.g., `87`)
    - A **status** label (e.g., "Brand Ready")
    - A **description** of the analysis

---

## Design Features

- **Glassmorphism card** with `backdrop-filter: blur(20px)` and semi-transparent background
- **Animated background glow** using a radial gradient that slowly pulsates
- **Smooth slide-up animation** when the page loads
- **Loading spinner** that appears while "analyzing"
- **Result fade-in animation** when the score is revealed
- **Focus glow** on the text input when active (indigo ring)
- Dark color scheme: `#030712` background, `#6366F1` (indigo) primary, `#10B981` (emerald) accent

---

## File Structure

```
AuraLite/
└── index.html   # The complete application (HTML + CSS + JS in one file)
```

---

## Extending AuraLite (Future)

The `analyze()` function in the JavaScript currently runs a **simulated** analysis (random score between 70–99 after a 1.5s delay). To connect it to a real AI API:

1. Replace the `setTimeout` block with a `fetch()` call to your API (e.g., OpenAI, Claude, or a custom backend).
2. Pass the `content` variable as the request body.
3. Display the real score and explanation from the API response.

Example (Claude API):
```javascript
async function analyze() {
  const content = document.getElementById('content').value;
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'x-api-key': 'YOUR_KEY',
      'anthropic-version': '2023-06-01',
      'content-type': 'application/json'
    },
    body: JSON.stringify({
      model: 'claude-haiku-4-5',
      max_tokens: 100,
      messages: [{ role: 'user', content: `Score this content 0-100 for brand quality: ${content}` }]
    })
  });
  const data = await response.json();
  // Parse and display the score from data
}
```
