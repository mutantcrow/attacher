# Attacher

Attacher is a lightweight, zero-dependency JavaScript library that attaches a "reference" element (like a tooltip or popover) to a "target" element. It handles automatic positioning, collision detection (preventing the element from going off-screen), and updates position on scroll or resize events.

[Demo Link](https://attacher-demo.web.app/)

## Installation

You can install the package via npm:

```bash
npm install attacher --save-dev

```

## Basic Usage

1. **Import the library** into your project.
2. **Select your DOM elements**: You need a reference element (the one moving) and a target element (the one staying still).
3. **Instantiate the class**: Pass the reference element and your configuration options.

```javascript
import Attacher from 'attacher';

// 1. Select the elements
const reference = document.querySelector('.my-tooltip');
const target = document.querySelector('.my-button');

// 2. Initialize
const attacher = new Attacher(reference, {
  target: target,
  posPriority: 'top', // Try to place it on top first
  autoActivate: true, // Show immediately
  padding: { x: 10, y: 15 } // Add some spacing
});

```

## Configuration Options

When creating a new `Attacher` instance, you can pass a configuration object as the second argument. Here are the available options:

* **target** (Element): The DOM element to which the reference will be attached. Default is `null`.
* **posPriority** (String): The preferred position relative to the target. Options are `'top'`, `'bottom'`, or `'center'`. Default is `'bottom'`.
* **autoActivate** (Boolean): If `true`, the attacher will activate and calculate position immediately upon initialization. Default is `false`.
* **debug** (Boolean): Enables logging to the console for debugging purposes. Default is `false`.
* **watchRefreshSeconds** (Number): The interval (in seconds) at which the position is re-checked during scrolling to prevent jitter. Default is `0.5`.

**Styles Configuration:**
Pass a `styles` object within the configuration to control visual behavior:

* **transition** (Number): The CSS transition duration in seconds for movement. Default is `1`.
* **focusIndex** (Number): The z-index applied to the reference when active. Default is `10`.

**Padding Configuration:**
Pass a `padding` object to control spacing between the reference and the target:

* **x** (Number): Horizontal padding in pixels. Default is `10`.
* **y** (Number): Vertical padding in pixels. Default is `20`.

**Boundary Padding Configuration:**
Pass a `bPadding` object to control how close the reference can get to the screen edges before flipping position:

* **x** (Number): Horizontal boundary padding. Default is `25`.
* **y** (Number): Vertical boundary padding. Default is `50`.

## API Methods

After initializing the class, you can control the instance using the following methods:

* **attacher.bind(target)**
Binds the reference element to a new target element. If `autoActivate` is true, it will immediately position itself.
* **attacher.unbind()**
Unbinds the reference from the current target, clears styles, and deactivates the watcher.
* **attacher.activate(transition)**
Makes the reference visible, calculates its position, and starts watching for scroll/resize events. You can pass `true` as an argument to enable the CSS transition defined in your options.
* **attacher.deactivate()**
Hides the reference (resets styles) and stops the scroll/resize watchers to save performance.
* **attacher.refresh()**
Manually recalculates and updates the position of the reference element.

## Development

This project uses Rollup for bundling.

* **Start Development Server:** `npm start` (Runs `rollup -c -w`)
* **Build for Production:** `npm run build` (Runs `rollup -c --environment production`)

## License

ISC
