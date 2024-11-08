# Implementing Tabs and Skeleton Components in shadcn UI

In any dynamic web application, Tabs provide an organized way to display multiple views, while Skeletons are ideal for loading placeholders. Together, they can enhance user experience by offering structured navigation and clear loading indicators. Let’s explore how to set up and customize both components in shadcn UI.

## Use Cases

- Tabs: Use tabs to organize content, such as different product categories, user settings, or data sections within a single page.
- Skeleton: Display skeletons as loading placeholders for images, text, or other content, offering visual feedback during data fetches.

## Installation

Install both components using the shadcn CLI:

```bash
npx shadcn@latest add tabs
npx shadcn@latest add skeleton
```

These commands will install the necessary components and dependencies for Tabs and Skeleton.

## Tabs Component

The Tabs component allows users to switch between different content panels with ease.

### Tag Explanation and Example

The primary tags for Tabs include:

- Tabs: The main container for the tab navigation.
- TabsList: Wraps the tab buttons, aligning them horizontally by default.
- TabsTrigger: Each trigger represents a tab button.
- TabsContent: Displays the content associated with each tab.

### Basic Example

Here’s a simple setup with two tabs:

```typescript
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";

<Tabs defaultValue="overview">
  <TabsList>
    <TabsTrigger value="overview">Overview</TabsTrigger>
    <TabsTrigger value="details">Details</TabsTrigger>
  </TabsList>
  <TabsContent value="overview">
    <p>This is the overview content.</p>
  </TabsContent>
  <TabsContent value="details">
    <p>This is the details content.</p>
  </TabsContent>
</Tabs>
```

This setup displays two tabs labeled "Overview" and "Details" with corresponding content sections.

### Customization

Customize tabs by modifying classes or adding icons to TabsTrigger for a more visually engaging design.

```typescript
<TabsList className="border-b">
  <TabsTrigger value="overview" className="px-4 py-2 text-blue-600">
    <span>Overview</span>
  </TabsTrigger>
  <TabsTrigger value="details" className="px-4 py-2 text-gray-600">
    <span>Details</span>
  </TabsTrigger>
</TabsList>
```

### Horizontal Scrolling

For mobile compatibility or when there are many tabs, add horizontal scrolling:

```typescript
<TabsList className="flex overflow-x-auto whitespace-nowrap">
  <TabsTrigger value="overview" className="px-4 py-2">
    Overview
  </TabsTrigger>
  <TabsTrigger value="details" className="px-4 py-2">
    Details
  </TabsTrigger>
  {/* Add more tabs as needed */}
</TabsList>
```

This setup enables horizontal scrolling, allowing users to swipe through tabs on smaller screens.

### Comprehensive Tabs Example

Here’s an example with multiple tabs, icons, and a scrollable list:

```typescript
<Tabs defaultValue="home">
  <TabsList className="flex overflow-x-auto border-b">
    <TabsTrigger value="home" className="px-4 py-2 flex items-center">
      <HomeIcon className="mr-2" /> Home
    </TabsTrigger>
    <TabsTrigger value="profile" className="px-4 py-2 flex items-center">
      <UserIcon className="mr-2" /> Profile
    </TabsTrigger>
    <TabsTrigger value="settings" className="px-4 py-2 flex items-center">
      <SettingsIcon className="mr-2" /> Settings
    </TabsTrigger>
  </TabsList>
  <TabsContent value="home">
    <p>Welcome to the home tab content.</p>
  </TabsContent>
  <TabsContent value="profile">
    <p>Your profile information goes here.</p>
  </TabsContent>
  <TabsContent value="settings">
    <p>Settings options will be displayed here.</p>
  </TabsContent>
</Tabs>
```

## Skeleton Component

The Skeleton component provides a placeholder effect, often used while data or images are loading.

### Tag Explanation and Example

- Skeleton: The main tag used to represent a loading element. Customize the dimensions to suit the content it will replace once loaded.

### Basic Example

Here’s a simple skeleton to simulate a loading state for a profile image:

```typescript
import { Skeleton } from "@/components/ui/skeleton";

<Skeleton className="w-16 h-16 rounded-full" />
```
This skeleton shows as a circular placeholder until the actual profile image is loaded.

### Customization

Customize the skeleton with various shapes and sizes. Here’s an example of a skeleton layout for a card:

```typescript
<div className="p-4 border rounded-lg">
  <Skeleton className="h-6 w-1/3 mb-2" />
  <Skeleton className="h-4 w-1/2 mb-2" />
  <Skeleton className="h-4 w-full mb-2" />
  <Skeleton className="h-4 w-2/3 mb-2" />
</div>
```

This layout simulates a card skeleton, giving the user a visual idea of the content while it loads.

### Comprehensive Skeleton Example

Here’s a more detailed example with multiple skeletons for a user profile page layout:

```typescript
<div className="p-4 max-w-md border rounded-lg">
  {/* Profile Image */}
  <Skeleton className="w-20 h-20 rounded-full mb-4" />

  {/* Profile Name */}
  <Skeleton className="h-6 w-3/5 mb-2" />

  {/* Profile Details */}
  <Skeleton className="h-4 w-full mb-1" />
  <Skeleton className="h-4 w-4/5 mb-1" />
  <Skeleton className="h-4 w-3/4 mb-1" />
</div>
```

This setup includes skeletons for a profile picture, name, and additional details, making it ideal for user profile pages.

## Conclusion

The Tabs and Skeleton components in shadcn UI provide essential UI elements for creating organized and responsive layouts. Use Tabs to improve navigation within a page and Skeletons to enhance loading experiences. By combining customization options and responsive designs, these components can greatly improve user engagement and usability in your web application.

Start experimenting with these components in your project to build interactive, user-friendly interfaces!




