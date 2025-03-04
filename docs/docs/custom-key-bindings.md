---
layout: docs
class: docs
title: 'Custom Key Bindings'
language: 'en'
---

## Custom key bindings

Key bindings are specified as a list of objects.

{% highlight toml %}
[bindings]
keys = [
	{ key = "q", with = "super", action = "Quit" }
	# Bytes[27, 91, 53, 126] is equivalent to "\x1b[5~"
	{ key = "home", with = "super | shift", bytes = [27, 91, 53, 126] }
]
{% endhighlight %}

### Key

Each value in key binding will specify an identifier of the key pressed:

- <span class="keyword">a-z</span>
- <span class="keyword">0-9</span>
- <span class="keyword">F1-F24</span>
- <span class="keyword">tab</span> <span class="keyword">esc</span>
- <span class="keyword">home</span> <span class="keyword">space</span> <span class="keyword">delete</span> <span class="keyword">insert</span> <span class="keyword">pageup</span> <span class="keyword">pagedown</span> <span class="keyword">end</span>  <span class="keyword">back</span> 
- <span class="keyword">up</span> <span class="keyword">down</span> <span class="keyword">left</span> <span class="keyword">right</span>
- <span class="keyword">@</span> <span class="keyword">colon</span> <span class="keyword">.</span> <span class="keyword">return</span> <span class="keyword">[</span> <span class="keyword">]</span> <span class="keyword">;</span> <span class="keyword">\\</span> <span class="keyword">+</span> <span class="keyword">,</span> <span class="keyword">/</span> <span class="keyword">=</span> <span class="keyword">-</span> <span class="keyword">*</span>
- <span class="keyword">numpadenter</span> <span class="keyword">numpadadd</span> <span class="keyword">numpadcomma</span> <span class="keyword">numpaddivide</span> <span class="keyword">numpadequals</span> <span class="keyword">numpadsubtract</span> <span class="keyword">numpadmultiply</span>
- <span class="keyword">numpad1</span> <span class="keyword">numpad2</span> <span class="keyword">numpad3</span> <span class="keyword">numpad4</span> <span class="keyword">numpad5</span> <span class="keyword">numpad6</span> <span class="keyword">numpad7</span> <span class="keyword">numpad8</span> <span class="keyword">numpad9</span> <span class="keyword">numpad0</span>

### Action

Execute a predefined action in Rio terminal.

{% highlight rust %}
Paste
Copy
Quit
ResetFontSize
IncreaseFontSize
DecreaseFontSize
TabSwitchNext
TabSwitchPrev
CreateWindow
CreateTab
CloseTab
OpenConfigEditor
None
{% endhighlight %}

### Bytes

Send a byte sequence to the running application.

The <span class="keyword">bytes</span> field writes the specified string to the terminal. This makes
it possible to pass escape sequences, like <span class="keyword">PageUp</span> ("\x1b[5~"). Note that applications use terminfo to map escape sequences back
to keys. It is therefore required to update the terminfo when changing an escape sequence.

### With

Key modifiers to filter binding actions

- <span class="keyword">none</span>
- <span class="keyword">control</span>
- <span class="keyword">option</span>
- <span class="keyword">super</span>
- <span class="keyword">shift</span>
- <span class="keyword">alt</span>

Multiple modifiers can be combined using <span class="keyword">|</span> like this:

{% highlight rust %}
with = "control | shift"
{% endhighlight %}

<!-- 
 - `mode`: Indicate a binding for only specific terminal reported modes
    This is mainly used to send applications the correct escape sequences
    when in different modes.
    - AppCursor
    - AppKeypad
    - Alt
    A `~` operator can be used before a mode to apply the binding whenever
    the mode is *not* active, e.g. `~Alt`. -->

### Overwriting

Bindings are always filled by default, but will be replaced when a new binding with the same triggers is defined. To unset a default binding, it can be mapped to the <span class="keyword">None</span> action.

--

[Move to plugins ->](/rio/docs/plugins#plugins)