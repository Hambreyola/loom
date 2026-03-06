# Loom

## Overview

**Loom** is a minimal, modern Wayland compositor designed to power the **Onyx desktop environment**.

The name reflects the compositor’s role: *weaving application surfaces together into a single screen.*

Loom focuses on:

- simplicity
- modern graphics
- minimal configuration
- sensible defaults
- a clean user experience

It intentionally avoids feature bloat while still providing a polished desktop foundation.

Loom is developed as an **independent project** that can be used outside of Onyx if desired.

The broader desktop stack will look like:


Onyx
├─ loom (compositor)
├─ panel (desktop panel)
├─ launcher (application launcher)
└─ settings (optional configuration UI)


---

# Core Design Philosophy

Loom aims to balance **minimalism with modern usability**.

Guiding principles:

- minimal code complexity
- clean default appearance
- no tiling paradigms
- floating window workflow
- subtle visual polish
- low configuration requirements
- standards-compliant Wayland protocols

The goal is a compositor that feels **clean, modern, and lightweight** without being overly barebones.

---

# Window Management Model

Loom uses a **floating-only window model**.

There is:

- no tiling
- no hybrid layouts
- no dynamic tiling modes

Windows can be freely moved and resized.

### Window Interaction

- **Border drag** → resize  
- **Mouse drag on titlebar** → move  
- **Focus follows mouse**

This model keeps the compositor simple while maintaining a flexible desktop experience.

---

# Window Decorations

Loom implements **server-side window decorations**.

This means Loom itself draws window frames.

Decorations include:

- minimal titlebar
- close button
- maximize button
- minimize button

### Design Goals

- extremely minimal visual footprint
- subtle rounded corners
- modern appearance
- consistent styling across all applications

Applications that provide their own decorations may still use them.

---

# Rendering Architecture

Loom is built using:

- **Rust**
- **Smithay**

Rendering uses **OpenGL / GLES**.

### Reasons

- mature ecosystem
- stable support in Smithay
- lower development complexity
- portable across hardware

Future **Vulkan** support may be explored but is not required for the initial compositor.

---

# Visual Style

The visual design is **modern minimal**.

Features include:

- wallpaper background
- subtle open/close window animations
- very light corner rounding
- minimal shadows
- optional transparency

Heavy effects such as **blur** are intentionally avoided unless they align with the minimal philosophy.

---

# Workspaces

Loom provides **fixed workspaces**.

Default layout:


1 2 3 4 5 6 7 8 9


### Characteristics

- windows belong strictly to one workspace
- switching workspace hides windows from others
- keyboard navigation is primary

---

# Input Model

Primary modifier key:


Super


### Example Shortcuts


Super + 1-9 switch workspace
Super + Q close window
Super + Space open launcher
Super + Enter open terminal


### Focus Model


focus follows mouse


---

# Protocol Support

Minimum supported Wayland protocols include:

- `xdg-shell`
- `xdg-decoration`
- `wl-seat`
- `layer-shell`

Support for **layer-shell** allows panels and overlays to function properly.

This ensures compatibility with components like desktop panels.

---

# Configuration

Loom uses a **minimal configuration file**.

Location:


~/.config/onyx/config.toml


### Goals

- minimal configuration surface
- sensible defaults
- no recompilation required
- human readable format

---

# Interprocess Communication (IPC)

Loom exposes a **Unix socket IPC interface**.

Example path:


/run/user/<uid>/onyx.sock


External programs can interact with Loom through commands such as:


open launcher
switch workspace
reload configuration


This allows tools like panels and launchers to communicate with the compositor.

---

# Development Mode

Loom supports **nested execution**.

This allows the compositor to run inside an existing Wayland session for development.

Example usage:


cargo run


A Loom window will open inside the current desktop, running its own Wayland session.

This avoids requiring TTY switching during development.

---

# Future Onyx Components

Planned companion tools include:


panel desktop panel
launcher application launcher
settings configuration interface


Existing minimal launchers such as:

- wofi
- rofi

may be used temporarily during early development.
