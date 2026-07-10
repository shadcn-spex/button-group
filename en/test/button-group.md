# BUTTONGROUP: Button Group Acceptance Tests

## Intent

Acceptance tests for the `button-group` package, written as Given-When-Then mapped to GEARS (Given → Where/While, When → When, Then → shall).
Each item runs against a rendered DOM (browser or DOM testing environment) with the reference styles applied, or against the imported module where stated.
Item IDs continue from [dev/button-group.md](../dev/button-group.md).

### BUTTONGROUP-15

Verifies: [BUTTONGROUP-1](../user/button-group.md#buttongroup-1), [BUTTONGROUP-9](../dev/button-group.md#buttongroup-9)

Where a `ButtonGroup` contains two buttons, when it is rendered, the DOM shall contain exactly one element with `role="group"` and `data-slot="button-group"` whose direct children are the two buttons, laid out with zero gap and equal cross-axis size.

### BUTTONGROUP-16

Verifies: [BUTTONGROUP-2](../user/button-group.md#buttongroup-2), [BUTTONGROUP-10](../dev/button-group.md#buttongroup-10)

Where a `ButtonGroup` is rendered without an `orientation` prop, the container shall carry no `data-orientation` attribute and shall apply the base and `horizontal` classes of [BUTTONGROUP-10](../dev/button-group.md#buttongroup-10).
Where a `ButtonGroup` is rendered with `orientation="horizontal"`, the container shall carry `data-orientation="horizontal"` and the same classes.

### BUTTONGROUP-17

Verifies: [BUTTONGROUP-2](../user/button-group.md#buttongroup-2), [BUTTONGROUP-10](../dev/button-group.md#buttongroup-10)

Where a `ButtonGroup` containing three buttons is rendered with `orientation="vertical"`, the container shall carry `data-orientation="vertical"` and lay the buttons out in a column, with the second and third buttons showing squared top corners and no top border, and the first and second buttons showing squared bottom corners.

### BUTTONGROUP-18

Verifies: [BUTTONGROUP-3](../user/button-group.md#buttongroup-3)

Where a `ButtonGroup`'s direct children are two nested `ButtonGroup` containers of two buttons each, when it is rendered, the outer container shall show a 0.5rem gap between the two nested groups, and the buttons inside each nested group shall stay flush with squared adjoining corners.

### BUTTONGROUP-19

Verifies: [BUTTONGROUP-4](../user/button-group.md#buttongroup-4), [BUTTONGROUP-11](../dev/button-group.md#buttongroup-11), [BUTTONGROUP-13](../dev/button-group.md#buttongroup-13)

Where a `ButtonGroup` contains two buttons with a prop-less `ButtonGroupSeparator` between them, when it is rendered, the separator element shall carry `data-slot="button-group-separator"`, `data-orientation="vertical"`, and `role="none"`, shall stretch to the container's full height, and shall be filled with the `--input` token color.

### BUTTONGROUP-20

Verifies: [BUTTONGROUP-5](../user/button-group.md#buttongroup-5), [BUTTONGROUP-11](../dev/button-group.md#buttongroup-11), [BUTTONGROUP-13](../dev/button-group.md#buttongroup-13)

Where a `ButtonGroup` contains a `ButtonGroupText` holding the text "Label" and an inline `svg` icon without a size class, when it is rendered, the text part shall be a `div` displaying "Label" with a border and the `--muted` token background, and the icon shall measure 1rem square with computed `pointer-events: none`.

### BUTTONGROUP-21

Verifies: [BUTTONGROUP-5](../user/button-group.md#buttongroup-5), [BUTTONGROUP-14](../dev/button-group.md#buttongroup-14)

Where a `ButtonGroupText` with `asChild` set is rendered with a single `label` child, the DOM shall contain a `label` element carrying the `ButtonGroupText` classes and text, and no wrapper `div` shall be rendered around it.

### BUTTONGROUP-22

Verifies: [BUTTONGROUP-6](../user/button-group.md#buttongroup-6)

Where a `ButtonGroup` contains three enabled buttons followed by an external focusable element, while focus is on the first button, when the user presses `Tab`, focus shall move to the second button.
While focus is on the third button, when the user presses `Tab`, focus shall leave the group and land on the external focusable element.

### BUTTONGROUP-23

Verifies: [BUTTONGROUP-6](../user/button-group.md#buttongroup-6)

Where a `ButtonGroup` contains three enabled buttons preceded by an external focusable element, while focus is on the second button, when the user presses `Shift+Tab`, focus shall move to the first button.
While focus is on the first button, when the user presses `Shift+Tab`, focus shall leave the group and land on the external focusable element.

### BUTTONGROUP-24

Verifies: [BUTTONGROUP-6](../user/button-group.md#buttongroup-6)

Where a `ButtonGroup` contains three enabled buttons, while focus is on the second button, when the user presses `ArrowRight`, `ArrowLeft`, `ArrowDown`, or `ArrowUp`, focus shall remain on the second button.
When the same group is rendered, neither the container nor any button shall carry a component-added `tabindex` attribute.

### BUTTONGROUP-25

Verifies: [BUTTONGROUP-7](../user/button-group.md#buttongroup-7)

Where a `ButtonGroup` contains two buttons, while the first button is focused via keyboard so that it matches `:focus-visible`, the first button shall have computed `position: relative` and `z-index: 10`, placing it above its sibling.

### BUTTONGROUP-26

Verifies: [BUTTONGROUP-8](../user/button-group.md#buttongroup-8), [BUTTONGROUP-1](../user/button-group.md#buttongroup-1)

Where a `ButtonGroup` is rendered with `aria-label="Pagination"`, the container shall be exposed with role `group` and the accessible name "Pagination".

### BUTTONGROUP-27

Verifies: [BUTTONGROUP-9](../dev/button-group.md#buttongroup-9), [BUTTONGROUP-10](../dev/button-group.md#buttongroup-10)

When the module is imported, it shall export exactly `ButtonGroup`, `ButtonGroupSeparator`, `ButtonGroupText`, and `buttonGroupVariants`.
When `buttonGroupVariants()` is called with no arguments, it shall return a class string containing the base and `horizontal` classes of [BUTTONGROUP-10](../dev/button-group.md#buttongroup-10); when called with `{ orientation: "vertical" }`, it shall return the base and `vertical` classes.

### BUTTONGROUP-28

Verifies: [BUTTONGROUP-14](../dev/button-group.md#buttongroup-14)

Where a `ButtonGroup` is rendered with `className="p-4"` and `id="toolbar"`, the container shall carry `id="toolbar"` and include `p-4` in its class attribute after the component's own classes.
Where a `ButtonGroup`'s direct children are a button, an `input`, and a select trigger without a width utility class, when it is rendered, the `input` shall grow to fill the remaining row width and the select trigger shall size to fit its content.
