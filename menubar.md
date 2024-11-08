# Creating a Menubar with shadcn UI

A menubar is an organized, persistent navigation tool, often seen in desktop-style applications where commands are grouped logically across menus. With shadcn UI, you can implement an accessible, customizable menubar, enhancing user interaction for complex applications. This guide covers everything from basic setup to advanced customization options, keyboard accessibility, and example implementations.

1. Overview

A menubar serves as a horizontal toolbar where users can access actions and options across multiple menus. This style of navigation is most effective for:

- Desktop-style Applications: Organize commands logically for productivity apps.
- Web Apps with Multiple Actions: Provide users with a clear structure for complex interactions.

2. Installation and Basic Setup

### CLI Installation

To install the menubar component in shadcn UI, use the CLI:

```bash
npx shadcn@latest add menubar
```

This command sets up the necessary files and components for the menubar.

### Basic Structure

Import the key components for creating a menubar: Menubar, MenubarMenu, MenubarTrigger, and MenubarContent.

```typescript
import {
  Menubar,
  MenubarMenu,
  MenubarTrigger,
  MenubarContent,
  MenubarItem,
  MenubarSeparator,
  MenubarCheckboxItem,
  MenubarRadioGroup,
  MenubarRadioItem,
  MenubarLabel,
  MenubarSub,
  MenubarSubTrigger,
  MenubarSubContent,
} from "@/components/ui/menubar";
```

### Menubar Structure:

1. Menubar: The main container for the menubar.
2. MenubarMenu: Wraps a single dropdown menu within the menubar.
3. MenubarTrigger: The button or trigger that opens each menu.
4. MenubarContent: Holds the menu items for each dropdown.

### Example Setup:

```tsx
<Menubar>
  <MenubarMenu>
    <MenubarTrigger>File</MenubarTrigger>
    <MenubarContent>
      <MenubarItem>New</MenubarItem>
      <MenubarItem>Open</MenubarItem>
      <MenubarSeparator />
      <MenubarItem>Exit</MenubarItem>
    </MenubarContent>
  </MenubarMenu>
</Menubar>
```

3. Difference in Themes: Default vs. New York

shadcn UI provides themes to style components. Here’s how the Default and New York themes differ for the menubar:

- Default Theme: Minimalistic styling, suited for modern applications with basic color schemes.
- New York Theme: Adds a touch of sophistication with refined spacing, shadows, and typography, providing a more polished, professional look.

You can switch themes or modify them to suit your design needs.

4. Functionality of Each Tag

- Menubar: The container for all menubar menus.
- MenubarMenu: Defines individual menus within the menubar, each opened by a MenubarTrigger.
- MenubarTrigger: The clickable trigger that opens the associated menu.
- MenubarContent: Contains the list of menu items within a menu.
- MenubarItem: An interactive item within the menu.
- MenubarSeparator: Visually separates items for logical grouping.
- MenubarCheckboxItem: Allows for multiple selections within a menu.
- MenubarRadioGroup: Groups multiple radio items to allow a single selection.
- MenubarRadioItem: A selectable item within a MenubarRadioGroup.
- MenubarLabel: Provides a label or heading within a menu.
- MenubarSub, MenubarSubTrigger, and MenubarSubContent: For creating submenus within a main menu.
- MenubarItemIndicator: Shows a visual indicator for selected items (e.g., checkmarks).

5. Advanced Options and Customization

### Submenus

Add submenus for nested options.

```tsx
<MenubarSub>
  <MenubarSubTrigger>More Options</MenubarSubTrigger>
  <MenubarSubContent>
    <MenubarItem>Save As...</MenubarItem>
    <MenubarItem>Export</MenubarItem>
  </MenubarSubContent>
</MenubarSub>
```

### Checkbox and Radio Groups

Enable users to toggle settings or select single options.

### Checkbox Example:

```tsx
<MenubarCheckboxItem checked={true}>Show Rulers</MenubarCheckboxItem>
```

### Radio Group Example

```tsx
<MenubarRadioGroup>
  <MenubarRadioItem value="light">Light Mode</MenubarRadioItem>
  <MenubarRadioItem value="dark">Dark Mode</MenubarRadioItem>
</MenubarRadioGroup>
```

### Alignment and Spacing

CSS variables are available for precise control over alignment, padding, and other spacing adjustments:

- --menubar-item-spacing: Adjusts spacing between items.
- --menubar-content-padding: Sets padding within the content area.

### Keyboard Navigation and Accessibility

The menubar supports full keyboard navigation and typeahead functionality:

- Arrow Keys: Navigate between menu items.
- Enter/Space: Activate the selected item.
- Esc: Closes the open menu.

6. Use Cases for Menubar on a Website

- Web Applications: Organize commands for document editing, design tools, or email clients.
- E-commerce Sites: Categorize product options (e.g., Men’s, Women’s, Kids) for streamlined navigation.
- Admin Dashboards: Quickly access settings, user management, and reports.

7. Key API Props with Examples

- Trigger: The interactive element to open the menu.

```tsx
<MenubarTrigger>Actions</MenubarTrigger>
```

- Content: Wraps items inside the dropdown.

```tsx
<MenubarContent>
  <MenubarItem>Settings</MenubarItem>
</MenubarContent>
```

- Arrow: An optional arrow to visually link the trigger with content.

```tsx
<MenubarContent sideOffset={5}>
  <MenubarArrow />
  <MenubarItem>Preferences</MenubarItem>
</MenubarContent>
```

- Item: Represents a selectable option.

```tsx
<MenubarItem>Open</MenubarItem>
```

- Group: Group items for better organization.

```tsx
<MenubarGroup>
  <MenubarItem>Cut</MenubarItem>
  <MenubarItem>Copy</MenubarItem>
</MenubarGroup>
```

- Checkbox Item: Adds a checkbox for toggling options.

```tsx
<MenubarCheckboxItem checked={true}>Show Toolbar</MenubarCheckboxItem>
```

- Label: Provides a heading within a menu.

```tsx
<MenubarLabel>View</MenubarLabel>
```

- Radio Group and Radio Item: Single-choice options.

```tsx
<MenubarRadioGroup>
  <MenubarRadioItem value="grid">Grid View</MenubarRadioItem>
  <MenubarRadioItem value="list">List View</MenubarRadioItem>
</MenubarRadioGroup>
```

- Item Indicator: Shows a check or other indicator for selected items.

```tsx
<MenubarItemIndicator>✔</MenubarItemIndicator>
```

- Separator: Divides items.

```tsx
<MenubarSeparator />
```

- Sub: Creates nested submenus.

```tsx
<MenubarSub>
  <MenubarSubTrigger>Advanced</MenubarSubTrigger>
  <MenubarSubContent>
    <MenubarItem>Backup Settings</MenubarItem>
  </MenubarSubContent>
</MenubarSub>
```

- Disable Items: Prevent user interaction.

```tsx
<MenubarItem disabled>Disabled Item</MenubarItem>
```

### Available Animations

You can apply animations to enhance user experience, such as sliding in and out for menus. Customize animations by setting CSS transitions on MenubarContent.

8. Comprehensive Example

Below is a complete example with multiple menus, items, and custom elements.

```tsx
<Menubar>
  <MenubarMenu>
    <MenubarTrigger>File</MenubarTrigger>
    <MenubarContent>
      <MenubarItem>New</MenubarItem>
      <MenubarItem>Open</MenubarItem>
      <MenubarSeparator />
      <MenubarCheckboxItem checked={true}>Enable Autosave</MenubarCheckboxItem>
      <MenubarSeparator />
      <MenubarItem>Exit</MenubarItem>
    </MenubarContent>
  </MenubarMenu>
  
  <MenubarMenu>
    <MenubarTrigger>Edit</MenubarTrigger>
    <MenubarContent>
      <MenubarItem>Undo</MenubarItem>
      <MenubarItem>Redo</MenubarItem>
      <MenubarSeparator />
      <MenubarGroup>
        <MenubarItem>Cut</MenubarItem>
        <MenubarItem>Copy</MenubarItem>
        <MenubarItem>Paste</MenubarItem>
      </MenubarGroup>
    </MenubarContent>
  </MenubarMenu>
  
  <MenubarMenu>
    <MenubarTrigger>View</MenubarTrigger>
    <MenubarContent>
      <MenubarCheckboxItem checked={false}>Show Toolbar</MenubarCheckboxItem>
      <MenubarCheckboxItem checked={true}>Show Rulers</MenubarCheckboxItem>
      <MenubarSeparator />
      <MenubarRadioGroup>
        <MenubarRadioItem value="grid">Grid View</MenubarRadioItem>
        <MenubarRadioItem value="list">List View</MenubarRadioItem>
      </MenubarRadioGroup>
      <MenubarSeparator />
      <MenubarSub>
        <MenubarSubTrigger>Zoom</MenubarSubTrigger>
        <MenubarSubContent>
          <MenubarItem>Zoom In</MenubarItem>
          <MenubarItem>Zoom Out</MenubarItem>
          <MenubarItem>Reset Zoom</MenubarItem>
        </MenubarSubContent>
      </MenubarSub>
    </MenubarContent>
  </MenubarMenu>
</Menubar>
```

This comprehensive example includes several common menu items and configurations:

- The File menu contains basic actions with separators and a checkbox item.
- The Edit menu includes grouped items for Cut, Copy, and Paste.
- The View menu includes checkboxes, a radio group for switching views, and a submenu for zoom options.

This setup allows users to interact with and customize their view in a structured, organized manner, similar to desktop applications.

## Conclusion

Creating a menubar with shadcn UI allows for a highly customizable, accessible, and visually appealing navigation experience, ideal for desktop-style and web applications with complex actions. With features like checkboxes, radio groups, separators, and nested submenus, the menubar component is flexible enough to support diverse use cases. Additionally, themes and CSS variables enable fine-tuning for seamless integration into any design system.

By leveraging shadcn UI’s menubar, developers can build intuitive, organized interfaces that enhance user productivity and satisfaction. Whether you’re developing a web-based editor, admin panel, or sophisticated e-commerce site, the menubar offers a polished, efficient way to structure actions and options for users.
















