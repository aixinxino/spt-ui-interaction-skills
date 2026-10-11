# Advanced Interaction Design

> 按需参考 · 主题 09《10种高级UI交互》。仅使用总入口选定的模式，不把本页全部效果加入项目。任务范围、输出形式与语言以用户当前请求和总入口为准。

## 10 种交互模式

### 1. Radial Theme Transition｜圆形主题切换

**适用场景：** 用户点击主题切换按钮，需要从浅色模式切换到深色模式，或在两套完整页面之间切换。

**必须保留：** 以真实点击或触摸位置为圆心；圆的半径覆盖到最远的屏幕角落；两套页面保持相同尺寸和位置；只裁切上层页面，不缩放页面内容。

```text
Implement a radial theme transition for an app interface. When the user presses the theme toggle, reveal the new theme from the exact pointer or touch position as the center of an expanding circle. Calculate the circle radius based on the distance from the touch point to the farthest viewport corner. Keep both theme layers at the same scale and position, and clip only the top layer with a circular mask instead of scaling the page. Support mouse and touch input, respect prefers-reduced-motion, and use a simple fallback transition when needed.
```

### 2. Drag-to-Reorder｜拖拽排序

**适用场景：** 用户拖动列表、卡片或任务项，重新决定它们的顺序。

**必须保留：** 拖动项暂时脱离普通列表流；每一帧重新计算落点索引；其他项目形成明确的空槽；每一项独立追赶新位置；用户中途停下时，布局也停在当前状态。

```text
Create a draggable sortable list. When the user holds and drags one row, temporarily remove it from the normal list flow and calculate the insertion index continuously from the pointer position. The other rows should create a visible empty slot and move out of the way. Animate each row independently with a spring motion so the layout feels soft and staggered. Keep the dragged item attached to the pointer, prevent layout jumps, and support both touch and keyboard interactions.
```

### 3. Staggered Bulk Selection｜批量勾选

**适用场景：** 用户点击全选或批量操作，需要让多条内容依次进入选中状态。

**必须保留：** 状态可以立即更新，但视觉反馈从第一项开始错峰执行；每个勾选出现时有轻微弹性放大；不能让动画阻塞用户继续操作。

```text
Implement a select-all interaction for the existing list of items. When the user activates select all, update the selection state immediately but animate the checkmarks one by one with a short staggered delay from the first item to the last. Add a subtle elastic scale effect when each checkmark appears, then return each item to its normal size. Make the sequence feel deliberate without slowing down the actual state update, and support keyboard and screen-reader accessibility.
```

### 4. Velocity-Based Slider Snap｜滑杆惯性吸附

**适用场景：** 用户拖动带有刻度的滑杆选择数值、档位或目标值。

**必须保留：** 记录释放速度；松手后允许滑块短距离过冲；再通过弹簧回到最近的有效刻度；最终值必须被限制在合法范围内。

```text
Create a stepped slider for selecting a target value. Track the pointer velocity while the user drags. When the user releases the slider, let the thumb continue slightly past the release point based on the release velocity, then use a spring animation to pull it back to the nearest valid tick. Clamp the final value to the available range, make the overshoot subtle, and support mouse, touch, keyboard control, and reduced-motion preferences.
```

### 5. Animated Text Disclosure｜文本展开

**适用场景：** 一段说明文字、详情内容或帮助信息需要在折叠和展开之间切换。

**必须保留：** 根据真实内容高度调整容器；从当前高度连续过渡到目标高度；箭头或图标旋转 180 度；不能让文字突然出现或造成布局跳动。

```text
Create an animated text disclosure component for a collapsible description. When the user opens it, measure the real content height and animate the container from its current height to the measured height instead of suddenly revealing the text. When it closes, animate back to the collapsed height. Rotate the trailing chevron by 180 degrees to represent the two states, keep the content accessible to screen readers, and avoid layout jumps.
```

### 6. Spring Stepper Progress｜步骤条回弹

**适用场景：** 用户完成表单、购买或设置流程中的一个步骤，需要推进到下一步。

**必须保留：** 进度段先略微超过目标位置，再回弹到准确位置；完成、当前和未完成状态要清晰区分；动画不能改变真实步骤状态。

```text
Create a multi-step progress indicator. When the user completes a step, animate the next progress segment so it slightly overshoots its target and then settles back with a soft spring motion. Update the completed, current, and upcoming states clearly, keep the progress value accurate throughout the animation, and make the transition feel responsive without delaying navigation. Support keyboard accessibility and prefers-reduced-motion.
```

### 7. Ripple Feedback for Related Switches｜开关联动反馈

**适用场景：** 一组相互关联的设置中，用户切换其中一个开关，需要提醒用户它属于同一组设置。

**必须保留：** 当前开关正常改变状态；邻近开关只产生轻微震动或涟漪反馈；邻近开关的真实开关状态不能被改变。

```text
Create a settings group with multiple toggle switches. When the user changes one switch, trigger a subtle ripple-like feedback effect that spreads to the neighboring switches. The neighboring switches may slightly shake or translate, but their actual on and off states must not change. The source switch should update normally, while the ripple remains purely visual feedback. Keep the effect contained within the group, support touch and keyboard input, and disable the motion for reduced-motion users.
```

### 8. Curved Card Deletion｜卡片曲线删除

**适用场景：** 用户滑动删除卡片、消息或任务，希望让删除动作有明确的去向。

**必须保留：** 卡片沿曲线路径移动到删除图标或回收区域；移动过程中逐渐缩小、旋转和变淡；未达到删除阈值时可以取消并回到原位；真实删除按项目事务、失败回滚或撤销规则处理；动画只负责展示，退出后清理对应的本地视觉占位，不能据此认定后端删除成功。

```text
Create a swipe-to-delete card interaction. When the user swipes a card past the delete threshold, animate the card along a curved path toward the delete icon or trash area. While moving, gradually reduce its scale, rotate it slightly, and fade its opacity. Keep real deletion, failure recovery and undo consistent with the application's transaction rules; only clean up the matching visual exit placeholder after the animation, without treating animation completion as backend success. If the user releases before the threshold, smoothly return the card to its original position. Support touch, mouse, keyboard deletion, and reduced-motion preferences.
```

### 9. Stacked Card Scroll｜卡片堆叠滚动

**适用场景：** 用户滚动一组有顺序的卡片、记录或历史内容，需要保留已经看过内容的空间线索。

**必须保留：** 顶部卡片到达边界后暂时固定；后续卡片向上移动并把前面的卡片压成一摞；压缩程度、缩放和层级根据后方卡片数量变化；内容不能突然消失。

```text
Create a vertically scrollable card stack. When the top card reaches the top boundary, keep it pinned temporarily while the cards behind it move upward and compress into a visible stack. Calculate each card's vertical offset, scale, and depth based on how many cards are behind it. The more cards that move forward, the deeper and smaller the previous cards should become. Preserve the user's scroll context, avoid abrupt disappearance, and support touch, mouse wheel, and keyboard scrolling.
```

### 10. Expanding Tag Selection｜标签挤开

**适用场景：** 用户从一行标签、筛选项或分类项中选择一个选项，需要突出当前选择。

**必须保留：** 当前标签稍微放大；邻近标签平滑向两侧让位；元素不能互相重叠或突然跳动；小屏幕下要正确处理换行。

```text
Create a selectable tag list with animated layout reflow. When the user selects a tag, slightly enlarge the active tag and make the neighboring tags move aside to create enough space. The surrounding tags should smoothly translate rather than overlap or jump. Clearly show the selected state, preserve the original order of the tags, handle wrapping on smaller screens, and support mouse, touch, keyboard navigation, and reduced-motion preferences.
```
