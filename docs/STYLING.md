# Orbit Styling & Theming Guide

Orbit is highly customizable, allowing you to tweak layouts, animations, colors, and raw CSS. Configuration is split into three main files located in your configuration directory (usually `~/.config/orbit/`).

## 1. Core Configuration (`config.toml`)
This file controls the structural behavior of the application, including positioning and animations.

```toml
# Window position on screen (e.g. top-right, bottom-center)
position = "top-right"

# Margins (in pixels) from screen edges
margin_top = 10
margin_bottom = 10
margin_left = 10
margin_right = 10

# Main window spawn animation
# Options: slidedown, slideup, slideleft, slideright, swingdown, swingup, swingleft, swingright, fade, crossfade, none
window_transition = "slidedown"
window_transition_duration = 200

# Tab switching animation
# Options: slidehorizontal, slidevertical, slidedown, slideup, slideleft, slideright, crossfade, none
stack_transition = "slidehorizontal"
stack_transition_duration = 200
```

## 2. Color Theme (`theme.toml`)
This file defines the primary color palette. Orbit uses these variables to automatically generate gradients, backgrounds, and accents for GTK4.

```toml
accent_primary = "#8b5cf6"
accent_secondary = "#06b6d4"
background = "#1e1e2e"
foreground = "#d4d4d8"
destructive = "#ef4444"
opacity = 0.91
```
*Note: Orbit supports hot-reloading. Saving changes to `theme.toml` updates the UI instantly.*

## 3. Advanced Custom CSS (`style.css`)
For advanced users who want to write their own GTK4 CSS, you can create a `style.css` file. Orbit loads this file last, allowing you to override any default styling.

> **Warning:** GTK4 CSS is not identical to Web CSS. Some properties like `pointer-events` are not supported. Use standard GTK4 properties and focus on colors, borders, shadows, and margins.

### CSS Class Reference

Orbit exposes semantic CSS classes for almost every UI element. Use these classes in your `style.css` to target specific components.

#### Layout & Containers
- `.background` - The root window background layer.
- `.orbit-panel` - The main content container card.
- `.orbit-scrolled` - Scrollable areas (lists of networks or devices).
- `.orbit-list` - The main container for vertical lists.
- `.orbit-footer` - Sticky footers (e.g., saved networks button container).
- `.orbit-section-header` - Title labels separating sections (e.g., "Saved Networks", "Paired Devices").

#### Interactive Elements
- `.orbit-button` - Base class for all interactive buttons.
- `.primary` - Modifier for primary action buttons (uses accent colors).
- `.flat` - Modifier for flat/ghost buttons.
- `.orbit-toggle-switch` - The main power switch (e.g., WiFi on/off).
- `.orbit-search-container` & `.orbit-search-entry` - The search bar at the top of the network list.

#### Network & Device Rows
- `.orbit-network-row` - Individual WiFi/Ethernet list items.
- `.orbit-device-row` - Individual Bluetooth list items.
- `.focused` - State class applied dynamically when a row is selected or hovered.

#### Text & Indicators
- `.orbit-ssid` / `.orbit-device-name` - The main text label for the connection/device.
- `.orbit-status` - Subtext labels (e.g., "Connected", "Saved").
- `.orbit-status-accent` - Highlighted status labels.
- `.orbit-icon-container` - The wrapper around signal and device icons.
- `.orbit-signal-icon` - Specific targeting for WiFi signal icons.
- `.orbit-device-icon` - Specific targeting for Bluetooth device icons.
- `.orbit-icon-accent` - Modifies icons to use the primary accent color.
- `.orbit-battery-mini` - Bluetooth battery indicators (also has `.low` for low battery states).
- `.orbit-working-indicator` - Loading spinners.

#### Signal Bars (WiFi Strength)
- `.orbit-signal-bars-pad` - Container for custom signal strength bars.
- `.orbit-signal-bar-active` - Filled signal bar.
- `.orbit-signal-bar-active-accent` - Filled signal bar when connected.
- `.orbit-signal-bar-inactive` - Empty signal bar.

#### Miscellaneous
- `.orbit-placeholder` - Placeholder text when lists are empty.

### Example `style.css`

```css
/* Make all buttons pill-shaped */
.orbit-button {
    border-radius: 99px;
}

/* Add a custom glow to the focused network row */
.orbit-network-row.focused {
    background-color: rgba(139, 92, 246, 0.2);
    border: 1px solid #8b5cf6;
}

/* Change the empty state placeholder text color */
.orbit-placeholder {
    color: #a1a1aa;
    font-style: italic;
}
```
