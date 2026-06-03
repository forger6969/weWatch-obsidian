---
zone: MCPs
type: reference
updated: 2026-06-03
author: Habibulloh
---

# computer-control-mcp — To'liq Qo'llanma

> **Nima:** Claude'ga kompyuterni boshqarish — sichqoncha, klaviatura, screenshot, OCR, oyna boshqaruvi.
> **Texnologiya:** PyAutoGUI + EasyOCR/Tesseract | Python 3.13 | uvx

## Config (~/.claude/settings.json)

```json
"computer-control-mcp": {
  "type": "stdio",
  "command": "/opt/homebrew/bin/uvx",
  "args": ["--python", "3.13", "computer-control-mcp@latest"],
  "env": {}
}
```

**Status:** ✅ Qo'shildi 2026-06-03 (Habibulloh tomonidan taqdim etildi)

## macOS Ruxsatlari (MAJBURIY)
- System Settings → Privacy & Security → **Accessibility** → Terminal/Claude ✅
- **Screen Recording** → screenshot uchun ✅

---

## 15 ta Tool

### Ekran (Screen)
| Tool | Asosiy parametrlar | Vazifa |
|------|--------------------|--------|
| `take_screenshot` | `title_pattern`, `save_to_downloads` | Ekran rasmi |
| `take_screenshot_with_ocr` | `title_pattern` | Ekran + matn o'qish (~20s sekin) |
| `get_screen_size` | — | Rezolutsiya |
| `list_windows` | — | Ochiq oynalar |

### Sichqoncha (Mouse)
| Tool | Parametrlar | Vazifa |
|------|-------------|--------|
| `click_screen` | `x`, `y` | Bosish |
| `move_mouse` | `x`, `y` | Kursor ko'chirish |
| `drag_mouse` | `from_x`, `from_y`, `to_x`, `to_y`, `duration` | Drag & drop |
| `mouse_down` | `button` (left/right/middle) | Tugma ushlab turish |
| `mouse_up` | `button` | Tugma qo'yib yuborish |

### Klaviatura (Keyboard)
| Tool | Parametrlar | Vazifa |
|------|-------------|--------|
| `type_text` | `text` | Matn yozish |
| `press_keys` | `keys` (str/list/nested list) | Tugma bosish |
| `key_down` | `key` | Tugma ushlab turish |
| `key_up` | `key` | Tugma qo'yib yuborish |

### Oyna (Window)
| Tool | Parametrlar | Vazifa |
|------|-------------|--------|
| `activate_window` | `title_pattern`, `threshold` | Oynani oldinga |

### Yordamchi
| Tool | Parametrlar | Vazifa |
|------|-------------|--------|
| `wait_milliseconds` | `milliseconds` | Kutish |

---

## Tipik Ssenariylar

```
# Matnni topib bosish (eng kuchli)
take_screenshot_with_ocr() → matn+koordinat → click_screen(x, y)

# Forma to'ldirish
activate_window("Brauzer") → click_screen(x,y) → type_text("...") → press_keys("enter")

# Copy-paste (macOS)
press_keys([["cmd","a"]]) → press_keys([["cmd","c"]]) → click → press_keys([["cmd","v"]])
```

## Computer Control vs computer-use MCP farqi

| | computer-control-mcp | computer-use (current) |
|---|---|---|
| **Paket** | `computer-control-mcp` (uvx/Python) | `computer-use-mcp` (npx) |
| **OCR** | ✅ EasyOCR/Tesseract | ❌ |
| **Oyna boshqaruv** | ✅ activate_window | ❌ |
| **Tool soni** | 15 | ~20 |
| **Muallif** | Habibulloh | — |

## Computer Control vs Playwright

| Holat | Ishlat |
|-------|--------|
| Brauzer ichida (sayt) | **Playwright** |
| Desktop dastur (Telegram, VSCode) | **Computer Control** |
| Butun ekran screenshot | **Computer Control** |
| Native oyna boshqaruvi | **Computer Control** |

---

*← [[MCPs/_index|MCPs Index]]*
