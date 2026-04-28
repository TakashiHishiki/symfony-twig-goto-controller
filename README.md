# Symfony: Twig ↔ Controller

A VS Code extension for Symfony developers that lets you jump instantly between Twig templates and their PHP Controllers — **in both directions**.

---

## Features

### Twig → Controller

Open the Controller that renders the currently active Twig template.

**How to use:**

- Right-click inside a `.twig` or `.html` file → **"Symfony: Open Controller for this Twig"**
- Or click the icon in the editor title bar while a Twig file is active

The extension searches in two ways:

1. **`render()` scan** — scans all PHP files under `src/Controller` for `render('your/template.html.twig')` calls and jumps to the exact line.
2. **Naming convention** — derives candidates from the template path (e.g. `templates/foo/bar.html.twig` → `FooController.php`, `Foo/BarController.php`).

When multiple matches are found, a Quick Pick list lets you choose.

---

### Controller → Twig

Open the Twig template(s) rendered by the currently active Controller.

**How to use:**

- Right-click inside a `.php` file → **"Symfony: Open Twig for this Controller"**
- Or click the icon in the editor title bar while a PHP file is active

The extension resolves templates in priority order:

1. **`render()` calls** — reads the open Controller and lists every `.twig` path found in `render()` calls, with the source line number.
2. **Naming convention** — derives candidates from the Controller filename (e.g. `Admin/DashboardController.php` → `templates/admin/dashboard/index.html.twig`).
3. **Fuzzy name match** — if nothing else is found, scans all Twig files for a base-name match.

---

### Open from selected text

Both directions also work from a selected or cursor-hovered template path string.

**In a Twig / HTML file:**  
Select `'admin/dashboard.html.twig'` → right-click → **"Symfony: Open Controller from template path"**

**In a PHP file:**  
Select or hover over `'admin/dashboard.html.twig'` → right-click → **"Symfony: Open Twig from template path"**

If no text is selected, the extension automatically extracts the nearest quoted `.twig` path on the current line.

---

## Context Menu (Right-Click)

| Active file | Menu item | Action |
|---|---|---|
| `.twig` / `.html` | Symfony: Open Controller for this Twig | Jump to Controller |
| `.twig` / `.html` + selection | Symfony: Open Controller from template path | Jump to Controller at `render()` line |
| `.php` | Symfony: Open Twig for this Controller | Jump to Twig template |
| `.php` + selection | Symfony: Open Twig from template path | Open the selected template |

---

## Configuration

Open **Settings** (`Ctrl+,`) and search for `symfonyTwig`.

| Setting | Default | Description |
|---|---|---|
| `symfonyTwig.templatesDir` | `templates` | Root directory for Twig templates, relative to the project root. |
| `symfonyTwig.controllerDir` | `src/Controller` | Root directory for Controllers, relative to the project root. |
| `symfonyTwig.searchInPhp` | `true` | When enabled, scans PHP files for `render()` calls in addition to naming-convention lookups. |

---

## Installation

### From VS Code Marketplace

Search for **"Symfony: Twig ↔ Controller"** in the Extensions panel, or install via Quick Open:

```
Ctrl+P → ext install colscenery.symfony-twig-goto-controller
```

### From VSIX file

```bash
code --install-extension symfony-twig-goto-controller.vsix
```

Or open VSCode → `Cmd+Shift+P` → `Extensions: Install from VSIX...`

---

## Requirements

- VS Code `^1.80.0`
- A standard Symfony project layout (`templates/` and `src/Controller/`)

---

## License

MIT
