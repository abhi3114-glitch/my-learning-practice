# Framer Motion

## Overview
Framer Motion is a production-ready motion library for React that makes creating animations simple and declarative.

## Basic Usage

### Simple Animation
```jsx
import { motion } from 'framer-motion';

function App() {
  return (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      transition={{ duration: 0.5 }}
    >
      Hello World
    </motion.div>
  );
}
```

### Animate Properties
```jsx
<motion.div
  animate={{
    x: 100,
    y: 50,
    scale: 1.2,
    rotate: 180,
    opacity: 0.5,
    backgroundColor: "#ff0000",
  }}
/>
```

## Gestures

### Hover & Tap
```jsx
<motion.button
  whileHover={{ scale: 1.1 }}
  whileTap={{ scale: 0.95 }}
  transition={{ type: "spring", stiffness: 400 }}
>
  Click me
</motion.button>
```

### Drag
```jsx
<motion.div
  drag
  dragConstraints={{ left: -100, right: 100, top: -100, bottom: 100 }}
  dragElastic={0.2}
  whileDrag={{ scale: 1.1 }}
>
  Drag me
</motion.div>
```

## Variants

### Defining Variants
```jsx
const containerVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: {
      staggerChildren: 0.1,
    },
  },
};

const itemVariants = {
  hidden: { y: 20, opacity: 0 },
  visible: { y: 0, opacity: 1 },
};

function List({ items }) {
  return (
    <motion.ul
      variants={containerVariants}
      initial="hidden"
      animate="visible"
    >
      {items.map((item) => (
        <motion.li key={item.id} variants={itemVariants}>
          {item.text}
        </motion.li>
      ))}
    </motion.ul>
  );
}
```

## AnimatePresence

### Exit Animations
```jsx
import { motion, AnimatePresence } from 'framer-motion';

function Modal({ isOpen, onClose }) {
  return (
    <AnimatePresence>
      {isOpen && (
        <motion.div
          initial={{ opacity: 0, scale: 0.9 }}
          animate={{ opacity: 1, scale: 1 }}
          exit={{ opacity: 0, scale: 0.9 }}
          transition={{ duration: 0.2 }}
          className="modal"
        >
          <p>Modal content</p>
          <button onClick={onClose}>Close</button>
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

### List Animations
```jsx
function TodoList({ todos }) {
  return (
    <AnimatePresence>
      {todos.map((todo) => (
        <motion.li
          key={todo.id}
          initial={{ opacity: 0, x: -100 }}
          animate={{ opacity: 1, x: 0 }}
          exit={{ opacity: 0, x: 100 }}
          layout
        >
          {todo.text}
        </motion.li>
      ))}
    </AnimatePresence>
  );
}
```

## Layout Animations

### Shared Layout
```jsx
function Card({ isExpanded, onClick }) {
  return (
    <motion.div 
      layout 
      onClick={onClick}
      style={{ borderRadius: 16 }}
    >
      <motion.h2 layout>Title</motion.h2>
      {isExpanded && (
        <motion.p
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
        >
          Expanded content
        </motion.p>
      )}
    </motion.div>
  );
}
```

### Layout ID for Shared Elements
```jsx
function Gallery({ selectedId }) {
  return (
    <div className="gallery">
      {items.map((item) => (
        <motion.img
          key={item.id}
          layoutId={item.id}
          src={item.src}
          onClick={() => setSelected(item.id)}
        />
      ))}
      
      <AnimatePresence>
        {selectedId && (
          <motion.div className="overlay">
            <motion.img
              layoutId={selectedId}
              src={items.find(i => i.id === selectedId).src}
            />
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
}
```

## Scroll Animations

### useScroll
```jsx
import { motion, useScroll, useTransform } from 'framer-motion';

function ParallaxImage() {
  const { scrollYProgress } = useScroll();
  const y = useTransform(scrollYProgress, [0, 1], [0, -200]);
  
  return (
    <motion.img
      src="image.jpg"
      style={{ y }}
    />
  );
}
```

### Scroll-triggered
```jsx
import { motion, useInView } from 'framer-motion';

function Section() {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: true });
  
  return (
    <motion.section
      ref={ref}
      initial={{ opacity: 0, y: 50 }}
      animate={isInView ? { opacity: 1, y: 0 } : {}}
      transition={{ duration: 0.6 }}
    >
      Content
    </motion.section>
  );
}
```

## Hooks

### useAnimation
```jsx
import { motion, useAnimation } from 'framer-motion';

function ControlledAnimation() {
  const controls = useAnimation();
  
  const handleClick = async () => {
    await controls.start({ x: 100 });
    await controls.start({ rotate: 180 });
    await controls.start({ x: 0, rotate: 0 });
  };
  
  return (
    <motion.div animate={controls}>
      <button onClick={handleClick}>Animate</button>
    </motion.div>
  );
}
```

### useMotionValue & useTransform
```jsx
import { motion, useMotionValue, useTransform } from 'framer-motion';

function Slider() {
  const x = useMotionValue(0);
  const background = useTransform(
    x,
    [-100, 0, 100],
    ["#ff0000", "#ffffff", "#00ff00"]
  );
  
  return (
    <motion.div style={{ background }}>
      <motion.div
        drag="x"
        style={{ x }}
        dragConstraints={{ left: -100, right: 100 }}
      />
    </motion.div>
  );
}
```

## Transition Types

```jsx
// Spring
<motion.div
  animate={{ x: 100 }}
  transition={{ type: "spring", stiffness: 100, damping: 10 }}
/>

// Tween
<motion.div
  animate={{ x: 100 }}
  transition={{ type: "tween", duration: 0.5, ease: "easeInOut" }}
/>

// Inertia
<motion.div
  drag
  dragTransition={{ power: 0.3, timeConstant: 200 }}
/>
```

## Best Practices

1. Use **variants** for complex animations
2. Add **layoutId** for shared element transitions
3. Wrap exit animations with **AnimatePresence**
4. Use **useInView** for scroll-triggered animations
5. Prefer **spring** animations for natural feel
6. Use **layout** prop for automatic layout animations

## Resources
- Framer Motion Documentation
- Framer Motion Examples
- Community showcases
