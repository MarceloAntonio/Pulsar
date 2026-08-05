# Pulsar Styling & Theming Guide

Pulsar is highly customizable, allowing you to tweak layouts, animations, colors, and raw CSS. Configuration is split into three main files located in your configuration directory (usually `~/.config/pulsar/`).

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
This file defines the primary color palette. Pulsar uses these variables to automatically generate gradients, backgrounds, and accents for GTK4.

```toml
accent_primary = "#8b5cf6"
accent_secondary = "#06b6d4"
background = "#1e1e2e"
foreground = "#d4d4d8"
destructive = "#ef4444"
opacity = 0.91
```
*Note: Pulsar supports hot-reloading. Saving changes to `theme.toml` updates the UI instantly.*

## 3. Advanced Custom CSS (`style.css`)
For advanced users who want to write their own GTK4 CSS, you can create a `style.css` file. Pulsar loads this file last, allowing you to override any default styling.

> **Warning:** GTK4 CSS is not identical to Web CSS. Some properties like `pointer-events` are not supported. Use standard GTK4 properties and focus on colors, borders, shadows, and margins.

### CSS Class Reference

Pulsar exposes semantic CSS classes for almost every UI element. Use these classes in your `style.css` to target specific components.

#### Layout & Containers
- `.background` - The root window background layer.
- `.pulsar-panel` - The main content container card.
- `.pulsar-scrolled` - Scrollable areas (lists of networks or devices).
- `.pulsar-list` - The main container for vertical lists.
- `.pulsar-footer` - Sticky footers (e.g., saved networks button container).
- `.pulsar-section-header` - Title labels separating sections (e.g., "Saved Networks", "Paired Devices").

#### Interactive Elements
- `.pulsar-button` - Base class for all interactive buttons.
- `.primary` - Modifier for primary action buttons (uses accent colors).
- `.flat` - Modifier for flat/ghost buttons.
- `.pulsar-toggle-switch` - The main power switch (e.g., WiFi on/off).
- `.pulsar-search-container` & `.pulsar-search-entry` - The search bar at the top of the network list.

#### Network & Device Rows
- `.pulsar-network-row` - Individual WiFi/Ethernet list items.
- `.pulsar-device-row` - Individual Bluetooth list items.
- `.focused` - State class applied dynamically when a row is selected or hovered.

#### Text & Indicators
- `.pulsar-ssid` / `.pulsar-device-name` - The main text label for the connection/device.
- `.pulsar-status` - Subtext labels (e.g., "Connected", "Saved").
- `.pulsar-status-accent` - Highlighted status labels.
- `.pulsar-icon-container` - The wrapper around signal and device icons.
- `.pulsar-signal-icon` - Specific targeting for WiFi signal icons.
- `.pulsar-device-icon` - Specific targeting for Bluetooth device icons.
- `.pulsar-icon-accent` - Modifies icons to use the primary accent color.
- `.pulsar-battery-mini` - Bluetooth battery indicators (also has `.low` for low battery states).
- `.pulsar-working-indicator` - Loading spinners.

#### Signal Bars (WiFi Strength)
- `.pulsar-signal-bars-pad` - Container for custom signal strength bars.
- `.pulsar-signal-bar-active` - Filled signal bar.
- `.pulsar-signal-bar-active-accent` - Filled signal bar when connected.
- `.pulsar-signal-bar-inactive` - Empty signal bar.

#### Miscellaneous
- `.pulsar-placeholder` - Placeholder text when lists are empty.

### Example `style.css`

```css
/* Make all buttons pill-shaped */
.pulsar-button {
    border-radius: 99px;
}

/* Add a custom glow to the focused network row */
.pulsar-network-row.focused {
    background-color: rgba(139, 92, 246, 0.2);
    border: 1px solid #8b5cf6;
}

/* Change the empty state placeholder text color */
.pulsar-placeholder {
    color: #a1a1aa;
    font-style: italic;
}
```
