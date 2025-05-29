[Home](index) > [Components](Components) > [Custom](Custom) > **Link Behaviour and Style**
***

## Behaviour: new window or tab
### Option 1 – Content Component

Use this option if you want a **link that is part of a paragraph** of other text that is not entirely a hyperlink.

1. Add a **Content component** to your form.
2. Enter your text and add a hyperlink using the WYSIWYG editor.
3. Save the component.
4. Click the **"Edit JSON"** icon (wrench).
5. In the JSON editor, locate the HTML line.
6. This line will have an `href` value specifying your URL
7. Add a space immediately after the end of the URL and insert `target=_blank`

This will make the link open in a **new window or tab**.
![image](https://github.com/user-attachments/assets/b495e4f1-4c5c-4594-bab7-59ba9eacdee4)

---

### Option 2 – HTML Component

Use this option if you want to create a **discrete "link component"** that behaves more like a button.

1. Add an **HTML component** to your form.
2. Set the **HTML Tag** to: `a`

3. Add the following attributes:
   - `href`: The URL you want the link to go to.
   - `target`: Set this to `_blank` to open in a new tab.

Example:

![image](https://github.com/user-attachments/assets/5f7fc4d5-59fa-4dee-b190-ee939a171279)


---

## 🎨 Styling Options

### Bootstrap Color Themes
Use any of the following:
- `primary`
- `secondary`
- `success`
- `danger`
- `warning`
- `info`
- `light`
- `dark`

### Bootstrap Sizes
- `sm`
- `md`
- `lg`

---

### 🧩 CSS Class Options
Example: 
Use CSS Class: `text-light` and Custom CSS Classes `btn btn-primary btn-lg` to make a link that looks like a button
![image](https://github.com/user-attachments/assets/02399598-e2e8-4c53-99c0-171872e9633e)

#### Applies to the content:
- Set text color: `text-[colorTheme]` (e.g., `text-primary`)
- Set hyperlink hover color: `link-[colorTheme]` (e.g., `link-warning`)

#### Applies to the Component:
- Make it look like a button: `btn`
- Style the button: `btn-[colorTheme]` (e.g., `btn-danger`)
- Add border: `border`
- Style border: `border-[colorTheme]`
- Size the button: `btn-[size]` (e.g., `btn-lg`)
- Add padding (all sides): `p-[size]` (e.g., `p-3`)
- Add padding to specific sides:
  - Top: `pt-[value]` (e.g., `pt-6`)
  - Left: `pl-[value]` (e.g., `pl-2`)
  - Right: `pr-[value]` (e.g., `pr-2`)
  - Bottom: `pb-[value]` (e.g., `pb-12`)

