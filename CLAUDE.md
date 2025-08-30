# Anime.js v4 Reference Guide for AI Assistants

## 🚨 CRITICAL: ALWAYS USE ANIME.JS V4 SYNTAX 🚨

**This project uses Anime.js v4.x.x - DO NOT use v3 syntax under any circumstances**

**If you're about to write `import anime from 'animejs'` - STOP!**
**That's v3. This project uses v4. Use the correct import below.**

## ❌ Common AI Mistakes to Avoid

### MISTAKE #1: Using v3 Import Pattern
```javascript
// ❌ WRONG - This is v3
import anime from 'animejs';
anime({ targets: '.element', translateX: 250 });

// ✅ CORRECT - Always use v4
import { animate } from 'animejs';
animate('.element', { x: 250 });
```

### MISTAKE #2: Using 'targets' Property
```javascript
// ❌ WRONG - 'targets' is v3
animate({ targets: '.element', translateX: 250 });

// ✅ CORRECT - First parameter is the target
animate('.element', { x: 250 });
```

### MISTAKE #3: Using 'easing' Instead of 'ease'
```javascript
// ❌ WRONG
animate('.element', { x: 250, easing: 'easeInOutQuad' });

// ✅ CORRECT
animate('.element', { x: 250, ease: 'inOutQuad' });
```

### MISTAKE #4: Using 'value' for Animation Values
```javascript
// ❌ WRONG - 'value' is v3
animate('.element', { x: { value: 250 } });

// ✅ CORRECT - Use 'to' for values
animate('.element', { x: { to: 250 } });
```

### MISTAKE #5: Wrong Timeline Syntax
```javascript
// ❌ WRONG - anime.timeline() is v3
const tl = anime.timeline();

// ✅ CORRECT - Use createTimeline
import { createTimeline } from 'animejs';
const tl = createTimeline();
```

## 📝 Code Formatting Guidelines

### Single-Line Format (Preferred for Simple Animations)
Use for animations with ≤4 properties:
```javascript
// ✅ GOOD - Clean and readable
animate('.element', { x: 250, duration: 1, ease: 'outQuad' });
animate('.box', { opacity: 0.5, scale: 0.8, duration: 0.3 });
```

### Multi-Line Format (For Complex Animations)
Use for animations with >4 properties or callbacks:
```javascript
// Complex animation with callbacks
animate('.element', {
  x: { to: [0, 100, 50], duration: 1000 },
  y: { to: [0, -50, 0], duration: 1000 },
  scale: [0, 1.2, 1],
  ease: 'outElastic(1, 0.5)',
  onComplete: () => console.log('Done!')
});
```

## Installation & Import

### NPM Installation
```bash
npm install animejs
```

### ES Module Import (REQUIRED for v4)
```javascript
// ✅ CORRECT v4 imports
import { animate, createTimeline, stagger, utils, svg, eases, engine } from 'animejs';

// ❌ WRONG v3 import - NEVER USE THIS
// import anime from 'animejs';
```

## Time Units Configuration

### Convert to Seconds (GSAP-friendly)
```javascript
import { engine } from 'animejs';

// Set time unit to seconds (default is milliseconds)
engine.timeUnit = 's';

// Now all durations are in seconds
animate('.element', { x: 250, duration: 1, delay: 0.5 });  // 1 second duration, 0.5s delay

// To switch back to milliseconds
engine.timeUnit = 'ms';
```

## Core API Reference

### 1. Basic Animation

```javascript
// ✅ CORRECT v4 syntax - both work!
animate('.element', { x: 250, rotate: 180, duration: 800, ease: 'inOutQuad' });

// Also valid (explicit names):
animate('.element', { translateX: 250, rotate: 180, duration: 800, ease: 'inOutQuad' });

// ❌ WRONG v3 syntax - NEVER USE
// anime({ targets: '.element', translateX: 250, easing: 'easeInOutQuad' });
```

### 2. Timeline Creation

```javascript
// ✅ CORRECT v4
const tl = createTimeline({ defaults: { duration: 1000, ease: 'outQuad' } });

tl.add('.element1', { x: 250 })
  .add('.element2', { y: 100 }, '+=200')
  .add('.element3', { rotate: 180 }, '<');

// ❌ WRONG v3 - NEVER USE
// const tl = anime.timeline({ ... });
```

### 3. Stagger Animations

```javascript
// ✅ CORRECT v4
animate('.elements', { x: 250, delay: stagger(100) });

// With options
animate('.elements', { x: 250, delay: stagger(100, { from: 'center', ease: 'inOutQuad' }) });

// Advanced stagger
animate('.grid-item', {
  scale: [0, 1],
  delay: stagger(50, {
    grid: [10, 10],
    from: 'center',
    axis: 'x'
  })
});
```

## Transform Properties (Shorthand Preferred)

```javascript
// ✅ Both syntaxes work in v4:
animate('.element', { x: 100, y: 50, z: 25 });           // shorthand (preferred)
animate('.element', { translateX: 100, translateY: 50, translateZ: 25 }); // explicit
```

## Property Syntax Changes (v3 → v4)

### Animation Values
```javascript
// ✅ v4: Use 'to' for target values
{ opacity: { to: 0.5 } }
{ x: { to: [0, 100] } }

// ❌ v3: DON'T use 'value'
// { opacity: { value: 0.5 } }
```

### Easing Functions
```javascript
// ✅ v4: Use 'ease' (no 'ease' prefix)
{ ease: 'inOutQuad' }
{ ease: 'outElastic(1, 0.5)' }
{ ease: 'cubicBezier(0.4, 0, 0.2, 1)' }

// ❌ v3: DON'T use 'easing' or 'ease' prefix
// { easing: 'easeInOutQuad' }
```

### Direction & Looping
```javascript
// ✅ v4
{
  loop: true,        // infinite loop
  loop: 3,          // loop 3 times
  alternate: true,   // alternate direction
  reversed: true     // play in reverse
}

// ❌ v3: DON'T use 'direction'
// { direction: 'alternate' }
```

## Callbacks (ALL prefixed with 'on')

```javascript
// ✅ v4: All callbacks start with 'on'
animate('.element', {
  x: 250,
  duration: 1000,
  onBegin: (anim) => console.log('Started'),
  onUpdate: (anim) => console.log('Progress:', anim.progress),
  onComplete: (anim) => console.log('Finished')
});

// ❌ v3: DON'T use unprefixed callbacks
// { update: () => {}, complete: () => {} }
```

## SVG Animations

```javascript
import { animate, svg } from 'animejs';

// Morph path
animate('#path1', { d: svg.morphTo('#path2'), duration: 1000 });

// Draw SVG line
const drawable = svg.createDrawable('.svg-path');
animate(drawable, { draw: '0% 100%', duration: 2000 });

// Motion path
const motionPath = svg.createMotionPath('#motion-path');
animate('.element', { 
  x: motionPath.translateX, 
  y: motionPath.translateY, 
  rotate: motionPath.rotate 
});
```

## Utility Functions

```javascript
import { utils } from 'animejs';

// DOM selection
const elements = utils.$('.elements');

// Get current value
const currentX = utils.get('.element', 'translateX');

// Set values immediately
utils.set('.element', { x: 100, opacity: 0.5 });

// Remove animations
utils.remove('.element');

// Math utilities
utils.random(0, 100);
utils.shuffle([1, 2, 3, 4]);
utils.lerp(0, 100, 0.5); // 50
utils.clamp(150, 0, 100); // 100
```

## Common Animation Patterns

### Fade In
```javascript
animate('.element', { opacity: { to: [0, 1] }, y: { to: [20, 0] }, duration: 600, ease: 'outQuad' });
```

### Scale Bounce
```javascript
animate('.element', { scale: { to: [0, 1] }, duration: 800, ease: 'outElastic(1, 0.5)' });
```

### Infinite Loop
```javascript
animate('.element', { rotate: 360, duration: 2000, loop: true, ease: 'linear' });
```

### Sequential Timeline
```javascript
const tl = createTimeline();
tl.add('.step1', { x: 100, duration: 500 })
  .add('.step2', { y: 100, duration: 500 })
  .add('.step3', { scale: 2, duration: 500 });
```

### Hover Animation
```javascript
element.addEventListener('mouseenter', () => {
  animate(element, { scale: 1.1, duration: 300, ease: 'outQuad' });
});

element.addEventListener('mouseleave', () => {
  animate(element, { scale: 1, duration: 300, ease: 'outQuad' });
});
```

### Scroll-triggered Animation
```javascript
import { createScrollObserver } from 'animejs';

createScrollObserver({
  target: '.scroll-element',
  root: document.querySelector('.scroll-container'),
  play: () => animate('.element', { x: 250 }),
  visibility: 0.5
});
```

## TypeScript Support

```typescript
import { 
  animate, 
  createTimeline, 
  JSAnimation,
  Timeline,
  AnimationParams,
  TimelineParams 
} from 'animejs';

const animation: JSAnimation = animate('.element', {
  x: 250,
  duration: 1000
} as AnimationParams);

const timeline: Timeline = createTimeline({
  defaults: { duration: 800 }
} as TimelineParams);
```

## Performance Tips

1. **Use transforms over position properties**
   ```javascript
   // ✅ Good - uses transform
   animate('.element', { x: 100 });
   
   // ❌ Avoid - triggers layout
   animate('.element', { left: 100 });
   ```

2. **Batch animations in timelines**
   ```javascript
   // ✅ Good - single timeline
   const tl = createTimeline();
   elements.forEach(el => tl.add(el, { x: 100 }));
   
   // ❌ Avoid - multiple animations
   elements.forEach(el => animate(el, { x: 100 }));
   ```

3. **Use will-change CSS property for complex animations**
   ```css
   .animated-element {
     will-change: transform, opacity;
   }
   ```

## How to Identify V3 Code (DON'T USE)

If you see ANY of these patterns, it's v3 and MUST be updated:

```javascript
// All of these are V3 - NEVER USE:
anime({ ... })
anime.timeline()
anime.stagger()
anime.random()
anime.remove()
anime.get()
anime.set()
anime.running
{ targets: '...' }
{ easing: '...' }
{ value: ... }
{ direction: 'alternate' }
```

## ✅ Quick Validation Checklist

Before generating anime.js code, verify:
- [ ] Using `import { animate, ... } from 'animejs'` NOT `import anime`
- [ ] Using `animate()` NOT `anime()`
- [ ] Using `createTimeline()` NOT `anime.timeline()`
- [ ] Using `ease:` NOT `easing:`
- [ ] Using `to:` for values, NOT `value:`
- [ ] Using `on` prefix for callbacks (onUpdate, onComplete)
- [ ] Using `loop` and `alternate` NOT `direction`
- [ ] Using correct v4 stagger syntax with `stagger()`
- [ ] Using shorthand properties (x, y, z) when possible

## AI Code Generation Rules

When asked to create animations with anime.js:

1. **ALWAYS** start with v4 imports
2. **NEVER** use `anime()` function
3. **ALWAYS** use `animate()` for animations
4. **NEVER** include `targets` property
5. **ALWAYS** use `ease` not `easing`
6. **NEVER** use `value`, use `to` instead
7. **ALWAYS** prefix callbacks with `on`
8. **NEVER** use `direction`, use `alternate` and `reversed`
9. **ALWAYS** use `createTimeline()` for timelines
10. **PREFER** shorthand (`x`) over explicit (`translateX`)
11. **FORMAT** short animations on single line (≤4 properties)
12. **NEVER** generate v3 syntax under any circumstances

## Version Check
```javascript
// Current version: 4.x.x
// If you see any code using anime({ targets: ... }), it's v3 and needs updating!
```