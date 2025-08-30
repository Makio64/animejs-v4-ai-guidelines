# GSAP to Anime.js v4 Migration Guide

## Time Units Configuration

To make migration from GSAP easier, you can configure anime.js to use seconds instead of milliseconds:

```javascript
import { engine } from 'animejs';

// Set to seconds (like GSAP)
engine.timeUnit = 's';

// Now you can use GSAP-like durations
animate('.box', { x: 300, duration: 2, ease: 'inOutQuad' });  // 2 seconds
```

## Core Concepts Comparison

| GSAP | Anime.js v4 | Notes |
|------|------------|-------|
| `gsap.to()` | `animate()` | Basic tween |
| `gsap.timeline()` | `createTimeline()` | Timeline creation |
| `gsap.set()` | `utils.set()` | Set properties instantly |
| `gsap.fromTo()` | Use array syntax | `{ x: [0, 100] }` |
| `gsap.stagger` | `stagger()` | Stagger helper |
| `ScrollTrigger` | `createScrollObserver()` | Scroll animations |

## Basic Animations

### Simple Tween
```javascript
// GSAP
gsap.to('.box', {
  x: 300,
  rotation: 360,
  duration: 2,
  ease: 'power2.inOut'
});

// Anime.js v4
import { animate } from 'animejs';

animate('.box', { x: 300, rotate: 360, duration: 2000, ease: 'inOutQuad' });
```

### From Animation
```javascript
// GSAP
gsap.from('.box', { opacity: 0, y: 50, duration: 1 });

// Anime.js v4
animate('.box', { opacity: { from: 0 }, y: { from: 50 }, duration: 1 });
```

### FromTo Animation
```javascript
// GSAP
gsap.fromTo('.box', 
  { x: 0, opacity: 0 },
  { x: 300, opacity: 1, duration: 2 }
);

// Anime.js v4
animate('.box', { x: { to: [0, 300] }, opacity: { to: [0, 1] }, duration: 2000 });
```

## Timelines

### Basic Timeline
```javascript
// GSAP
const tl = gsap.timeline();
tl.to('.box1', { x: 300, duration: 1 })
  .to('.box2', { y: 200, duration: 1 }, '-=0.5')
  .to('.box3', { rotation: 360, duration: 1 }, '<');

// Anime.js v4
import { createTimeline } from 'animejs';

const tl = createTimeline();
tl.add('.box1', { x: 300, duration: 1000 })
  .add('.box2', { y: 200, duration: 1000 }, '-=500')
  .add('.box3', { rotate: 360, duration: 1000 }, '<');
```

### Timeline with Defaults
```javascript
// GSAP
const tl = gsap.timeline({
  defaults: { duration: 1, ease: 'power2.out' },
  repeat: -1,
  yoyo: true
});

// Anime.js v4
const tl = createTimeline({
  defaults: { duration: 1000, ease: 'outQuad' },
  loop: true,
  alternate: true
});
```

## Stagger Animations

### Basic Stagger
```javascript
// GSAP
gsap.to('.item', {
  x: 100,
  stagger: 0.1
});

// Anime.js v4
import { animate, stagger } from 'animejs';

animate('.item', {
  x: 100,          // shorthand works!
  delay: stagger(100)
});
```

### Advanced Stagger
```javascript
// GSAP
gsap.to('.item', {
  scale: 1.5,
  stagger: {
    amount: 1,
    from: 'center',
    grid: [10, 10],
    axis: 'x'
  }
});

// Anime.js v4
animate('.item', {
  scale: 1.5,
  delay: stagger(100, {
    from: 'center',
    grid: [10, 10],
    axis: 'x'
  })
});
```

## Easing Functions

| GSAP | Anime.js v4 |
|------|------------|
| `'none'` or `'linear'` | `'linear'` |
| `'power1.in'` | `'in'` |
| `'power1.out'` | `'out'` |
| `'power1.inOut'` | `'inOut'` |
| `'power2.in'` | `'inQuad'` |
| `'power2.out'` | `'outQuad'` |
| `'power2.inOut'` | `'inOutQuad'` |
| `'power3.in'` | `'inCubic'` |
| `'power3.out'` | `'outCubic'` |
| `'power3.inOut'` | `'inOutCubic'` |
| `'power4.in'` | `'inQuart'` |
| `'power4.out'` | `'outQuart'` |
| `'power4.inOut'` | `'inOutQuart'` |
| `'back.in'` | `'inBack'` |
| `'back.out'` | `'outBack'` |
| `'back.inOut'` | `'inOutBack'` |
| `'elastic.out'` | `'outElastic'` |
| `'bounce.out'` | `'outBounce'` |
| `'circ.out'` | `'outCirc'` |
| `'expo.out'` | `'outExpo'` |
| `'sine.inOut'` | `'inOutSine'` |

### Custom Easing
```javascript
// GSAP
gsap.to('.box', {
  x: 300,
  ease: CustomEase.create('custom', 'M0,0 C0.4,0 0.2,1 1,1')
});

// Anime.js v4
import { animate, eases } from 'animejs';

animate('.box', {
  translateX: 300,
  ease: eases.cubicBezier(0.4, 0, 0.2, 1)
});
```

## Control Methods

```javascript
// GSAP
const tween = gsap.to('.box', { x: 300, duration: 2 });
tween.pause();
tween.resume();
tween.reverse();
tween.seek(1);
tween.progress(0.5);
tween.kill();

// Anime.js v4
const animation = animate('.box', { translateX: 300, duration: 2000 });
animation.pause();
animation.resume();
animation.reverse();
animation.seek(1000);
animation.progress = 0.5;
animation.cancel();
```

## Callbacks

```javascript
// GSAP
gsap.to('.box', {
  x: 300,
  onStart: () => console.log('Started'),
  onUpdate: () => console.log('Updating'),
  onComplete: () => console.log('Complete'),
  onRepeat: () => console.log('Repeat')
});

// Anime.js v4
animate('.box', {
  x: 300,          // shorthand works!
  onBegin: () => console.log('Started'),
  onUpdate: () => console.log('Updating'),
  onComplete: () => console.log('Complete'),
  onLoop: () => console.log('Loop')
});
```

## ScrollTrigger → ScrollObserver

```javascript
// GSAP with ScrollTrigger
gsap.to('.box', {
  x: 300,
  scrollTrigger: {
    trigger: '.box',
    start: 'top 80%',
    end: 'bottom 20%',
    scrub: true
  }
});

// Anime.js v4
import { createScrollObserver, animate } from 'animejs';

const scrollAnimation = animate('.box', {
  translateX: 300,
  autoplay: false
});

createScrollObserver({
  target: '.box',
  visibility: 0.2,  // Start when 20% visible
  onEnter: () => scrollAnimation.play(),
  // For scrub-like behavior, use onScroll
  onScroll: (observer) => {
    scrollAnimation.seek(observer.progress * scrollAnimation.duration);
  }
});
```

## Advanced Patterns

### Morph SVG Paths
```javascript
// GSAP (with MorphSVGPlugin)
gsap.to('#path1', {
  morphSVG: '#path2',
  duration: 2
});

// Anime.js v4
import { animate, svg } from 'animejs';

animate('#path1', { d: svg.morphTo('#path2'), duration: 2 });  // 2 seconds
```

### Draw SVG
```javascript
// GSAP (with DrawSVGPlugin)
gsap.fromTo('.path', 
  { drawSVG: '0%' },
  { drawSVG: '100%', duration: 2 }
);

// Anime.js v4
import { animate, svg } from 'animejs';

const drawable = svg.createDrawable('.path');
animate(drawable, { draw: '0% 100%', duration: 2 });  // 2 seconds
```

### Text Animation
```javascript
// GSAP (with SplitText)
const split = new SplitText('.text', { type: 'chars' });
gsap.from(split.chars, {
  opacity: 0,
  y: 50,
  stagger: 0.05
});

// Anime.js v4
import { animate, stagger, createTextSplitter } from 'animejs';

const splitter = createTextSplitter('.text', { type: 'chars' });
animate(splitter.chars, {
  opacity: { to: [0, 1] },
  translateY: { to: [50, 0] },
  delay: stagger(50)
});
```

## Property Names Mapping

| GSAP Property | Anime.js v4 Property |
|--------------|---------------------|
| `x` | `x` (preferred) or `translateX` |
| `y` | `y` (preferred) or `translateY` |
| `z` | `z` (preferred) or `translateZ` |
| `rotation` | `rotate` |
| `rotationX` | `rotateX` |
| `rotationY` | `rotateY` |
| `rotationZ` | `rotateZ` |
| `scaleX` | `scaleX` |
| `scaleY` | `scaleY` |
| `scale` | `scale` |
| `opacity` | `opacity` |
| `autoAlpha` | Use `opacity` + `visibility` |
| `xPercent` | `translateX: '100%'` |
| `yPercent` | `translateY: '100%'` |

## Performance Considerations

### GSAP
```javascript
// GSAP automatically batches and optimizes
gsap.to('.many-elements', {
  x: 100,
  stagger: 0.1
});
```

### Anime.js v4
```javascript
// Use timeline for better performance with many elements
const tl = createTimeline();
document.querySelectorAll('.many-elements').forEach((el, i) => {
  tl.add(el, { x: 100 }, i * 0.1);  // shorthand preferred, using seconds
});
```

## Migration Checklist

When converting from GSAP to Anime.js v4:

1. [ ] Replace `gsap.to()` with `animate()`
2. [ ] Replace `gsap.timeline()` with `createTimeline()`
3. [ ] Convert property names (x → translateX, rotation → rotate)
4. [ ] Convert duration from seconds to milliseconds (or use `engine.timeUnit = 's'`)
5. [ ] Map easing functions to Anime.js equivalents
6. [ ] Replace `stagger` object with `stagger()` function
7. [ ] Update callback names (onStart → onBegin, etc.)
8. [ ] Replace ScrollTrigger with ScrollObserver
9. [ ] Convert plugin features (MorphSVG, DrawSVG) to Anime.js equivalents
10. [ ] Test performance with large numbers of elements

## Example: Complete Migration

### GSAP Version
```javascript
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const tl = gsap.timeline({
  defaults: { duration: 1, ease: 'power2.out' },
  scrollTrigger: {
    trigger: '.container',
    start: 'top center',
    end: 'bottom center',
    scrub: 1
  }
});

tl.from('.title', { opacity: 0, y: 50 })
  .to('.boxes', { 
    x: 300, 
    rotation: 360,
    stagger: { amount: 1, from: 'start' }
  }, '-=0.5')
  .to('.fade', { autoAlpha: 0 }, '<');
```

### Anime.js v4 Version
```javascript
import { createTimeline, animate, stagger, utils, createScrollObserver } from 'animejs';

const tl = createTimeline({
  defaults: { duration: 1000, ease: 'outQuad' },
  autoplay: false
});

tl.add('.title', { 
    opacity: { to: [0, 1] }, 
    y: { to: [50, 0] }     // shorthand works!
  })
  .add('.boxes', { 
    x: 300,                // shorthand works! 
    rotate: 360,
    delay: stagger(100, { from: 'first' })
  }, '-=500')
  .add('.fade', { 
    opacity: 0,
    onComplete: () => utils.set('.fade', { visibility: 'hidden' })
  }, '<');

createScrollObserver({
  target: '.container',
  visibility: 0.5,
  onScroll: (observer) => {
    tl.seek(observer.progress * tl.duration);
  }
});
```
