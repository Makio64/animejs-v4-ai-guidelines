# Anime.js v4 Quick Reference (Condensed)

## 🚨 CRITICAL: USE V4 SYNTAX ONLY

**NEVER use `import anime from 'animejs'` - that's v3!**

## ✅ Correct v4 Import
```javascript
import { animate, createTimeline, stagger, utils, svg, engine } from 'animejs';
```

## 🎯 Quick Syntax Reference

### Basic Animation
```javascript
// ✅ CORRECT - v4
animate('.element', { x: 250, rotate: 180, duration: 800, ease: 'inOutQuad' });

// ❌ WRONG - v3 (NEVER USE)
anime({ targets: '.element', translateX: 250, easing: 'easeInOutQuad' });
```

### Timeline
```javascript
// ✅ CORRECT - v4
const tl = createTimeline({ defaults: { duration: 1000 } });
tl.add('.el1', { x: 100 })
  .add('.el2', { y: 100 }, '+=200')  // 200ms after previous
  .add('.el3', { scale: 2 }, '<');   // at start of previous

// ❌ WRONG - v3
const tl = anime.timeline();
```

### Stagger
```javascript
// ✅ CORRECT - v4
animate('.items', { x: 100, delay: stagger(100) });
animate('.items', { y: 50, delay: stagger(100, { from: 'center' }) });

// ❌ WRONG - v3
anime({ targets: '.items', stagger: 100 });
```

## 📋 Property Quick Reference

| v3 (WRONG) | v4 (CORRECT) | Notes |
|------------|--------------|-------|
| `targets: '.el'` | First parameter | `animate('.el', {...})` |
| `easing: 'easeInOutQuad'` | `ease: 'inOutQuad'` | No 'ease' prefix |
| `value: 100` | `to: 100` | For animation values |
| `direction: 'alternate'` | `alternate: true` | Boolean property |
| `loop: true` | `loop: true` | Same syntax |
| `complete: fn` | `onComplete: fn` | All callbacks prefixed with 'on' |
| `translateX` | `x` (preferred) or `translateX` | Shorthand available |

## 🔄 Transform Shorthands (Preferred)
```javascript
// Prefer shorthand
animate('.el', { x: 100, y: 50, z: 25 });

// Also valid but verbose
animate('.el', { translateX: 100, translateY: 50, translateZ: 25 });
```

## ⏱️ Use Seconds (Optional)
```javascript
import { engine } from 'animejs';
engine.timeUnit = 's';  // Now use seconds like GSAP
animate('.el', { x: 100, duration: 1 });  // 1 second
```

## 🔴 Common Mistakes to Avoid

1. **Wrong import**: `import anime from 'animejs'` ❌
2. **Using targets**: `{ targets: '.el' }` ❌
3. **Wrong easing**: `{ easing: 'easeInOutQuad' }` ❌
4. **Using value**: `{ x: { value: 100 } }` ❌
5. **Wrong timeline**: `anime.timeline()` ❌
6. **Wrong callbacks**: `{ complete: fn }` ❌

## 🎨 Common Patterns

```javascript
// Fade in
animate('.el', { opacity: [0, 1], y: [20, 0], duration: 600 });

// Infinite loop
animate('.el', { rotate: 360, duration: 2000, loop: true });

// Scale bounce
animate('.el', { scale: [0, 1], duration: 800, ease: 'outElastic(1, 0.5)' });

// Hover effect
el.addEventListener('mouseenter', () => animate(el, { scale: 1.1, duration: 300 }));
el.addEventListener('mouseleave', () => animate(el, { scale: 1, duration: 300 }));
```

## ✅ Quick Validation Checklist

Before using anime.js code:
- [ ] Import uses `{ animate, ... }` NOT `anime`
- [ ] Using `animate()` NOT `anime()`
- [ ] Using `ease:` NOT `easing:`
- [ ] NO `targets` property
- [ ] Callbacks have `on` prefix
- [ ] Using `createTimeline()` for timelines

**Remember: If you see `anime({ targets: ... })` it's v3 - UPDATE IT!**