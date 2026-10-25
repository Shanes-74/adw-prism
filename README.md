# adw-prism

> An adw-gtk3-based theme that partners with [matugen](https://github.com/InioX/matugen)
> to bring **Material You dynamic color** to your GTK desktop.

Your wallpaper picks the palette. adw-prism paints the interface.

adw-prism is not a direct fork of adw-gtk3 — it borrows the visual language and
the Adwaita aesthetic from the original project, but is rebuilt around a
different premise: **color comes from matugen, not from a static theme file**.
The result is a GTK theme that repaints itself whenever your wallpaper changes,
following the same principles as Android's Material You.

![screenshot](docs/screenshot.png)

## ✨ Features

- 🎨 **Material You, properly** — uses [matugen](https://github.com/InioX/matugen)
  as the color engine, the same approach Android uses for its dynamic palette
- 🌗 **Light & dark** — matugen generates both schemes; adw-prism applies the
  one that matches your system preference
- 🧩 **GTK3 & GTK4** — covers both toolkits, including libadwaita apps
- 🖥️ **Hyprland-first** — built and tested on Hyprland (Wayland)
- 🔌 **Portal-aware** — plays nicely with `xdg-desktop-portal` so GTK4/libadwaita
  apps receive the color-scheme preference

## 🖼️ How it works

adw-prism doesn't extract colors itself. It delegates that job to **matugen**,
which does Material You color science properly, and then applies the result to
the Adwaita visual language.

1. **matugen** reads your wallpaper and generates a Material You palette
   (primary, surface, on-surface, etc.), in both light and dark variants.
2. matugen outputs those colors into a set of **templates** shipped with
   adw-prism — SCSS files that map Material You tokens to GTK widget states.
3. The SCSS is compiled into `gtk-3.0.css` and `gtk-4.0.css`.
4. The generated CSS is written to `~/.config/gtk-3.0/gtk.css` and
   `~/.config/gtk-4.0/gtk.css`, overriding the base Adwaita styles.
5. `gsettings` and the XDG portal propagate the color-scheme preference
   (`prefer-dark` / `prefer-light`) to GTK4 and libadwaita applications.

In other words: **adw-prism is the theme layer; matugen is the color layer.**
They are designed to work together, not to overlap.

## 📦 Requirements

- [matugen](https://github.com/InioX/matugen) — Material You color generator
- `adw-gtk3` — base theme (the visual foundation)
- `sassc` — SCSS → CSS compilation
- `xdg-desktop-portal`, `xdg-desktop-portal-gtk`, `xdg-desktop-portal-hyprland`
- `gsettings` (part of `glib2`)

On Arch:

```bash
sudo pacman -S xdg-desktop-portal xdg-desktop-portal-gtk xdg-desktop-portal-hyprland glib2
# matugen is in the AUR
yay -S matugen-bin
