---
title: WheelEvent
slug: Web/API/WheelEvent
page-type: web-api-interface
browser-compat: api.WheelEvent
---

{{APIRef("UI Events")}}

The **`WheelEvent`** interface represents events that occur due to the user moving a mouse wheel or similar input device.

> [!NOTE]
> This is the standard wheel event interface to use. Old versions of browsers implemented the non-standard and non-cross-browser-compatible `MouseWheelEvent` and {{DOMxRef("MouseScrollEvent")}} interfaces. Use this interface and avoid the non-standard ones.

Don't confuse the `wheel` event with the {{domxref("Element/scroll_event", "scroll")}} event:

- A `wheel` event doesn't necessarily dispatch a `scroll` event. For example, the element may be unscrollable at all. Zooming actions using the wheel or trackpad also fire `wheel` events.
- A `scroll` event isn't necessarily triggered by a `wheel` event. Elements can also be scrolled by using the keyboard, dragging a scrollbar, or using JavaScript.
- Even when the `wheel` event does trigger scrolling, the `delta*` values in the `wheel` event don't necessarily reflect the content's scrolling direction.

{{InheritanceDiagram}}

## Constructor

- {{DOMxRef("WheelEvent.WheelEvent", "WheelEvent()")}}
  - : Creates a `WheelEvent` object.

## Instance properties

_This interface inherits properties from its ancestors, {{DOMxRef("MouseEvent")}}, {{DOMxRef("UIEvent")}}, and {{DOMxRef("Event")}}._

- {{DOMxRef("WheelEvent.deltaX")}} {{ReadOnlyInline}}
  - : Returns a `double` representing the horizontal scroll amount.
- {{DOMxRef("WheelEvent.deltaY")}} {{ReadOnlyInline}}
  - : Returns a `double` representing the vertical scroll amount.
- {{DOMxRef("WheelEvent.deltaZ")}} {{ReadOnlyInline}}
  - : Returns a `double` representing the scroll amount for the z-axis.
- {{DOMxRef("WheelEvent.deltaMode")}} {{ReadOnlyInline}}
  - : Returns an `unsigned long` representing the unit of the `delta*` values' scroll amount.
- {{DOMxRef("WheelEvent.wheelDelta")}} {{ReadOnlyInline}} {{Deprecated_Inline}} {{Non-standard_Inline}}
  - : Returns an integer (32-bit) representing the distance in pixels.
- {{DOMxRef("WheelEvent.wheelDeltaX")}} {{ReadOnlyInline}} {{Deprecated_Inline}} {{Non-standard_Inline}}
  - : Returns an integer representing the horizontal scroll amount.
- {{DOMxRef("WheelEvent.wheelDeltaY")}} {{ReadOnlyInline}} {{Deprecated_Inline}} {{Non-standard_Inline}}
  - : Returns an integer representing the vertical scroll amount.

> [!NOTE]
> [Element: mousewheel event](/en-US/docs/Web/API/Element/mousewheel_event) has additional documentation about the deprecated properties `wheelDelta`, `wheelDeltaX`, `wheelDeltaY`.

## Instance methods

_This interface doesn't define any specific methods, but inherits methods from its ancestors, {{DOMxRef("MouseEvent")}}, {{DOMxRef("UIEvent")}}, and {{DOMxRef("Event")}}._

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("Element/wheel_event", "wheel")}} event
- Interfaces replaced by this one:
  - Gecko's legacy mouse wheel event object: {{DOMxRef("MouseScrollEvent")}}
