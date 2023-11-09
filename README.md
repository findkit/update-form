# `updateForm()`

Javascript function to update from fields from a Javascript object which can handle inputs, selects, radio buttons and checkboxes.

## Install

Just copy paste [it](#code). You don't need npm for small functions.

## Usage

```js
const form = document.querySelector(form);

updateForm(form, {
  name: "John Doe",
  tags: ["ding", "dong"],
});

```

## Code


```js
/**
 * See https://findk.it/update-form
 *
 * @param {HTMLFormElement} form
 * @param {{ [key: string]: string | string[] }} data
 */
function updateForm(form, data) {
    for (const [key, values] of Object.entries(data)) {
        const item = form.elements.namedItem(key);
        const arrayValues = Array.isArray(values) ? values : [values];
        for (const value of arrayValues) {
            const list =
                item instanceof RadioNodeList ? Array.from(item) : [item];
            for (const el of list) {
                if (el instanceof HTMLSelectElement) {
                    for (const option of el.options) {
                        if (option.value === value) {
                            option.selected = true;
                            continue;
                        }
                    }
                } else if (el instanceof HTMLInputElement) {
                    if (el.type === "checkbox" || el.type === "radio") {
                        el.checked = el.value === value;
                    } else {
                        el.value = value;
                    }
                }
            }
        }
    }
}
```
