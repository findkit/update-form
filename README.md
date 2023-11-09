# `updateForm()`

Javascript function to update fomr fields from a Javascript object. Handles inputs, selects, radio buttons and checkboxes.
Plays well when integrating custom forms to [FindkitUI](https://www.findkit.com/building-e-commerce-search/).

## Install

Just copy paste it. You don't need npm for everthing.

## Usage

```js
const form = document.querySelector("form");

updateForm(form, {
  name: "John Doe",
  tags: ["ding", "dong"],
});

```

Demo https://jsfiddle.net/p4qsyndv/31/

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
                        if (el.value === value) {
                            el.checked = true;
                            continue;
                        }
                    } else {
                        el.value = value;
                    }
                }
            }
        }
    }
}
```
