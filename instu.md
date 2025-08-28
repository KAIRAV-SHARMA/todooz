# 📱 Mobile Optimization Prompt for Cursor

You are optimizing the **Veltra Automations** website for **all mobile breakpoints (≤1024px, ≤768px, ≤480px)**.  
Do not rewrite desktop code — only apply **responsive overrides**.  
Preserve the **premium, futuristic, trustworthy feel** of the site.

---

## 🎯 Goals
- Ensure all sections (Nav, Hero, Products, About, FAQ, Contact, Modal) look **flawless on mobile**.  
- No clipped text, broken grids, or hidden CTAs.  
- CTAs must remain **tap-friendly (≥44px height)**.  
- Animations and background morphing must scale smoothly on smaller screens.  

---

## 🔑 Responsive Adjustments

### 1. Navigation Bar & Overlay
- **≤1024px**: Hide desktop `.nav-links`, show `.mobile-menu-btn`.  
- Full-screen mobile overlay: **dark gradient + blur**, vertical stacked links with `52px` spacing.  
- **CTA button**: large, full-width, **fixed at bottom** inside overlay.  

### 2. Hero Section
- **Video background**: `object-fit: cover`, auto-center crop.  
- Reduce **hook text size** by ~20%.  
- Keep hero CTAs stacked **vertically with 16px gap**, buttons expand full width.  
- Maintain **fade-in reveal** after delay, even on reload.  

### 3. Products Section
- **≤1024px**: Grid → 2 columns.  
- **≤768px**: Grid → single column, card padding reduced (24px → 20px).  
- **≤480px**: Headings scale down (`2rem` max), CTAs shrink padding.  

### 4. About Section
- **≤768px**: Collapse grid → single column, text center-aligned.  
- **Counters**: Stack vertically with `32px` gap.  
- Titles and paragraphs scale with `clamp()` for readability.  

### 5. FAQ Section
- Accordion must remain **full-width** with padding reduced to `20px`.  
- Questions remain **one-line on small screens**, icons aligned right.  

### 6. Contact Section
- **≤768px**: Contact grid → single column.  
- Emails and phone numbers remain tappable (no zoom).  
- Founder cards stack vertically with `24px` spacing.  

### 7. Book a Demo Modal
- On mobile:  
  - **Max height 85vh**, scrollable inside modal.  
  - Form inputs stacked, dropdowns span full width.  
  - Phone/time groups collapse to vertical layout.  
  - Submit button full width.  

### 8. Orb & Background Morph System
- On mobile:  
  - Reduce orb size (5px → 3.5px).  
  - Limit to 25 orbs per section.  
  - Maintain smooth scroll morph without lag.  

---

## ✅ Expected Mobile UX
- Clean, legible typography scaled with `clamp()`.  
- Seamless morphing background across all devices.  
- Nav overlay feels premium: gradient blur, stacked links, CTA at bottom.  
- Hero video + text perfectly centered with safe padding.  
- All CTAs easily tappable with consistent spacing.  
- No horizontal scrolling anywhere.  

---

**Instruction for Cursor:**  
Apply these overrides **only inside responsive breakpoints** without changing desktop layout. Keep all animations and premium visuals intact.
