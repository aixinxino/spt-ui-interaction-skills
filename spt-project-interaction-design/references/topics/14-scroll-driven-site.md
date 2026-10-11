# Scroll-Driven Official Site

> 按需参考 · 主题 14《3种官网滚动交互》。仅使用总入口选定的模式，不把本页全部效果加入项目。任务范围、输出形式与语言以用户当前请求和总入口为准。

For an authorized implementation task, use these patterns to build responsive, browser-based scroll storytelling. If the user requests only advice, return advice without changing the project. A video or static collage is not a substitute for a requested interactive website. Apply the implementation and completion checks only to the patterns selected for this task.

## Start with the page story

Before writing components, identify the content and assign each section a job:

1. **Scroll-driven opening** introduces one product or interface.
2. **Horizontal scroll section** lets a user inspect a row of related work, features, or screens while continuing to scroll vertically.
3. **Scroll-driven exploded view** explains the parts of one physical product in a deliberate order.

Use only the patterns the content needs. If all three are requested, keep them as three visually different sections with a clear transition between them. Do not reuse one card grid with different colors and call it three interactions.

## Shared interaction rules

- The scroll position is the source of truth. Derive a normalized progress value from the section's actual start and end positions.
- Use an eased mapping such as `smoothstep` or an equivalent cubic easing for visual motion. Keep text readable while the object moves.
- A reverse scroll must reverse the same state along the same path. Do not make the page jump to a new state on the way back up.
- Keep the main object inside the vertical safe area of the page. The browser viewport, not a design-board screenshot, is the final layout authority.
- Use `position: sticky` for pinned scenes and release the pin only when the story is complete.
- Do not attach a CSS `transition` to every scroll update. That creates lag and makes the object chase the scroll. Use a frame-synced update, an animation library's scrubbed timeline, or a small interpolation loop.
- Preserve the relationship between the object and its content. A screen texture, label, or annotation must move with the surface it describes.
- Avoid visual fatigue: one meaningful zoom or focus pass is usually enough. After focusing, pan to the next detail instead of repeatedly zooming out and in.

## Pattern 1: scroll-driven opening

Build a tall section containing a sticky viewport. Start with the product closed, folded, or visually quiet in the center of the composition. The first scroll action should reveal the product rather than immediately replacing the hero with a different card.

The opening should generally follow this sequence:

1. Product enters or is already present in its closed state.
2. The title and supporting copy ease out as the user's scroll begins.
3. The product opens around its real hinge, fold, or pivot.
4. The interface or surface content remains attached to the product as it moves.
5. The product settles into its open state before the page releases into the next section.

For a laptop, rotate the screen around the bottom hinge while the base stays stable. Do not rotate the entire laptop as one flat image. If a true 3D model is unavailable, use separate screen and base layers with a clearly defined transform origin, or use a pre-rendered image sequence that already contains the correct perspective.

Keep the opening progress independent from page opacity. A useful model is:

```js
const progress = clamp((scrollY - sectionStart) / (sectionEnd - sectionStart));
const opening = easeInOutCubic(progress);
const titleOpacity = 1 - smoothstep(0.08, 0.32, progress);
const screenAngle = lerp(-8, 96, opening);
```

The exact numbers are content-dependent. The important constraints are the real pivot, a stable base, an attached surface, and a smooth reversible path.

## Pattern 2: horizontal scroll section

Pin a viewport while a horizontal track travels from right to left. The user continues to scroll vertically; the content moves horizontally without changing the user's input direction.

Compute the travel distance from the actual DOM sizes:

```js
const distance = Math.max(0, track.scrollWidth - viewport.clientWidth);
const progress = clamp((scrollY - sectionStart) / (sectionEnd - sectionStart));
track.style.transform = `translate3d(${-distance * easeInOutCubic(progress)}px, 0, 0)`;
```

If distance is zero, use normal document flow without an artificial pinned wait. Define and clamp progress using the actual sticky travel range; guard a zero-length range.

The section must remain pinned until the last card or screen is fully inside the viewport. Do not hard-code a translation that leaves the final item clipped or creates an empty stretch after the track has finished. Recalculate after font loading, image loading, and resize.

Give each item the hierarchy its real content needs; use a title, caption, category or index only when useful. Do not insert tutorial chapter numbers, effect names, or decorative English subtitles into a product website. Use a visible progress indicator when the track is long. Keep card widths large enough to inspect the content; on small screens, switch to direct touch scrolling, a paged carousel, or a normal vertical stack instead of squeezing every card into a narrow column.

## Pattern 3: scroll-driven exploded view

Use this pattern for hardware, a device, a component system, or a product whose internal structure needs explanation. The product stays optically centered while independent parts separate in a planned order.

The preferred order is:

1. Complete product state.
2. Outer shell moves away first.
3. Internal driver, board, or core component becomes visible.
4. Grille, cushion, connector, or final detail moves last.
5. Labels and explanations highlight the current part.
6. Reverse scroll brings each part back along its original path.

Only the current layer should receive strong emphasis. Do not scatter every part at once; the viewer must always know what to look at. Keep the assembled start and exploded end stable so the interaction can be scrubbed in either direction; reverse scrolling reassembles the product.

Use one of these asset strategies:

- A real 3D model with independently addressable nodes.
- Separate transparent renders or SVG layers for each part.
- A pre-rendered state sequence when the required perspective or material quality cannot be produced in the browser.

If the source is only one ordinary product photograph, do not claim that hidden internal parts have been accurately reconstructed. Either request suitable assets or label the result as a conceptual visualization.

Use progress windows instead of making every part respond to the same value:

```js
const shell = remap(progress, 0.16, 0.40);
const driver = remap(progress, 0.34, 0.64);
const detail = remap(progress, 0.58, 0.86);
```

Each `remap` value should be eased before it drives position, rotation, opacity, or scale. Keep labels in a separate UI layer so they remain crisp while the model moves.

## Visual direction

Aim for the restraint of a high-end product site:

- Establish a small token set for background, text, muted text, accent, border, and shadow before styling sections.
- Use generous whitespace and a strong typographic hierarchy. The title, support copy, navigation, and interaction hint should not compete with the model.
- Prefer one dominant product stage over multiple floating cards.
- Use subtle grid lines, gradients, depth shadows, or material highlights only when they clarify the object.
- Keep navigation and chapter labels stable while the main scene changes.
- Design the bottom of each sticky scene so the next section enters without a hard cut or an unexplained blank gap.

## Responsive and accessible behavior

- Design the desktop and mobile compositions separately when the available reading space changes materially.
- Keep all important content in semantic HTML, with meaningful headings and `alt` text for images.
- Provide keyboard and pointer access for any control that is more than decorative.
- Honor `prefers-reduced-motion`: keep the product and text visible, reduce or remove scrubbed motion, and preserve the reading order.
- Make sure the page still communicates the story if WebGL or a heavy asset fails to load. Use a clearly designed poster or static state as the fallback.
- Test at the target phone width, a narrow phone width, tablet width, and desktop width. Check that the product, labels, and last horizontal item are not clipped.

## Build and review workflow

1. Inspect the existing project, framework, route structure, and asset pipeline before changing files.
2. Identify the actual content and asset source for each product. Preserve licenses and attribution when using external assets.
3. Implement each chosen pattern as an isolated section with a measurable scroll range.
4. Add the reverse path before polishing the forward path. A scroll interaction is incomplete if it only works downward.
5. Run the project build and open the actual route in a browser.
6. Review at progress values near `0`, `0.25`, `0.5`, `0.75`, and `1`, plus the exact boundaries between sections.
7. Resize while the page is open, refresh after assets load, and check the reduced-motion path.
8. Report which route, assets, and interactions were actually verified. Do not claim browser acceptance from source inspection or a successful build alone.

## Completion criteria

For each selected pattern, apply the relevant checks below; omitted patterns are not required features:

- The opening begins with the product in the intended closed or quiet state and opens around the correct pivot.
- Titles and annotations fade or move without colliding with the product.
- The horizontal section reveals every item completely and releases at the correct point.
- The exploded view reveals one understandable layer at a time and reassembles on reverse scroll.
- No main object is clipped, compressed, or pushed out of the mobile safe area.
- The page has a reduced-motion behavior and a usable static fallback.
- The actual browser route has been checked at the section boundaries and during reverse scrolling.

When reporting the result, provide the route, the asset sources, the interaction summary, the responsive behavior, and the checks that were actually run. Do not return a video-only deliverable unless the user separately asks for a rendered video.
