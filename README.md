# 🌸 clocktodo

A cute, minimal **Analog Clock Todo List** — a single-file HTML app where your tasks live on the clock face as colored pizza slices, so you always know what's happening and when.

![clocktodo light mode](imgs\dark-mode.png)
![clocktodo dark mode](imgs\light-mode.png)


---

## ✦ Preview

| Light Mode | Dark Mode |
|:----------:|:---------:|
| Clean white background with pastel task slices on the clock | Soft dark surface with the same colorful slices |

> Tasks appear as **filled pizza-slice sectors** on the analog clock face. The arc covers the exact time block — start to end — with the task name printed inside the slice.

---

## ✦ Features

### 🕐 Analog Clock
- Live SVG analog clock with real-time hour, minute, and second hands
- Second hand in soft pink, center dot accent
- 12-hour clock face with minute ticks and numerals
- Digital time display above the clock

### 🍕 Clock Visualization
- Each task renders as a **filled colored sector** (pizza slice) on the clock ring
- Slice arc length corresponds to the task duration
- Task name is printed inside the slice, rotated to follow the arc
- The **upcoming task** (starting within 15 minutes) pulses with a dashed ring animation

### 📝 Task Management
- Add tasks with: name, category, priority, start time, duration, and an optional note
- Duration is fully flexible — type hours and minutes manually, or use quick-pick buttons (15m, 30m, 1h, 2h, 4h, 8h)
- Tasks sorted by scheduled time automatically
- Mark tasks as **done** (checkbox → strikethrough + fade)
- Delete individual tasks
- **Clear all** via a custom confirm modal (no browser dialogs)
- All tasks saved to **localStorage** — persist across page refreshes

### 🏷 Categories
Five color-coded categories, each with a distinct pastel color:

| Category | Color |
|----------|-------|
| Work | Blue `#7BAFD4` |
| Study | Purple `#B09FE8` |
| Personal | Teal `#6BBFAA` |
| Health | Pink `#F4A7BB` |
| Other | Amber `#F0C070` |

### 🔍 Filtering
Filter the task list by category with one click. The clock always shows all active tasks regardless of filter.

### 🌙 Dark Mode
Toggle between light and dark mode with the button in the top-right corner. All surfaces, borders, badge colors, and the clock face switch cleanly.

---

## ✦ Validation Rules

| Rule | Behavior |
|------|----------|
| Empty task name | Blocked with toast error |
| Name over 50 characters | Blocked (live character counter shown) |
| No start time selected | Blocked with toast error |
| No duration set | Blocked with toast error |
| Duration over 24 hours | Blocked with toast error |
| Task end time already passed | Blocked — task is fully over |
| Task is **ongoing** (started in past, ends in future) | ✅ **Allowed** |
| Duplicate start time | Blocked — another task starts at that exact minute |
| Overlapping time blocks | Blocked — new task can't overlap an existing one |
| More than 12 active tasks | Blocked — max capacity reached |

> Scheduling in the past is allowed **as long as the task is still ongoing** — useful for logging tasks you started earlier in the day.

---

## ✦ Getting Started

No install, no build step, no dependencies.

1. Download `clock-todo.html`
2. Open it in any modern browser
3. Start adding tasks

```bash
# Or clone this repo
git clone https://github.com/your-username/clocktodo.git
cd clocktodo
open clock-todo.html
```

---

## ✦ Tech Stack

| Layer | Detail |
|-------|--------|
| Markup | HTML5 |
| Styling | CSS3 — custom properties, grid, transitions |
| Logic | Vanilla JavaScript (ES6+) |
| Clock | Inline SVG, drawn and updated every second |
| Persistence | `localStorage` |
| Fonts | [Nunito](https://fonts.google.com/specimen/Nunito) + [Space Mono](https://fonts.google.com/specimen/Space+Mono) via Google Fonts |
| Dependencies | **None** |

Everything lives in a single `.html` file — no framework, no bundler, no server needed.

---

## ✦ File Structure

```
clocktodo/
│
└── imgs                # folder for images
└── clock-todo.html     # The entire app — styles, markup, and logic in one file
└── README.md           # This file
```

---

## ✦ How the Clock Visualization Works

The clock face is a 12-hour display. Each task's start and end time is converted to an angle on the clock:

```
angle = (minutes_since_midnight % 720) / 720 × 360°
```

The task is drawn as a filled donut sector (pizza slice) between the start angle and end angle, using an SVG `<path>` with arc commands. The task name is placed at the midpoint of the arc and rotated to follow the curve.

The inner donut hole keeps the clock hands and numerals readable at the center.

---

## ✦ Customization

All colors are defined as CSS custom properties at the top of the file. You can restyle the entire app by editing the `:root` and `[data-theme]` blocks:

```css
:root {
  --purple: #B09FE8;   /* primary accent (buttons, checkboxes) */
  --pink:   #F4A7BB;   /* Health category + second hand */
  --teal:   #6BBFAA;   /* Personal category */
  /* ... */
}
```

To add a new category, add an entry to the `CAT` object in the JavaScript and a corresponding `<option>` in the category `<select>`.

---

## ✦ Browser Support

Works in all modern browsers: Chrome, Firefox, Safari, Edge. No polyfills required.

---

## ✦ License

MIT — free to use, modify, and share.

---

<p align="center">Made with 🌸 as a thesis group project</p>