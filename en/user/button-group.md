# BUTTONGROUP: Button Group Behavior

## Intent

This package pins the user-visible behavioral contract of the official shadcn/ui `button-group` component [[1]], a container that groups related buttons and companion controls with joined styling.
The contract is derived from the component source published in the shadcn/ui registry [[2]] under the MIT license (Copyright (c) 2023 shadcn).
The subjects of this package are the `ButtonGroup` container and its `ButtonGroupSeparator` and `ButtonGroupText` parts; the behavior of grouped controls themselves (buttons, inputs, select triggers) is outside this package.

### BUTTONGROUP-1

When a `ButtonGroup` renders, it shall produce a single container element with `role="group"` and `data-slot="button-group"` that sizes itself to fit its content, lays out its direct children along one axis with no gap between adjacent children, and stretches each child to the group's full cross-axis size.

### BUTTONGROUP-2

The `ButtonGroup` shall lay out and visually join its direct children according to the `orientation` table below.

| `orientation` | Layout | Joined edges |
| --- | --- | --- |
| `horizontal` (default) | children in a row | every child except the first has its left corners squared and its left border removed; every child except the last has its right corners squared |
| `vertical` | children in a column | every child except the first has its top corners squared and its top border removed; every child except the last has its bottom corners squared |

Where the `orientation` prop is set, the container shall expose its value in a `data-orientation` attribute.
Where the `orientation` prop is omitted, the container shall render the `horizontal` layout and shall not carry a `data-orientation` attribute.

### BUTTONGROUP-3

Where the direct children of a `ButtonGroup` include nested `ButtonGroup` containers, the outer container shall separate its direct children with a visible 0.5rem gap, while the children inside each nested group remain joined per [BUTTONGROUP-2](#buttongroup-2).

### BUTTONGROUP-4

When a `ButtonGroupSeparator` renders inside a `ButtonGroup`, it shall produce a divider element with `data-slot="button-group-separator"` that stretches across the group's full cross-axis size and is excluded from the accessibility tree via `role="none"`.
Where the separator's `orientation` prop is omitted, the divider shall render with `data-orientation="vertical"`.

### BUTTONGROUP-5

When a `ButtonGroupText` renders, it shall display its children as a non-interactive region visually matched to sibling buttons — bordered, filled with the muted background, in small text with medium font weight — and any inline `svg` icon inside it shall render at 1rem square (unless the icon carries its own size class) and shall not receive pointer events.
Where `asChild` is `true`, `ButtonGroupText` shall render its single child element in place of the default `div`, with the same classes and props applied to that child.

### BUTTONGROUP-6

While focus is on a focusable child of a `ButtonGroup`, when the user presses a key listed below, focus shall land as stated in the table.

| Key | Focus outcome |
| --- | --- |
| `Tab` | the next focusable element in document order: the next focusable child, or the first focusable element after the group when focus is on the last focusable child |
| `Shift+Tab` | the previous focusable element in document order: the previous focusable child, or the last focusable element before the group when focus is on the first focusable child |
| `ArrowRight` / `ArrowLeft` / `ArrowDown` / `ArrowUp` | unchanged; the group provides no arrow-key (roving) navigation of its own |

The `ButtonGroup` shall not add a `tabindex` attribute to itself or to its children.

### BUTTONGROUP-7

While a direct child of a `ButtonGroup` shows keyboard focus (matches `:focus-visible`), the container shall raise that child above its siblings (positioned, `z-index: 10`) so the child's focus ring renders unclipped by adjacent children.

### BUTTONGROUP-8

Where an `aria-label` or `aria-labelledby` prop is set on a `ButtonGroup`, the group element shall carry that attribute, exposing the corresponding accessible name for the group.

## References

[1]: https://ui.shadcn.com/docs/components/radix/button-group "shadcn/ui docs — Button Group"
[2]: https://ui.shadcn.com/r/styles/new-york-v4/button-group.json "shadcn/ui registry — button-group (new-york-v4)"
