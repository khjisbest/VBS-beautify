# VBS Beautifier

A single-file browser tool for deobfuscating and beautifying VBScript (.vbs) code.

## Features

Each feature can be toggled on/off independently:

| Toggle | Description |
|--------|-------------|
| **Eval arithmetic** | Evaluates pure numeric expressions (`2*3+1` → `7`, `Chr(64+1)` → `"A"`) |
| **Resolve Chr()** | Converts `Chr(72)` / `ChrW(&H48)` to string literals or VBS constants (`vbCr`, `vbLf`, `vbTab`) |
| **Resolve Replace()** | Evaluates `Replace("obfXMFuscated", "XMF", "")` → `"obfuscated"` |
| **Join & / + concat** | Merges adjacent string literals (`"Hel" & "lo"` → `"Hello"`) |
| **Beautify** | Re-indents VBScript blocks and splits `:` colon-separated statements onto individual lines |

## Processing pipeline

```
Eval arithmetic → Resolve Chr() → Resolve Replace() → Join concat → Beautify
```

The order matters: arithmetic runs first so `Chr(64+1)` → `Chr(65)` → `"A"` chains correctly.

## Usage

Open `index.html` in a browser (no build step, no dependencies).

```bash
python -m http.server 8080
# then open http://localhost:8080
```

Keyboard shortcut: **Ctrl+Enter** to process.

## Supported VBScript constructs (indentation)

`If/ElseIf/Else/End If` · `For/Next` · `For Each/Next` · `While/Wend` · `Do/Loop` · `With/End With` · `Sub/End Sub` · `Function/End Function` · `Class/End Class` · `Property Get/Let/Set` · `Select Case/Case/End Select`
