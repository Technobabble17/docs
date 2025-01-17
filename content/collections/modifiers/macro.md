---
id: c0ab61af-c0c2-4ead-b64f-2e23325e917f
blueprint: modifiers
modifier_types:
  - string
  - array
  - utility
  - markup
title: Macro
---
Macro is a very special modifier. It performs no modifications of its own, but rather lets you create reusable groups of modifiers and give them a name. Those groups are each called a "macro" and are stored in your `resources/macros.yaml` file. Keep in mind that the order of modifiers within a macro matter, the same way as regular modifiers.


```yaml
# /resources/macros.yaml
headline:
  title: true
  widont: true
  remove_right: .

# Page content
title: Actually i don't know what we're talking about.
```

::tabs

::tab antlers
```antlers
{{ title | macro('headline') }}
```
::tab blade
```blade
{{ Statamic::modify($title)->macro('headline') }}
```
::

```html
Actually I Don't Know What We're Talking&nbsp;About
```

When passing multiple parameters to a modifier, you'll need to pop down into a simple list:

```yaml
# /resources/macros.yaml
excerpt:
  safe_truncate:
    - 175
    - ...
```

This is equivalent to:

::tabs
::tab antlers
```antlers
{{ content | safe_truncate(175, '...') }}
```
::tab blade
```blade
{{ Statamic::modify($content)->safeTruncate([175, '...']) }}
```
::
