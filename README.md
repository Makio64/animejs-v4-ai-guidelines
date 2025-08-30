# 🎨 Anime.js v4 AI Guidelines

> **Make AI assistants understand anime.js v4 syntax correctly, every time.**

This repository contains comprehensive instructions to ensure AI coding assistants (Claude, Cursor, ChatGPT, etc.) generate correct anime.js v4 code and properly migrate from GSAP.

## 🚀 Quick Usage

Just copy and paste these commands into your AI assistant:

### Claude Code
```bash
# Quick reference (condensed version):
"Add rules from https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE_CONDENSED.md"

# Full reference (comprehensive):
"Add rules from https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE.md"

# Migrate from GSAP:
"Follow https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/GSAP_TO_ANIME.md to migrate this GSAP code"
```

### Cursor
```bash
# Quick reference (condensed):
@https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE_CONDENSED.md

# Full reference:
@https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE.md

# Migrate from GSAP:
@https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/GSAP_TO_ANIME.md migrate from GSAP
```

### ChatGPT / Claude.ai / Others
```bash
# Quick reference (faster, condensed):
"Use instructions from https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE_CONDENSED.md for anime.js v4"

# Full reference (comprehensive):
"Use instructions from https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE.md for anime.js v4"

# For GSAP migration:
"Follow the guide at https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/GSAP_TO_ANIME.md"
```

## 📚 What's Included

### [`CLAUDE_CONDENSED.md`](./CLAUDE_CONDENSED.md) ⚡ (Recommended for quick tasks)
Condensed anime.js v4 reference with:
- ✅ Essential v4 syntax rules
- 🎯 Quick property reference table
- ⚠️ Common mistakes to avoid
- 🎨 Most-used animation patterns
- 📋 Validation checklist

### [`CLAUDE.md`](./CLAUDE.md) 📖 (Full reference)
Complete anime.js v4 reference guide with:
- ✅ Correct v4 syntax and imports
- ⚠️ Common AI mistakes (and how to avoid them)
- 📝 Code formatting guidelines
- 🎯 Quick validation checklist
- 📚 Full API reference
- 🎨 All animation patterns
- 💻 TypeScript support
- ⚡ Performance tips

### [`GSAP_TO_ANIME.md`](./GSAP_TO_ANIME.md)
Complete GSAP to anime.js v4 migration guide:
- 🔄 Property name mappings
- 🎨 Easing function conversions
- ⏱️ Timeline migration patterns
- 📜 ScrollTrigger → ScrollObserver
- 🎯 Side-by-side code examples

## 🎯 Why Use This?

**Problem:** AI assistants often generate outdated anime.js v3 syntax, causing errors and confusion.

**Solution:** These guidelines enforce v4 syntax and prevent common mistakes.

### Before (AI generates v3 - Wrong ❌)
```javascript
import anime from 'animejs';

anime({
  targets: '.element',
  translateX: 250,
  easing: 'easeInOutQuad',
  duration: 2000
});
```

### After (With these guidelines - Correct ✅)
```javascript
import { animate } from 'animejs';

animate('.element', { 
  x: 250, 
  ease: 'inOutQuad', 
  duration: 2000 
});
```

## 💻 Integration Options

### Option 1: Reference in your project's CLAUDE.md
Add one of these lines to your existing `CLAUDE.md`:
```markdown
# For quick reference (recommended):
For animations, follow: https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE_CONDENSED.md

# For comprehensive reference:
For animations, follow: https://github.com/Makio64/animejs-v4-ai-guidelines/blob/main/CLAUDE.md
```

### Option 2: Copy content directly
```bash
# Append to your CLAUDE.md
curl https://raw.githubusercontent.com/Makio64/animejs-v4-ai-guidelines/main/CLAUDE.md >> CLAUDE.md
```

### Option 3: Clone for reference
```bash
git clone https://github.com/Makio64/animejs-v4-ai-guidelines.git
```

## 🔍 Quick Validation

When AI generates anime.js code, check for these red flags:

❌ **Wrong (v3)**
- `import anime from 'animejs'`
- `anime({ targets: ... })`
- `anime.timeline()`
- `easing: 'easeInOutQuad'`

✅ **Correct (v4)**
- `import { animate } from 'animejs'`
- `animate('.element', { ... })`
- `createTimeline()`
- `ease: 'inOutQuad'`

## 🤝 Contributing

Found an issue or want to add more examples? Contributions are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-addition`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-addition`)
5. Open a Pull Request

## 📄 License

MIT License - Use these guidelines freely in your projects!

## 🔗 Resources

- [Anime.js v4 Documentation](https://animejs.com)
- [GSAP Documentation](https://greensock.com/docs/)
- [Report Issues](https://github.com/Makio64/animejs-v4-ai-guidelines/issues)

---

**Remember:** Always verify AI-generated code uses v4 syntax. When in doubt, reference these guidelines!