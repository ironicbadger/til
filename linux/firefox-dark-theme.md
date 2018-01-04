### Fix Firefox Text Input Box Themeing Issues

Arc Dark Theme made all my text input box backgrounds, well, dark. Too dark. Here's how to fix it.

```
cd ~/.mozilla/firefox
ls [Check for the directory for the profile you wish to fix]
cd [profile directory]
mkdir chrome
cd chrome
vi userContent.css
```

The content of `userContent.css` should be thus:

```css
input:not(.urlbar-input):not(.textbox-input):not(.form-control):not([type='checkbox']) {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

#downloads-indicator-counter {
    color: white;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

select {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}
```

- Source(s)
  - [1](https://www.youtube.com/watch?v=2a7rgRsO6q4)
  - [2](link2)
