# Refactoring UI

**Authors**: Adam Wathan and Steve Schoger

## Start with a Feature, Not a Layout

Begin your design process with the actual functionality, not the shell or layout. Details like typefaces, shadows, and icons can come later. Avoid obsessing over small details early on.

### Design in Grayscale

Delay the use of colors. Designing in grayscale forces you to rely on spacing, contrast, and size to establish hierarchy and clarity. This results in a stronger interface that can be enhanced with color later.

### Don't Design Too Much

Avoid designing every feature before implementation. Instead, work in **short cycles**:

1. **Start Simple**: Design a basic version of the next feature.
2. **Make It Real**: Implement the design and identify any unexpected complexities.
3. **Iterate**: Refine the design until the issues are resolved.
4. **Repeat**: Move to the next feature and repeat the process.

### Choose the Personality

Every design conveys a personality. Consider the type of impression you want to create based on your audience:

#### Typography

- **Elegant/Classic**: Use serif typefaces.
- **Modern/Neutral**: Opt for sans-serif typefaces.

#### Color

Colors influence the feel of your design:

- **Blue**: Safe and familiar.
- **Gold**: Sophisticated and luxurious.
- **Pink**: Playful and lighthearted.

#### Border Radius

- **No Radius**: Serious and formal.
- **Small Radius**: Neutral.
- **Large Radius**: Playful.

#### Language

Tone plays a critical role in personality:

- **Professional**: Use formal and precise language.
- **Friendly**: Opt for casual, conversational language.

#### Deciding the Right Personality

Look at other sites your audience uses for inspiration, but avoid mimicking direct competitors. Your design should feel unique and tailored to your audience.

### Limit Your Choices

Having too many options can be overwhelming. Simplify decision-making by defining constraints:

#### Define Systems in Advance

Establish predefined options for:

- Font sizes (e.g., a restrictive type scale).
- Margins, padding, and other spacing values.

#### Design by Process of Elimination

When selecting from a constrained set of values:

1. Guess the best option.
2. Compare it to neighboring values.
3. Eliminate bad choices until the best option remains.

#### Systematize Everything

Create systems for:

- Font sizes and weights.
- Line height.
- Colors.
- Margins and padding.
- Widths, heights, and shadows.
- Border radius and width.

Approach design with a system-focused mindset, and introduce new systems as needed. This minimizes repetitive decisions and ensures consistency.

---

## Hierarchy is Everything

### Not All Elements Are Equal

When everything in an interface is competing for attention, the result is noisy and chaotic—a wall of content where it's unclear what truly matters. By deliberately de-emphasizing secondary and tertiary information and highlighting the most important elements, the interface becomes more pleasing and clear, even without changes to the color scheme, font choice, or layout.

### Size Isn’t Everything

Relying solely on font size for hierarchy often results in disproportionate content sizes—primary content becomes too large, and secondary content too small. Instead, use font weight or color to create emphasis:

- **Bold text** communicates importance while maintaining reasonable font sizes.
- **Softer colors** for secondary text maintain readability while de-emphasizing less important content.

Stick to a simple hierarchy:

- **Two or three colors**:
  - Dark color for primary content (e.g., headlines).
  - Grey for secondary content (e.g., dates).
  - Light grey for tertiary content (e.g., footer copyright).
- **Two font weights**:
  - Normal (400-500) for most text.
  - Bold (600-700) for emphasized text.

Avoid font weights below 400 for UI work—they reduce readability.

### Don’t Use Grey Text on Colored Backgrounds

De-emphasizing text with lighter grey works on white backgrounds but fails on colored backgrounds. Instead, make the text closer to the background color to create hierarchy.

Avoid reducing opacity to achieve this—it can make text look dull, washed out, or disabled. Instead, adjust the text color to blend harmoniously with the background.

### Labels Are a Last Resort

In many cases, labels aren’t necessary. The format of the data often provides enough context (e.g., email addresses, phone numbers, or prices).

If labels are used:

- Combine labels with values for clarity (e.g., “12 left in stock” instead of “In stock: 12”).
- Treat labels as secondary content, emphasizing them only when users need to find them quickly.

### Separate Visual Hierarchy from Document Hierarchy

Semantically correct tags (e.g., `<h1>` for titles) don’t always need to dictate size. A page title like "Manage Account" doesn’t have to be large just because it’s an `<h1>`—design hierarchy should prioritize usability over semantics.

### Balance Weight and Contrast

**Weight and contrast** play a crucial role in creating hierarchy:

- **Reducing contrast**: Helps de-emphasize “heavy” elements like bold text or solid icons by using softer colors.
- **Increasing weight**: Adds emphasis to subtle elements (e.g., thin borders) without making the design feel harsh.

For icons, lower their contrast to balance their visual weight when placed next to text.

### Semantics Are Secondary

Actions on a page should reflect their importance in the hierarchy:

- **Primary actions**: Obvious and prominent (e.g., solid, high-contrast buttons).
- **Secondary actions**: Clear but less prominent (e.g., outlined or low-contrast buttons).
- **Tertiary actions**: Discoverable but unobtrusive (e.g., styled as links).

**Destructive actions**:

- Should match their place in the hierarchy.
- Use secondary or tertiary styling unless it’s the primary action.
- Combine with a confirmation step where the destructive action becomes primary and uses bold, high-contrast styling.

---

## Layout and Spacing

### Start with Too Much White Space

One of the easiest ways to clean up a design is to give every element more room to breathe. White space should be removed, not added.

- **Designing for the web**: White space is typically added when elements look too cramped—margins or padding are increased until things feel right.
- **Dense UIs have their place**: While designs with ample breathing room feel cleaner and simpler, some interfaces benefit from a more compact layout depending on the context.

### Establish a Spacing and Sizing System

Avoid nitpicking between arbitrary values like 120px and 125px. Instead, build a consistent spacing and sizing system.

- **Linear scales don’t work**: A naive approach like "make everything a multiple of 4px" doesn’t simplify decisions.
- **Defining the system**:
  - Start with a sensible base value (e.g., **16px**, which divides nicely and is the browser default font size).
  - Build a scale using factors and multiples of the base value.
  - Smaller values should be tightly packed, and larger values should become progressively more spaced out.

**Example scale**: 4px, 8px, 16px, 24px, 32px, 48px, 64px, 80px, 96px.

- **Using the system**:
  - Refer to your scale when adding spacing or sizing elements.
  - If one value isn’t enough, the next value will likely work.
  - A consistent spacing system speeds up design workflows and adds subtle uniformity to your designs.

A spacing and sizing system allows you to create cleaner, faster, and more consistent designs with less effort.

### You Don’t Have to Fill the Whole Screen

Give each element the space it needs—don’t force layouts to fill the entire canvas unnecessarily.

- **Shrink the canvas**: If designing a small interface on a large canvas feels challenging, shrink the canvas to match real-world constraints.
  - Start with mobile designs. Once satisfied, expand to larger screens and make adjustments as needed.
- **Don’t force it**: Avoid cramming elements into small areas when it’s unnecessary—let them breathe.

### Grids Are Overrated

Grid systems are helpful but shouldn’t be treated like a religion. Not all elements need to be fluid or follow a strict grid.

- **Fixed vs. relative widths**:
  - For elements like sidebars, a fixed width optimized for content is often better than a relative width (e.g., 25%).
  - The main content area can remain flexible and use its own internal grid for children.

**Don’t shrink an element until you need to.**

### Relative Sizing Doesn’t Scale

While relative sizing can help adapt designs to different screen sizes, it has limitations:

- **Headers**: On smaller screens, headers should scale down to avoid dominating the layout.
- **Small text**: Avoid scaling text too small—it can quickly become unreadable.

### Avoid Ambiguous Spacing

Spacing should clarify relationships between groups of elements, not confuse them.

- **The fix**: Increase space between groups to ensure it’s clear which elements belong together.
- **Rule of thumb**: There should always be more space _around_ a group of elements than _within_ it.

**Poor spacing** makes interfaces harder to understand and less visually appealing.

---

## Designing Text

### Establish a Type Scale

**Hand-crafted scales**:  
For interface design, it’s more practical to pick values by hand. This avoids subpixel rounding errors and gives you full control over which sizes exist, rather than relying on a mathematical formula.

- **Avoid em units**:  
  Don’t use `em` units for font sizes. Since `em` is relative to the parent element’s font size, nested elements can end up with font sizes that don’t align with your scale.

### Use Good Fonts

#### Play it Safe

For UI design, stick to neutral sans-serif fonts like **Helvetica**. If you’re unsure, rely on the system font stack:

- apple-system, Segoe UI, Roboto, Noto Sans, Ubuntu, Cantarell, Helvetica Neue;

#### Optimize for Legibility

Fonts are designed for specific purposes:

- **Headlines**: Tighter letter-spacing and shorter lowercase letters (short x-height).
- **Body text**: Wider letter-spacing and taller lowercase letters (tall x-height).

Avoid condensed typefaces or fonts with short x-heights for main UI text.

#### Trust the Wisdom of the Crowd

Popular fonts are usually good fonts. Sort font directories by popularity to simplify your choices.

### Keep Your Line Length in Check

Avoid designing text to fit the layout at the cost of readability.

- **Ideal line length**: 45–75 characters per line.
- **Wider content**: Even with mixed content like images, limit paragraph widths for better readability.

### Baseline, Not Center

Align mixed font sizes by their **baseline**—the invisible line letters rest on.

- Baseline alignment works naturally with how our eyes perceive text and avoids awkward visual inconsistencies.

### Line-Height Is Proportional

Start with a **line-height of 1.5** for readability. Adjust line-height based on content width and font size:

- **Narrow content**: Shorter line-height (e.g., 1.5).
- **Wide content**: Taller line-height (e.g., up to 2).

**Accounting for font size**:

- **Small text**: Needs extra line spacing to guide the eyes back to the next line.
- **Large text**: Requires less line spacing; a line-height of 1 can work for headlines.

**Rule**: Line-height and font size are inversely proportional. Use taller line-heights for small text and shorter line-heights for large text.

### Not Every Link Needs a Color

Links in blocks of text should stand out but not overwhelm:

- Use subtle emphasis like a heavier font weight or a darker color.
- Add underlines or color changes **on hover** for clarity.

### Align with Readability in Mind

Text alignment should match the language direction:

- **Left-aligned**: Best for English and most other languages.

#### Don’t Center Long-Form Text

Center alignment works for:

- Headlines
- Short, independent blocks of text

For anything longer than 2–3 lines, use left alignment. If necessary, rewrite content to shorten it and improve consistency.

#### Right-Align Numbers

In tables, right-align numbers to make decimals easier to compare.

#### Hyphenate Justified Text

Justified text can look great but often introduces awkward gaps. Enable hyphenation to reduce spacing issues.

### Use Letter-Spacing Effectively

**Improving all-caps legibility**:  
Most fonts are optimized for sentence case, where capital letters mix with lowercase letters. All-caps text lacks visual variety, making it harder to read.

- **Solution**: Increase letter-spacing for all-caps text to improve clarity.

---

## Working with Colors

### Ditch Hex for HSL

HSL (Hue, Saturation, Lightness) is a more intuitive way to work with colors:

- **Hue**: A color’s position on the color wheel (e.g., red, blue).
- **Saturation**: How vivid or colorful a color looks (0% = gray, 100% = vibrant).
- **Lightness**: Measures how close a color is to black (0%) or white (100%).

#### HSL vs. HSB

Don’t confuse HSL with HSB (Hue, Saturation, Brightness):

- In HSL, **50% lightness** with 100% saturation gives a pure color.
- In HSB, **100% brightness** is only white if saturation is 0%. Otherwise, it’s equivalent to 100% saturation and 50% lightness in HSL.

### You Need More Colors Than You Think

Interfaces use more colors than you might expect, especially greys.

#### Greys

You’ll need 8–10 shades of grey to cover various uses like text, backgrounds, and panels.

#### Primary Colors

Most sites need 1–2 primary colors for actions, navigation, and branding (e.g., Facebook’s blue).

#### Accent Colors

Accent colors are essential for conveying additional information or drawing attention to specific elements.

### Define Your Shades Up Front

1. **Choose the Base Color**:  
   Start with a middle shade that represents the core of your color scale.
2. **Find the Edges**:  
   Pick the darkest and lightest shades based on their use cases.
3. **Fill in the Gaps**:  
   Create at least 5–10 shades between the darkest and lightest colors. A scale of 9 shades (e.g., 100, 500, 900) is particularly versatile.

#### What About Greys?

Follow the same process as with colors:

- Darkest grey: Suitable for text.
- Lightest grey: Works well as a subtle off-white background.

### Don’t Let Lightness Kill Your Saturation

In HSL, saturation diminishes at extreme lightness values:

- At **50% lightness**, colors appear most vivid.
- At **90% lightness**, even 100% saturation can look washed out.

#### Adjusting Saturation

To maintain vibrancy, increase saturation as lightness moves away from 50%.

#### Rotating Hue for Brightness

- To make a color darker, rotate the hue towards the nearest dark hue: 0° (red), 120° (green), or 240° (blue).

### Accessible Doesn’t Have to Mean Ugly

#### Flipping the Contrast

- Light text on dark backgrounds often requires very dark colors to meet the **4.5:1 contrast ratio**.
- Instead, use **dark text on light backgrounds** for a cleaner and less intrusive design.

#### Rotating the Hue

For colored text on colored backgrounds, adjust hue, lightness, and saturation to ensure sufficient contrast.

### Don’t Rely on Color Alone

Color enhances information but shouldn’t be the sole means of communication:

- **Metric cards**: Use icons or text to indicate changes (e.g., positive or negative trends).
- **Graphs**: Rely on contrast (light vs. dark) instead of different hues to make trends distinguishable for colorblind users.

Always ensure that color supports existing design elements and isn’t the only way to convey information.

---

## Creating Depth

### Emulate a Light Source

Shadows can do more than just add flair — they help position elements on a virtual z-axis, creating a meaningful sense of depth.

- **Small shadows**: Tight blur radius makes an element feel slightly raised (e.g., buttons).
- **Medium shadows**: Moderate blur radius positions elements like dropdowns higher.
- **Large shadows**: High blur radius draws focus to elements like modal dialogs.

#### Establishing an Elevation System

To maintain consistency, define a fixed set of shadows for your design:

1. Start with the **smallest shadow** and the **largest shadow**.
2. Fill in the middle with shadows that increase in size linearly.
3. Five options are usually sufficient.

#### Combining Shadows with Interaction

Shadows enhance interactivity by providing visual cues:

- **Clickable elements**: Add a shadow when an item is clicked to make it feel elevated.
- **Pressed buttons**: Switch to a smaller shadow (or remove it) to simulate being pressed into the page.

When assigning shadows, think about where the element should sit on the z-axis rather than the shadow itself.

### Even Flat Designs Can Have Depth

Flat designs often avoid shadows, gradients, or real-world light effects. However, depth can still be conveyed in creative ways:

#### Creating Depth with Color

- Lighter colors feel closer; darker colors feel further away.
- Use lighter shades for raised elements and darker shades for inset effects (e.g., wells).

#### Using Solid Shadows

Short, vertically offset shadows with no blur radius can make elements like cards or buttons stand out while preserving a flat aesthetic.

### Overlap Elements to Create Layers

Overlapping elements can make designs feel multi-layered and dynamic:

#### Offset Elements

- Let cards or components extend beyond their container to cross transitions between backgrounds.
- Make an element taller than its parent to create overlap on both sides.

#### Overlapping Smaller Components

- Use overlap in carousel controls or similar UI elements to add depth.

#### Overlapping Images

To avoid clashing, use an **“invisible border”**:

- Match the border color to the background to create a gap between images.
- This maintains the layered appearance without visual clutter.

---

## Working with Images

### Text Needs Consistent Contrast

**Add an Overlay**  
To improve text contrast on background images:

- Add a **semi-transparent overlay**.
- Lower the image contrast.
- Colorize the image.
- Add a **text shadow** to make text more legible.

### Everything Has an Intended Size

#### Don’t Scale Up Icons

Scaling up small icons (16–24px) for larger spaces often results in disproportionate, chunky visuals. Instead:

- Enclose icons in a shape with a background color to keep them closer to their intended size while filling the space.

#### Don’t Scale Down Screenshots or Icons

Scaling down can lead to loss of clarity and professionalism. Always use appropriately sized assets.

### Beware User-Uploaded Content

#### Control the Shape and Size

To avoid background bleed (when an image’s background color blends with the UI):

- Use a **subtle inner box shadow** instead of a border.
- Alternatively, use a **semi-transparent inner border** for a clean look without clashing colors.

---

## Finishing Touches

### Supercharge the Defaults

Elevate existing design elements to make your pages more engaging:

- Replace **bullets** in lists with icons (e.g., checkmarks or arrows).
- Highlight testimonials by enlarging and recoloring quotes.
- Style **links** with custom underlines or unique colors.
- Customize form elements like checkboxes and radio buttons using brand colors for selected states.

### Decorate Your Backgrounds

#### Change the Background Color

- Use a different color to emphasize panels or page sections.
- Add a **gradient** with hues no more than 30° apart for a subtle, dynamic effect.

#### Use a Repeating Pattern

- Incorporate subtle, low-contrast patterns (e.g., from Hero Patterns).
- Patterns can be applied across the entire background or along specific edges.

#### Add a Simple Shape or Illustration

- Place geometric shapes, small pattern chunks, or simplified illustrations (e.g., a world map) in specific positions.
- Keep contrast low to ensure readability.

### Don’t Overlook Empty States

Empty states are a user’s first interaction with a new feature. Make them engaging:

- Use an image or illustration to grab attention.
- Emphasize the **call-to-action** to encourage user interaction.
- Hide unnecessary UI elements like tabs or filters until content is created.

Empty states should excite users and guide them toward the next step, avoiding a plain or uninviting experience.
