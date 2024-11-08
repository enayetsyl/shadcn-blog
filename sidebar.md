# Building a Dynamic Sidebar with shadcn UI

The sidebar is a powerful navigation element, and shadcn UI offers a flexible, themeable, and customizable Sidebar component. In this post, we’ll dive into how to set up and customize a sidebar in your project, covering essential elements like SidebarProvider, collapsible menus, and integrating data fetching with React Query.

## Use Cases

A sidebar is ideal for applications requiring a persistent navigation area or additional content organization, such as:

- Dashboards with quick access to main pages
- CMS systems with nested content sections
- E-commerce admin panels with a collapsible menu for product categories

## Installation

To add the sidebar component, use the following command:

```bash
npx shadcn@latest add sidebar
```

This command installs the necessary files and dependencies. Make sure to add custom colors to your global CSS for theming.

## Sidebar Structure and Components

The sidebar in shadcn UI is built from multiple components, each serving a specific purpose. Let’s break down each part and how it contributes to the sidebar's functionality.

1. SidebarProvider

The SidebarProvider wraps your application to manage the sidebar’s state and context. Here’s how to set it up in layout.tsx:

```typescript
import { SidebarProvider, SidebarTrigger } from "@/components/ui/sidebar";
import { AppSidebar } from "@/components/app-sidebar";

export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <SidebarProvider>
      <AppSidebar />
      <main>
        <SidebarTrigger />
        {children}
      </main>
    </SidebarProvider>
  );
}
```

2. Sidebar

The main container for the sidebar, Sidebar manages its positioning, size, and style. Use the side, variant, and collapsible props for additional control:

```typescript
<Sidebar side="left" variant="sidebar" collapsible="offcanvas">
  <SidebarHeader />
  <SidebarContent>
    <SidebarGroup />
  </SidebarContent>
  <SidebarFooter />
</Sidebar>
```

- Side: Determines the sidebar’s position (left or right).
- Variant: sidebar for standard sidebars, floating for a detached look, and inset for overlay effects.
- Collapsible: Options like offcanvas (slides in/out), icon (collapses to icons), or none for a static sidebar.

3. Sidebar Trigger

The SidebarTrigger toggles the sidebar’s visibility. It can be customized to match your layout and is best placed in a header or main layout.

```typescript
<SidebarTrigger />
```

## Sidebar Components with Examples and Customizations

### Sidebar Header, Footer, and Content
- SidebarHeader: Place branding or a logo here.
- SidebarContent: The main area for navigation items, often scrollable.
- SidebarFooter: Add secondary actions like profile or settings.

```typescript
<Sidebar>
  <SidebarHeader>My App</SidebarHeader>
  <SidebarContent>
    <SidebarGroup />
  </SidebarContent>
  <SidebarFooter>Settings</SidebarFooter>
</Sidebar>
```

### Sidebar Group and Collapsible Sidebar Group

Group similar items in a SidebarGroup. To make it collapsible, wrap it in a Collapsible component.

```typescript
<SidebarContent>
  <SidebarGroup label="Main">
    <SidebarMenu />
  </SidebarGroup>
  
  <Collapsible defaultOpen>
    <SidebarGroup label="Settings">
      <SidebarMenu />
    </SidebarGroup>
  </Collapsible>
</SidebarContent>
```

### Sidebar Menu and Menu Components

- SidebarMenu: Contains individual items or nested menus.
- SidebarMenuItem: An item in the menu.
- SidebarMenuButton: A button inside the menu item, which can also render links or custom actions.

```typescript
<SidebarMenu>
  <SidebarMenuItem>
    <SidebarMenuButton asChild>
      <a href="#home">Home</a>
    </SidebarMenuButton>
  </SidebarMenuItem>
</SidebarMenu>
```

### Dropdown Menu and Submenus

The DropdownMenu is useful for additional actions within the sidebar. You can nest items using SidebarMenuSub.

```typescript
<SidebarMenuItem>
  <SidebarMenuButton>Actions</SidebarMenuButton>
  <DropdownMenu>
    <DropdownMenuTrigger asChild>
      <SidebarMenuAction>
        <MoreHorizontal />
      </SidebarMenuAction>
    </DropdownMenuTrigger>
    <DropdownMenuContent>
      <DropdownMenuItem>Edit</DropdownMenuItem>
      <DropdownMenuItem>Delete</DropdownMenuItem>
    </DropdownMenuContent>
  </DropdownMenu>
</SidebarMenuItem>
```

### Badges, Skeletons, and Separators

- SidebarMenuBadge: Adds a badge to items (e.g., notifications).
- SidebarMenuSkeleton: Placeholder for loading states, ideal for asynchronous data.
- SidebarSeparator: Visually divides sections within the sidebar.

```typescript
<SidebarMenuItem>
  <SidebarMenuButton>Notifications</SidebarMenuButton>
  <SidebarMenuBadge>5</SidebarMenuBadge>
</SidebarMenuItem>
<SidebarSeparator />
<SidebarMenuSkeleton />
```

## Data Fetching with React Query

Integrate React Query for dynamic content in the sidebar, such as a project list:

```typescript
import { useQuery } from "react-query";
import { SidebarMenu, SidebarMenuItem, SidebarMenuButton, SidebarMenuSkeleton } from "@/components/ui/sidebar";

function ProjectList() {
  const { data, isLoading } = useQuery("projects", fetchProjects);

  if (isLoading) {
    return <SidebarMenuSkeleton />;
  }

  return (
    <SidebarMenu>
      {data.map((project) => (
        <SidebarMenuItem key={project.id}>
          <SidebarMenuButton asChild>
            <a href={`/projects/${project.id}`}>{project.name}</a>
          </SidebarMenuButton>
        </SidebarMenuItem>
      ))}
    </SidebarMenu>
  );
}
```

## Conclusion

The Sidebar component in shadcn UI is highly flexible, allowing you to create structured, themeable sidebars for complex applications. With support for collapsible groups, dynamic data loading, and customizable styles, you can build a powerful navigation experience that’s both functional and visually appealing.

This blog covered the essential components and customization options for the sidebar. Start experimenting and create the sidebar that best fits your project’s needs!





