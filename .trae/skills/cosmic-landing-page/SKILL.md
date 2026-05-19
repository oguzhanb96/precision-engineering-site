---
name: "cosmic-landing-page"
description: "Creates cinematic space-travel landing pages with animated cosmic backgrounds, liquid-glass UI, and smooth scroll. Invoke when building space-themed landing pages or hero sections."
---

# Cosmic Space-Travel Landing Page

Single-page landing site with two full-height sections (Hero + Capabilities), animated cosmic background, liquid-glass design system, and Framer Motion entrance animations.

## Tech Stack (CDN-only)

```html
<!-- Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Barlow:wght@300;400;500;600&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">

<!-- React 18 -->
<script src="https://unpkg.com/react@18.3.1/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js"></script>

<!-- Babel for JSX -->
<script src="https://unpkg.com/@babel/standalone@7.29.0/babel.min.js"></script>

<!-- Framer Motion -->
<script src="https://unpkg.com/framer-motion@11.11.17/dist/framer-motion.js"></script>
<script>window.Motion = window.FramerMotion;</script>
```

## Tailwind Config

```javascript
tailwind.config = {
    theme: {
        extend: {
            fontFamily: {
                heading: ['Instrument Serif', 'serif'],
                body: ['Barlow', 'sans-serif'],
            },
            borderRadius: {
                DEFAULT: '9999px',
            },
        },
    },
}
```

## Fonts

- **Instrument Serif** (italic) → `font-heading` → hero headlines, partner names
- **Barlow** → `font-body` → body text, navigation links

## Homogenized Cosmic Background (Full Page)

### CSS (Single Animated Gradient)

```css
body {
    background: linear-gradient(135deg, #0c0c1e 0%, #1a0a2e 25%, #16213e 50%, #0f0f23 75%, #1a1a3e 100%);
    background-size: 400% 400%;
    animation: cosmicShift 15s ease infinite;
}
@keyframes cosmicShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}
```

### Star Field Component

```javascript
const StarField = () => {
    const stars = Array.from({ length: 100 }, (_, i) => ({
        id: i,
        left: `${Math.random() * 100}%`,
        top: `${Math.random() * 100}%`,
        delay: `${Math.random() * 3}s`,
        size: Math.random() * 2 + 1
    }));
    return (
        <div style={{ position: 'absolute', inset: 0, overflow: 'hidden' }}>
            {stars.map((star) => (
                <div key={star.id} style={{
                    position: 'absolute',
                    left: star.left,
                    top: star.top,
                    width: `${star.size}px`,
                    height: `${star.size}px`,
                    background: 'white',
                    borderRadius: '50%',
                    animation: `twinkle ${3}s infinite`,
                    animationDelay: star.delay,
                }} />
            ))}
        </div>
    );
};
```

```css
@keyframes twinkle {
    0%, 100% { opacity: 0.3; transform: scale(1); }
    50% { opacity: 1; transform: scale(1.2); }
}
```

## Liquid-Glass Design System

### CSS

```css
.liquid-glass {
    background: rgba(255,255,255,0.01);
    background-blend-mode: luminosity;
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    border: none;
    box-shadow: inset 0 1px 1px rgba(255,255,255,0.1);
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
}
.liquid-glass:hover {
    background: rgba(255,255,255,0.03);
}
.liquid-glass::before {
    content: "";
    position: absolute;
    inset: 0;
    border-radius: inherit;
    padding: 1.4px;
    background: linear-gradient(180deg,
        rgba(255,255,255,0.45) 0%,
        rgba(255,255,255,0.15) 20%,
        rgba(255,255,255,0) 40%,
        rgba(255,255,255,0) 60%,
        rgba(255,255,255,0.15) 80%,
        rgba(255,255,255,0.45) 100%);
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor;
    mask-composite: exclude;
    pointer-events: none;
}

.liquid-glass-strong {
    background: rgba(255,255,255,0.02);
    backdrop-filter: blur(50px);
    -webkit-backdrop-filter: blur(50px);
    box-shadow: 4px 4px 4px rgba(0,0,0,0.05), inset 0 1px 1px rgba(255,255,255,0.15);
    transition: all 0.3s ease;
}
.liquid-glass-strong:hover {
    background: rgba(255,255,255,0.05);
    transform: scale(1.02);
}
.liquid-glass-strong:active {
    transform: scale(0.98);
}
```

### Liquid Glass Usage Examples

| Element | Class | Purpose |
|---------|-------|---------|
| Navbar container | `liquid-glass rounded-full` | Main nav bar |
| Inner nav links | `liquid-glass rounded-full px-1.5 py-1.5` | Link container |
| Primary CTA | `liquid-glass-strong rounded-full` | Important buttons |
| Feature cards | `liquid-glass rounded-[1.25rem]` | Content cards |
| Stat cards | `liquid-glass rounded-[1.25rem]` | Stats display |
| Tags/chips | `liquid-glass rounded-full` | Small badges |
| Icon boxes | `liquid-glass rounded-[0.75rem]` | Icon containers |

## Interactive Button Styles

```css
.btn-primary {
    background: #fff;
    color: #000;
    transition: all 0.3s ease;
}
.btn-primary:hover {
    background: #f0f0f0;
    transform: scale(1.05);
    box-shadow: 0 10px 40px rgba(255,255,255,0.2);
}
.btn-primary:active {
    transform: scale(0.95);
}

.btn-secondary {
    color: #fff;
    transition: all 0.3s ease;
}
.btn-secondary:hover {
    text-shadow: 0 0 20px rgba(255,255,255,0.5);
}
.btn-secondary:hover svg {
    transform: translateX(4px);
}
```

## Section Structure

### Hero Section
```jsx
<section className="relative min-h-screen w-full overflow-hidden">
    <StarField />
    {/* Content with z-10 */}
</section>
```

### Capabilities Section
```jsx
<section className="relative min-h-screen w-full overflow-hidden">
    <StarField />
    {/* Content with z-10 */}
</section>
```

### Signup Section
```jsx
<section className="relative min-h-screen w-full overflow-hidden flex items-center justify-center">
    <StarField />
    {/* Content with z-10 */}
</section>
```

## BlurText Component (Word-by-Word Animation)

```javascript
const BlurText = ({ text, className }) => {
    const ref = useRef(null);
    const isInView = useInView(ref, { once: true, amount: 0.1 });
    const words = text.split(' ');

    return (
        <p ref={ref} className={`flex flex-wrap justify-center ${className}`}>
            {words.map((word, i) => (
                <motion.span
                    key={i}
                    initial={{ filter: 'blur(10px)', opacity: 0, y: 50 }}
                    animate={isInView ? [
                        { filter: 'blur(5px)', opacity: 0.5, y: -5, transition: { duration: 0.35, ease: 'easeOut', delay: i * 0.1 } },
                        { filter: 'blur(0px)', opacity: 1, y: 0, transition: { duration: 0.35, ease: 'easeOut', delay: i * 0.1 + 0.35 } }
                    ] : {}}
                    style={{ display: 'inline-block', marginRight: '0.28em' }}
                >
                    {word}
                </motion.span>
            ))}
        </p>
    );
};
```

## Key Framer Motion Animations

| Delay | Element | Animation |
|-------|---------|----------|
| 0.2s | Navbar | blur(10)→0, opacity 0→1, y: -20→0 |
| 0.4s | Badge | blur(10)→0, opacity 0→1, y: 20→0 |
| 0.8s | Subheading | blur(10)→0, opacity 0→1, y: 20→0 |
| 1.1s | CTAs | blur(10)→0, opacity 0→1, y: 20→0 |
| 1.3s | Stats | blur(10)→0, opacity 0→1, y: 20→0 |
| 1.4s | Partners | blur(10)→0, opacity 0→1, y: 20→0 |

## Navigation Implementation

```javascript
const App = () => {
    const [modal, setModal] = useState({ isOpen: false, title: '', content: '' });

    const handleNavigate = (section) => {
        if (section === 'signup') {
            setModal({ isOpen: true, title: 'Claim Your Spot', content: <SignupForm /> });
        } else {
            document.getElementById(section)?.scrollIntoView({ behavior: 'smooth' });
        }
    };

    return (
        <>
            <Navbar onNavigate={handleNavigate} />
            <main>
                <Hero onNavigate={handleNavigate} />
                <Capabilities onNavigate={handleNavigate} />
                <SignupSection />
            </main>
            <Footer onNavigate={handleNavigate} />
            <Modal isOpen={modal.isOpen} onClose={() => setModal({ isOpen: false })}>
                {modal.content}
            </Modal>
        </>
    );
};
```

## Modal Component

```javascript
const Modal = ({ isOpen, onClose, title, children }) => {
    if (!isOpen) return null;
    return (
        <motion.div
            className="fixed inset-0 z-[100] flex items-center justify-center p-4"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
        >
            <div className="absolute inset-0 bg-black/80 backdrop-blur-sm" onClick={onClose} />
            <motion.div
                className="relative liquid-glass-strong rounded-3xl p-8 max-w-md w-full"
                initial={{ scale: 0.9, opacity: 0 }}
                animate={{ scale: 1, opacity: 1 }}
            >
                <button onClick={onClose} className="absolute top-4 right-4">✕</button>
                <h3 className="font-heading italic text-white text-3xl mb-4">{title}</h3>
                {children}
            </motion.div>
        </motion.div>
    );
};
```

## Key Design Principles

1. **Homogeneous Background**: Single animated gradient on body, not per-section backgrounds
2. **StarField on Each Section**: 100 randomly positioned twinkling stars per section
3. **No Scroll Snap**: Normal smooth scrolling (snap removed)
4. **No Dark Overlays**: Contrast comes from liquid-glass chrome, not video overlays
5. **White Text Only**: All text white (#fff), no gradients or green
6. **Framer Motion Entrance**: blur(10px)→0, opacity 0→1, y: 20→0 with staggered delays
7. **Interactive Hover States**: scale, glow, text-shadow effects on buttons

## Color Palette

| Color | Hex | Usage |
|-------|-----|-------|
| Deep Space | #0c0c1e | Background base |
| Nebula Purple | #1a0a2e | Background gradient |
| Cosmic Blue | #16213e | Background gradient |
| Dark Matter | #0f0f23 | Background gradient |
| Midnight | #1a1a3e | Background gradient |
| White | #ffffff | All text, primary buttons |

## Typography Scale

| Element | Size | Font | Style |
|---------|------|------|-------|
| Hero Headline | text-6xl/7xl/5.5rem | Instrument Serif | italic |
| Section Headline | text-6xl/7xl/6rem | Instrument Serif | italic |
| Feature Title | text-3xl/4xl | Instrument Serif | italic |
| Partner Names | text-2xl/3xl | Instrument Serif | italic |
| Body | text-sm/base | Barlow | light/regular |
| Nav Links | text-sm | Barlow | medium |
| Labels | text-xs | Barlow | medium |

## Usage

When user asks for a space-themed landing page:
1. Use this skill immediately
2. Follow the exact CSS patterns for liquid-glass
3. Use the cosmic gradient on body, not sections
4. Add StarField component to each section
5. Implement BlurText for headlines
6. Add all hover states from btn-primary/btn-secondary
7. Use Framer Motion with staggered delays
