# Theming in shadcn UI: Customizing Your Design with CSS Variables

Welcome to our fourth blog in the shadcn UI series! In this post, we’ll explore the theming options available in shadcn UI, focusing on how to use CSS variables to create dynamic, easily customizable themes. Let’s dive into the configuration options and see how they can be applied to build both light and dark themes.

## Choosing a Theming Method

shadcn UI offers two methods for theming: CSS Variables and Tailwind CSS utility classes.

- CSS Variables: This approach makes your theme flexible, allowing for quick, global updates to color schemes and other style properties. If you enable CSS variables in components.json, you can change themes without modifying individual components.
- Utility Classes: For a more static setup, you can use Tailwind utility classes directly within components. This method requires setting cssVariables to false.


## Example: Setting Up CSS Variables
To enable CSS variables, set cssVariables to true in your components.json file:

```json
"tailwind": {
  "cssVariables": true
}
```

With CSS variables enabled, you can now use global variables to control your component styles:

```html
<div class="bg-background text-foreground">
  Welcome to shadcn UI
</div>
```

## CSS Variables for Theming

Using CSS variables, you can customize colors, borders, and more. Below is a list of variables you can set, with examples of how each might be used.

1. --background and --foreground
- Purpose: Defines the default background and text colors across components.
- Example Use Cases:
  - Light Theme: --background: 0 0% 100%; (white), --foreground: 222.2 47.4% 11.2%; (dark text)
  - Dark Theme: --background: 222.2 47.4% 11.2%; (dark), --foreground: 210 40% 98%; (light text)

2. --muted and --muted-foreground
- Purpose: Used for muted backgrounds and text, suitable for components like TabsList, Skeleton, and Switch.
- Example Use Cases:
  - Info Cards: Use --muted for the background of informational cards to provide a soft, unobtrusive color.
  - Disabled Buttons: Set buttons in a disabled state with --muted-foreground to indicate inactivity without complete invisibility.

3. --card and --card-foreground
- Purpose: Sets the color scheme for card components.
- Example Use Cases:
  - Product Cards: Apply --card to product card backgrounds for a clean and consistent look.
  - Profile Cards: Use --card-foreground for text on user profile cards to maintain readability.

4. --popover and --popover-foreground
- Purpose: Specifies colors for popovers, such as dropdown menus and tooltips.
- Example Use Cases:
  - Dropdown Menus: Set --popover for dropdown menus to match the theme, ensuring they stand out without clashing.
  - Hover Tooltips: Use --popover-foreground to set readable text colors in tooltips.

5. --border
- Purpose: Defines the default border color for elements.
- Example Use Cases:
  - Input Borders: Apply --border to input fields for a subtle boundary without overpowering the design.
  - Dividers: Use as the color for dividing lines in components like lists or card sections.

6. --input
- Purpose: Sets the border color for inputs, selects, and textareas.
- Example Use Cases:
  - Form Fields: Use --input to color the borders of input fields, creating a cohesive form design.
  - Dropdown Borders: Apply --input to dropdown components to align with the form field styles.

7. --primary and --primary-foreground
- Purpose: Sets the primary color and its text color, typically used for buttons.
- Example Use Cases:
  - Primary Action Buttons: Use --primary for call-to-action buttons to make them prominent.
  - Highlights: Apply --primary-foreground for any text that needs emphasis, ensuring readability on the primary color.

8. --secondary and --secondary-foreground
- Purpose: Secondary colors, often used for buttons with secondary importance.
- Example Use Cases:
  - Secondary Buttons: Use --secondary for secondary action buttons that complement the primary button.
  - Secondary Accents: Apply --secondary-foreground for text on secondary background elements.

9. --accent and --accent-foreground
- Purpose: Accent colors, generally used for hover effects and selected items.
- Example Use Cases:
  - Hover States: Set --accent for hover effects on menu items to provide feedback.
  - Selected Items: Use --accent-foreground for text in selected dropdown items.

10.  --destructive and --destructive-foreground
- Purpose: Colors for destructive actions, like delete buttons.
- Example Use Cases:
  - Delete Buttons: Apply --destructive to indicate a potentially irreversible action.
  - Error Messages: Use --destructive-foreground for text in error messages to draw attention.

11.  --ring
- Purpose: Sets the color for focus rings, typically used to indicate active or focused states.
- Example Use Cases:
  - Input Focus: Apply --ring on inputs to show focus clearly.
  - Button Focus: Use for focus states on interactive elements, ensuring accessibility and visibility.

12.  --radius
- Purpose: Defines the border radius for components, making corners rounded or sharp.
- Example Use Cases:
  - Rounded Cards: Set --radius to 0.5rem for soft, rounded corners on card components.
  - Sharp Buttons: Use --radius: 0; for buttons to give them a more defined, sharp look.


## Adding New CSS Variables

If you want to add additional colors to your theme, define them in your CSS file and update your tailwind.config.js file accordingly:

```css
:root {
  --warning: 38 92% 50%;
  --warning-foreground: 48 96% 89%;
}
```
Then, add them to tailwind.config.js:

```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        warning: "hsl(var(--warning))",
        "warning-foreground": "hsl(var(--warning-foreground))",
      },
    },
  },
}
```

With this configuration, you can use these new variables in your components like so:

```html
<div class="bg-warning text-warning-foreground">
  Warning: Changes cannot be undone!
</div>
```

## Wrapping Up

Using CSS variables in shadcn UI gives you powerful theming flexibility. With variables like --primary, --secondary, --background, and more, you can maintain a consistent design while easily switching themes and colors. This setup also keeps your code DRY, allowing for quick and global changes.

In the next blog, we’ll dive into Dark Mode and explore how you can implement theme switching with minimal setup. Stay tuned!