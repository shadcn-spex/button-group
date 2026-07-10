# BUTTONGROUP: Button Group Implementation

## Intent

This file states the implementation requirements for regenerating a source-equivalent shadcn/ui `button-group` module.
The ground truth is the registry item [[1]]; the generated reference implementation lives at [reference/typescript/button-group.tsx](../../reference/typescript/button-group.tsx).
Item IDs continue from [user/button-group.md](../user/button-group.md).

### BUTTONGROUP-9

The module shall export exactly the four bindings below, each rendering the listed element with the listed `data-slot` attribute.

| Export | Renders | `data-slot` |
| --- | --- | --- |
| `ButtonGroup` | `div` with `role="group"` | `button-group` |
| `ButtonGroupSeparator` | the registry `separator` component | `button-group-separator` |
| `ButtonGroupText` | `div`, or the child element when `asChild` is `true` | none |
| `buttonGroupVariants` | class-variance-authority variant function (not an element) | — |

### BUTTONGROUP-10

`buttonGroupVariants` shall be a `cva` definition emitting exactly the class strings below, with `defaultVariants: { orientation: "horizontal" }`.

| Slot | Classes |
| --- | --- |
| base | `flex w-fit items-stretch has-[>[data-slot=button-group]]:gap-2 [&>*]:focus-visible:relative [&>*]:focus-visible:z-10 has-[select[aria-hidden=true]:last-child]:[&>[data-slot=select-trigger]:last-of-type]:rounded-r-md [&>[data-slot=select-trigger]:not([class*='w-'])]:w-fit [&>input]:flex-1` |
| `orientation: horizontal` | `[&>*:not(:first-child)]:rounded-l-none [&>*:not(:first-child)]:border-l-0 [&>*:not(:last-child)]:rounded-r-none` |
| `orientation: vertical` | `flex-col [&>*:not(:first-child)]:rounded-t-none [&>*:not(:first-child)]:border-t-0 [&>*:not(:last-child)]:rounded-b-none` |

When `ButtonGroup` renders, it shall apply `buttonGroupVariants({ orientation })` merged with the caller's `className`, and shall set `data-orientation` to the value of the `orientation` prop.

### BUTTONGROUP-11

`ButtonGroupText` shall apply exactly the classes `flex items-center gap-2 rounded-md border bg-muted px-4 text-sm font-medium shadow-xs [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4`, merged with the caller's `className`.
`ButtonGroupSeparator` shall render the registry `separator` component with its `orientation` prop defaulting to `"vertical"` and exactly the classes `relative m-0! self-stretch bg-input data-[orientation=vertical]:h-auto`, merged with the caller's `className`.

### BUTTONGROUP-12

The module shall use exactly the external dependencies below.

| Kind | Dependency | Used for |
| --- | --- | --- |
| npm | `class-variance-authority` | `cva`, `VariantProps` |
| npm | `radix-ui` | `Slot.Root` for `asChild` composition |
| registry | `button` | intended direct children of the group |
| registry | `separator` | composed by `ButtonGroupSeparator` |

### BUTTONGROUP-13

The module's classes shall consume only the semantic theme tokens below and shall contain no literal color values.

| Token | Utility class | Consumer |
| --- | --- | --- |
| `--muted` | `bg-muted` | `ButtonGroupText` background |
| `--border` | `border` | `ButtonGroupText` border |
| `--input` | `bg-input` | `ButtonGroupSeparator` fill |

### BUTTONGROUP-14

The module shall satisfy the composition constraints below.

- Each part shall spread all remaining props onto its rendered element and shall merge the caller's `className` after its own classes via the `cn` utility from `@/lib/utils`, so caller classes win on conflict.
- Where `asChild` is `true`, `ButtonGroupText` shall compose via `Slot.Root` from `radix-ui`, which requires exactly one child element.
- Where grouped controls are not direct children of `ButtonGroup`, the joining, focus-elevation, and sizing selectors of [BUTTONGROUP-10](#buttongroup-10) shall not apply to them, since those selectors target direct children only (`[&>*]`, `[&>input]`, `[&>[data-slot=select-trigger]]`).
- Where a direct child is a select trigger (`data-slot="select-trigger"`) without a width utility class, the base classes shall size it to fit its content; where a direct child is an `input`, the base classes shall let it grow to fill the remaining main-axis space; where the group's last child is a hidden native `select` (`aria-hidden="true"`), the last select trigger shall keep its right corner rounding.

## References

[1]: https://ui.shadcn.com/r/styles/new-york-v4/button-group.json "shadcn/ui registry — button-group (new-york-v4)"
