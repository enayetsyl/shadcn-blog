# Building a Navigation Menu with shadcn UI

A navigation menu is a crucial UI component that guides users through a website or application, helping them find content and perform actions efficiently. shadcn UI provides customizable components for creating a versatile navigation menu that suits any application or website. This guide walks you through setting up a navigation menu, customization options, and advanced features.

1. Overview
Navigation menus are fundamental in web design, offering a structured way for users to explore different sections of a site or app. They’re especially useful for:

- Multi-page Websites: Directing users to various categories, subcategories, or product pages.
- Single-page Applications: Allowing seamless transitions between sections without reloading.
- Dashboards: Organizing tools, settings, and data views for easy access.

2. Installation and Basic Setup

### CLI Installation

To install the navigation menu component in shadcn UI, use the CLI:

```bash
npx shadcn@latest add navigation-menu
```

This command sets up all necessary files and components for the navigation menu.

### Basic Structure

Import the core components for the navigation menu: NavigationMenu, NavigationMenuList, NavigationMenuItem, NavigationMenuTrigger, and NavigationMenuContent.

```typescript
import {
  NavigationMenu,
  NavigationMenuList,
  NavigationMenuItem,
  NavigationMenuTrigger,
  NavigationMenuContent,
  NavigationMenuLink,
  NavigationMenuIndicator,
  NavigationMenuViewport,
} from "@/components/ui/navigation-menu";
```

### Navigation Menu Structure:

- NavigationMenu: The main wrapper.
- NavigationMenuList: Holds the list of menu items.
- NavigationMenuItem: Defines an individual item within the list.
- NavigationMenuTrigger: The element that opens each dropdown or section.
- NavigationMenuContent: Wraps content within the dropdown or submenu.

### Example Setup:

```tsx
<NavigationMenu>
  <NavigationMenuList>
    <NavigationMenuItem>
      <NavigationMenuTrigger>Home</NavigationMenuTrigger>
      <NavigationMenuContent>Welcome to our site!</NavigationMenuContent>
    </NavigationMenuItem>
    <NavigationMenuItem>
      <NavigationMenuTrigger>About</NavigationMenuTrigger>
      <NavigationMenuContent>Learn more about us.</NavigationMenuContent>
    </NavigationMenuItem>
    <NavigationMenuItem>
      <NavigationMenuTrigger>Contact</NavigationMenuTrigger>
      <NavigationMenuContent>Get in touch with us.</NavigationMenuContent>
    </NavigationMenuItem>
  </NavigationMenuList>
</NavigationMenu>
```

3. Use Cases

- E-commerce Sites: Directing users to product categories, offers, and support pages.
- Portfolio Sites: Guiding visitors to work samples, about sections, and contact forms.
- Corporate Sites: Organizing services, about sections, and client testimonials.
- Application Dashboards: Arranging analytics, settings, and user profiles.

4. Explanation of Each Tag

- NavigationMenu: The container for the entire navigation structure.
- NavigationMenuList: Holds multiple NavigationMenuItem elements.
- NavigationMenuItem: Represents an individual menu option within the list.
- NavigationMenuTrigger: The button or link that opens a submenu or navigational section.
- NavigationMenuContent: Displays content for each menu item when selected.
- NavigationMenuLink: The anchor link for routing or navigating to different pages.
- NavigationMenuIndicator: A visual indicator showing the selected menu item.
- NavigationMenuViewport: Manages content that appears outside of the primary menu list.

5. Advanced Customizations

### Submenus

To add submenus, use nested NavigationMenuItem and NavigationMenuContent elements for multi-level navigation.

```tsx
<NavigationMenuItem>
  <NavigationMenuTrigger>Services</NavigationMenuTrigger>
  <NavigationMenuContent>
    <NavigationMenuItem>
      <NavigationMenuTrigger>Web Development</NavigationMenuTrigger>
      <NavigationMenuContent>Custom Websites</NavigationMenuContent>
    </NavigationMenuItem>
    <NavigationMenuItem>
      <NavigationMenuTrigger>SEO</NavigationMenuTrigger>
      <NavigationMenuContent>Search Engine Optimization</NavigationMenuContent>
    </NavigationMenuItem>
  </NavigationMenuContent>
</NavigationMenuItem>
```

### Client-side Routing
Use NavigationMenuLink to handle client-side routing.

```tsx
<NavigationMenuLink href="/services">Services</NavigationMenuLink>
```

### Indicators

The NavigationMenuIndicator shows the active or highlighted item, providing a visual cue to users.

```tsx
<NavigationMenu>
  <NavigationMenuIndicator />
  {/* Rest of the navigation menu */}
</NavigationMenu>
```

### Viewport for Content Display

NavigationMenuViewport is useful for showing content outside the main list area, such as popovers or previews.

```tsx
<NavigationMenuViewport>
  <div>More Info or Content Preview</div>
</NavigationMenuViewport>
```

6. Styling Options

### CSS Variables

Customize the menu’s appearance using CSS variables:

- --viewport-width and --viewport-height: Define dimensions for NavigationMenuViewport.
- --animation-duration: Adjusts transition duration for smooth animations.
- --indicator-color: Sets the color for NavigationMenuIndicator.

### Vertical and Flexible Layouts

Transform the layout to vertical by adjusting CSS, making it suitable for sidebar-style menus in dashboards or apps.

```css
.NavigationMenu {
  flex-direction: column;
}
```

### Adding Advanced Animations

Customize transitions with animations like fading, sliding, or scaling.

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
.NavigationMenuContent {
  animation: fadeIn 0.3s ease-in-out;
}
```

7. Comprehensive Example

Below is a complete example of a navigation menu with indicators, submenus, and client-side routing.

```tsx
<NavigationMenu>
  <NavigationMenuList>
    <NavigationMenuItem>
      <NavigationMenuTrigger>Home</NavigationMenuTrigger>
      <NavigationMenuContent>
        <NavigationMenuLink href="/">Welcome</NavigationMenuLink>
      </NavigationMenuContent>
    </NavigationMenuItem>
    
    <NavigationMenuItem>
      <NavigationMenuTrigger>Products</NavigationMenuTrigger>
      <NavigationMenuContent>
        <NavigationMenuItem>
          <NavigationMenuTrigger>Web Hosting</NavigationMenuTrigger>
          <NavigationMenuContent>
            <NavigationMenuLink href="/hosting">Learn More</NavigationMenuLink>
          </NavigationMenuContent>
        </NavigationMenuItem>
        <NavigationMenuItem>
          <NavigationMenuTrigger>Domain Registration</NavigationMenuTrigger>
          <NavigationMenuContent>
            <NavigationMenuLink href="/domains">Find Your Domain</NavigationMenuLink>
          </NavigationMenuContent>
        </NavigationMenuItem>
      </NavigationMenuContent>
    </NavigationMenuItem>

    <NavigationMenuItem>
      <NavigationMenuTrigger>Contact Us</NavigationMenuTrigger>
      <NavigationMenuContent>
        <NavigationMenuLink href="/contact">Get in Touch</NavigationMenuLink>
      </NavigationMenuContent>
    </NavigationMenuItem>

    <NavigationMenuIndicator />
  </NavigationMenuList>
  <NavigationMenuViewport>
    <div>Preview Content or Additional Info</div>
  </NavigationMenuViewport>
</NavigationMenu>
```

This example includes:

- A Home menu item with a simple content link.
- A Products menu item with a submenu, including links to Web Hosting and Domain Registration.
- A Contact Us menu item with a link to the contact page.
- Indicators and Viewport for additional styling and functionality.

## Conclusion

Creating a navigation menu with shadcn UI provides a seamless way to guide users across a site or app, with extensive customization options to match any design or user experience requirements. From submenus and flexible layouts to advanced animations and client-side routing, shadcn UI’s navigation components allow you to build a menu that’s both functional and visually engaging. Whether for a multi-page site or a single-page application, this navigation menu setup delivers a clear, structured path for users, enhancing usability and engagement.


