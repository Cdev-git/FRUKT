# FRUKT UI
uGUI menus for FRUKT mods. BepInEx 6 IL2CPP and MelonLoader 0.7.

```cs
var w = Ui.Window("My Mod");
w.Key = Keys.F3;
w.Toggle("God mode", false, on => god = on);
w.Slider("Gravity", 0, 20, 9.81f, v => Physics.gravity = new Vector3(0, -v, 0));
var row = w.Row();
row.Button("Spawn", Spawn);
row.Button("Clear", Clear);
```

## Install
BepInEx: `BepInEx/plugins` + `[BepInDependency(FruktUI.Ui.Guid)]`
MelonLoader: `Mods` + `[assembly: MelonAdditionalDependencies("FruktUI")]`
Main thread only.

## Window
`Ui.Window(title, width)`
- `Title` `Visible` `Show()` `Hide()` `Toggle()` `Center()` `Remove()` `ScrollTo(y)`
- `Key` toggle key, `Keys.None` for none
- `Position` `WindowWidth` in 1920x1080 units
- `MaxHeight` scrolls past this, default 640
- `FreeCursor` `Closable` `Remember` default true
- `OnOpen` `OnClose`

## Containers
Window, `Row()`, `Column()`, `Scroll()` and tab pages all have:
```cs
Label(text)  Header(text)  Note(text)
Button(text, onClick)
Toggle(text, value, onChanged)
Slider(text, min, max, value, onChanged)
Dropdown(text, options, index, onChanged)
TextField(text, value, onChanged)
KeyField(text, key, onChanged)
Progress(text, value)
Image(texture, height)
Row()  Column()  Scroll(height)  Tabs()
Separator()  Space(height)  Clear()  Items
```
Empty `text` makes the control full width.

## Controls
Every control: `Visible` `Enabled` `Tooltip` `Height` `Width` `Grow` `Tag` `ScreenRect` `GameObject` `RectTransform` `Remove()`
- **Label** `Text` `Color`
- **Button** `Text` `Highlight` `OnClick` `Click()`
- **Toggle** `Text` `Value` `OnChanged` `SetSilently()`
- **Slider** `Text` `Min` `Max` `Value` `Whole` `Step` `Format` `Display` `OnChanged` `SetSilently()`
- **Dropdown** `Options` `Index` `Selected` `OnChanged` `SetOptions(list, index)` `SetSilently()`
- **TextField** `Value` `Placeholder` `MaxLength` `Allow` `OnChanged` `OnSubmit` `Focused` `Focus()` `SetSilently()`
- **KeyField** `Value` `Listening` `OnChanged` (Escape cancels, Backspace clears)
- **ProgressBar** `Value` (0-1) `Text` `Display`
- **ImageBox** `Texture` `Tint`
- **ScrollBox** `Offset` `ScrollToEnd()`
- **Tabs** `Page(name)` `Index` `OnChanged`

Setting `Value` or `Index` fires `OnChanged`. `SetSilently` doesn't.

## Toast and HUD
```cs
Ui.Toast("Saved", 3f);
var hud = Ui.Hud("30 / 30", Anchor.BottomRight, 40, 120);
hud.Text = "29 / 30";
```

## Keys
Windows virtual key codes: `Keys.F1`, `Keys.R`, `Keys.Mouse4`...
```cs
Keys.Pressed(Keys.G)
Keys.Held(Keys.LeftShift)
Keys.Name(Keys.PageUp)
```
False while typing or when FRUKT isn't focused. Don't use `Application.isFocused`.

## Ui
`Windows` `CloseAll()` `PointerOverUi` `Typing` `GameFocused` `Guid` `Version`
`OnUpdate` runs every frame after input.

## Theme
Set before building windows.
```cs
Theme.Accent = new Color(0.4f, 0.8f, 1f);
Theme.RowHeight = 34f;
Theme.Sounds = false;
```
Colors: `Panel` `Bar` `Line` `Text` `Muted` `Accent` `AccentText` `Control` `ControlHover` `ControlPressed` `Field` `Track` `Disabled`
Sizes: `FontSize` `TitleSize` `HeaderSize` `RowHeight` `Spacing` `Padding` `TitleHeight`
`Font` is the game's font, or set your own `TMP_FontAsset`.
