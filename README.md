pro calc
readme = """# Scientific Calculator

A sleek, modern scientific calculator built with pure HTML, CSS, and JavaScript. No frameworks, no dependencies — just open and use!

![Calculator Preview](https://img.shields.io/badge/Calculator-Scientific-blue?style=for-the-badge)
![Made With](https://img.shields.io/badge/Made%20With-HTML%20%7C%20CSS%20%7C%20JS-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Basic Operations** | Addition, Subtraction, Multiplication, Division |
| **Scientific Functions** | sin, cos, tan, log, ln, √, power (xʸ), π, e |
| **Keyboard Support** | Use number keys, Enter, Backspace, Escape |
| **History Log** | Click any previous calculation to reuse it |
| **Responsive Design** | Works perfectly on mobile & desktop |
| **Dark Theme** | Easy on the eyes |

## 🚀 Live Demo

**[Click here to try it live!](https://your-username.github.io/scientific-calculator/)**

*(Replace `your-username` with your actual GitHub username after deploying)*

## 📸 Screenshot

```
┌─────────────────────────────┐
│  sin(45)                    │  ← Expression
│  0.7071...                  │  ← Result
├─────────────────────────────┤
│  AC  (   )   ÷              │
│  sin cos tan  ×             │
│  7   8   9   −              │
│  4   5   6   +              │
│  1   2   3   √              │
│  0   .   xʸ  =              │
│  ln  log  π   e              │
└─────────────────────────────┘
```

## 🎯 How to Use

### Online (No Download Needed)
Simply visit the live demo link above!

### Local Use
1. Download `calculator.html`
2. Double-click to open in any browser
3. Start calculating!

### Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `0-9` | Enter numbers |
| `+ - * /` | Operators |
| `Enter` | Calculate result |
| `Backspace` | Delete last character |
| `Escape` or `C` | Clear all |

## 🛠️ Technologies Used

- **HTML5** — Structure
- **CSS3 Grid** — Button layout & responsive design
- **Vanilla JavaScript** — All logic (no libraries!)

## 📁 File Structure

```
scientific-calculator/
├── calculator.html    ← Main file (everything in one!)
└── README.md          ← This file
```

## 🚀 Deploy on GitHub Pages

1. Fork or upload this repository to your GitHub
2. Go to **Settings** → **Pages**
3. Set Source to `main` branch
4. Your calculator will be live at:
   ```
   https://your-username.github.io/scientific-calculator/
   ```

## 🤝 Contributing

Found a bug or want to add a feature? Feel free to open an issue or pull request!

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

**Made with ❤️ for easy math!**
"""

with open('/mnt/agents/output/README.md', 'w', encoding='utf-8') as f:
    f.write(readme)

print("README.md saved successfully!")
