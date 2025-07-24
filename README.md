# zmk-hatsumini

### Info about setting up the trackball

See https://github.com/inorichi/zmk-pmw3610-driver:


### TODO
- [x] Fix cyrillic layout: add missing letters and signs
- [x] Split numbers and specials to different layers and move everything to the right hand. Layer-tap with left hand and typing non-letter stuff on the right.
- [x] Figure out how to emulate layer-tap behavior with mouse click so that it's possible to use it for scroll and MB3
- [x] Improve layer switching
    - [x] Implement POC for switching to Russian and from Russian to other layers - using a tap combo
    - [x] Implement POC for switching to Russian and from Russian to other layers - using hold-tap behavior
    - [x] Cyrillic layout should be able to switch to other layouts but with switching language at the same time
- [x] Sync layout with cheatsheet v2, including homerow mods and compose key
    - [x] common keys
    - [x] layer switch combos
    - [x] layer switch hold-tap
    - [x] scroll
    - [x] dvorak keys
    - [x] qwerty keys
    - [x] qwerty combos
    - [x] special keys
    - [x] number keys
    - [x] nav keys
    - [x] fn keys
    - [x] mouse keys
    - [x] blank keys instead of transparent
    - [x] homerow mods - copypaste from hold-tap article
- [x] Fixes
    - [x] switching from cyrillic to other layers doesn't switch language
    - [x] cyrillic layer hold doesn't switch language
    - [x] in navigation and mouse layers right hand mods should be disabled
    - [x] MO_NUM, MO_SPEC etc are not working - maybe because layers have hierarchy and instead of &mo I need to use &to
- [x] Add colon to numbers
- [x] Swap forward slash and back slash
- [x] Add PrintScreen
- [x] Add MB1 and MB2 to hold left and right from scroll hold
- [x] Add caps word
- [x] Redesign specials so that "+" and "_" don't require shift
- [x] Caps word should continue after backspase and delete
- [ ] Hotkeys and improved navigation
    - [x] add volume and brightness controls to hotkey layer
    - [x] add cut/copy/paste to hotkey layer and a mod for macos
    - [x] add text navigation to nav layer: jump word, home/end - and a mod for macos
    - [x] add delete word mod that works same on macos and linux
    - [x] add undo/redo keys to hotkey layer and macos mod
    - [x] add macos workspace navigation to hotkey layer
- [x] Make up arrow repeatable
- [x] Try to optimize layer toggle
- [ ] Ideas for v2:
    - [ ] merge numbers and specials - using shift and putting extra specials in top row
    - [ ] merge mouse and navigation - put navigation to left hand or top row
    - [ ] move home row mods to middle row and put all layer switching to one bottom row
    - [ ] add sticky mods: press KEY_LMOD+mod to make it sticky, then something else to unstick it
    - [ ] add macos navigation layer: jump word, home/end
- [ ] Add something to Hotkey Layer and assign switching to it
- [ ] Try adding auto-scroll: press to start scrolling, press again to stop - look at Key Repeat behavior
- [ ] try snipe layer
- [ ] Try changing scroll speed
- [ ] try automouse layer (AML)


### Generating switching between layers

```
layers = [
 'LAYER_DVORAK',
 'LAYER_QWERTY',
 'LAYER_SPEC',
 'LAYER_NUMBER',
 'LAYER_NAV',
 'LAYER_FN',
 'LAYER_HOTKEY',
 'LAYER_MOUSE',
 ]

for layer_from in layers:
    print(f'// from {layer_from}')
    for layer_to in layers:
        if layer_from == layer_to:
            continue
        print(f'COMBO_TO_LAYER{'_LANG' if 'QWERTY' in layer_from or 'QWERTY' in layer_to else ''}{'_MACOS' if 'DVORAK' in layer_from else ''}_RH({layer_from}, {layer_to})')

```