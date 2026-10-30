# Enhanced Online Graphing Calculator

A standalone, 100% client-side graphing calculator web interface with desktop-friendly keyboard shortcuts, single-character `Backspace`, hardware-level `Ctrl+Z` Undo / `Ctrl+Y` Redo, and a 20% larger native display.

---

## 🔒 Bring Your Own ROM (Zero Proprietary Firmware Included)

To ensure full copyright compliance:
- **No proprietary ROMs, operating system binaries, or firmware files are distributed or hosted in this repository.**
- When you open the web application, supply your own calculator OS state or ROM dump (`.h84statej`, `.h84state`, or `.rom`).
- **Persistent Local Storage (IndexedDB):** The web app saves your ROM file directly into your browser's private local database (`IndexedDB`). It is never uploaded to any remote server and loads automatically on all subsequent visits—**you only need to provide the file once**. You can change or reload a ROM at any time via the **📁 Load ROM** button in the toolbar.
- For local development, if an OS state file is placed inside the `assets/` directory on your workstation, the local server detects it and boots immediately without prompting.

---

## Key Features & Enhancements

1. **Direct Curly Brace (`{` / `}`) & Bracket (`[` / `]`) Keyboard Input**
   - Typing `{` or `}` on your physical keyboard automatically dispatches the `2nd` + `(` or `2nd` + `)` hardware sequence synchronously to the calculator CPU, allowing rapid list entry (`L1`, `L2`).
   - Supports `[` (`2nd` + `*`) and `]` (`2nd` + `-`) for matrix operations and indexing.

2. **Single-Character `Backspace` (Instead of Clearing the Entire Line)**
   - Standard calculator implementations map `Backspace` to the `CLEAR` key, erasing the entire equation whenever you try to correct a typo.
   - This calculator dynamically inspects the OS edit buffer pointers in RAM (`editTop` at `0xD02437` and `editCursor` at `0xD0243A`) and issues `Left Arrow` + `DEL` when typing inside an active line—deleting **only the last character**.
   - Full line clearing is assigned to `Esc`.

3. **Hardware-Level Undo (`Ctrl+Z`) & Redo (`Ctrl+Y` / `Ctrl+Shift+Z`)**
   - 50-step undo/redo stack (`undoStack` / `redoStack`) with toolbar buttons (**↶ Undo**, **↷ Redo**).
   - Captures sub-millisecond snapshots of CPU registers, ASIC hardware states, and the RAM buffer before every keypress.
   - Accidentally cleared a 30-digit formula or statistical table? Press `Ctrl+Z` to bring it back instantly.

4. **Cleaner UI & 20% Larger Native Pixel Size (`100%`)**
   - Stripped away all outer wrapper frames, advertisements, and descriptive filler text.
   - Sized the unscaled base display to **`309.6px × 724.8px`** (20% larger in native pixels than legacy calculator web layouts) for crisp vector rendering and desktop readability.

---

## Keyboard Shortcuts

| Shortcut | Action |
| :--- | :--- |
| `{` / `}` | Insert curly braces (`2nd` + `(` / `2nd` + `)`) for lists |
| `[` / `]` | Insert square brackets (`2nd` + `*` / `2nd` + `-`) |
| `Backspace` | Delete only the last character (`Left Arrow` + `DEL`) |
| `Ctrl+Z` / `Cmd+Z` | Undo last action (restores deleted line) |
| `Ctrl+Y` / `Ctrl+Shift+Z` | Redo action |
| `Esc` | Clear current line (`CLEAR`) |
| `Enter` | Execute / `ENTER` |
| `0`–`9`, `+`, `-`, `*`, `/`, `^`, `(`, `)`, `,`, `.` | Standard numbers and mathematical operators |
| Arrow Keys | Directional navigation for menus, lists, and graphs |

---

## Live Demo

- **Live Site**: [https://graphing-calculator-h5xs.onrender.com](https://graphing-calculator-h5xs.onrender.com)

---

## Running Locally

```bash
git clone https://github.com/iaminov/graphing-calculator.git
cd graphing-calculator
python -m http.server 8000
```

Open **`http://localhost:8000`** in your browser.
