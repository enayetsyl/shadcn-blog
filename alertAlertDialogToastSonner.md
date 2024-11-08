# Effective User Notifications with Alert, Alert Dialog, Toast, and Sonner in shadcn UI

Notifications are essential for guiding users, providing feedback, and confirming actions. The Alert, Alert Dialog, Toast, and Sonner components in shadcn UI offer flexible, accessible solutions for creating notifications and alerts in your application. This post will guide you through each component’s setup, use cases, customization options, and examples.

## Use Cases

- Alert: Display static, informational messages or warnings, like “Your account will expire soon.”
- Alert Dialog: Confirm critical actions, such as deletions or significant changes, where user acknowledgment is necessary.
- Toast: Show brief, non-blocking messages, like “Message sent” or “Saved successfully.”
- Sonner: Advanced toast notifications with additional features like stacking and animations.

## Installation

To add each component to your project, use the shadcn CLI commands:

```bash
npx shadcn@latest add alert
npx shadcn@latest add alert-dialog
npx shadcn@latest add toast
npx shadcn@latest add sonner
```

These commands will install the necessary files and dependencies for each notification component.

## Alert Component

The Alert component is ideal for conveying static messages, warnings, or information to the user.

### Tags Explanation and Basic Example

- Alert: The main container for the alert message.
- AlertTitle: Displays a prominent title within the alert.
- AlertDescription: Adds additional context or description.

```typescript
import { Alert, AlertTitle, AlertDescription } from "@/components/ui/alert";

<Alert>
  <AlertTitle>Warning</AlertTitle>
  <AlertDescription>Your subscription will expire soon.</AlertDescription>
</Alert>
```

### Customization Options

You can add custom colors and icons for different alert types, like success or error.

```typescript
<Alert className="bg-yellow-100 border border-yellow-300 text-yellow-700">
  <AlertTitle>Success</AlertTitle>
  <AlertDescription>Your profile has been updated successfully.</AlertDescription>
</Alert>
```

Add an icon for a more visually informative alert:

```typescript
<Alert>
  <AlertTitle className="flex items-center">
    <CheckCircleIcon className="mr-2 text-green-500" />
    Success
  </AlertTitle>
  <AlertDescription>Your data has been saved.</AlertDescription>
</Alert>
```

## Alert Dialog Component

The Alert Dialog is perfect for confirming critical user actions, such as deleting data.

### Tags Explanation and Basic Example

- AlertDialog: The main container for the dialog.
- AlertDialogTrigger: Button or element that opens the dialog.
- AlertDialogContent: Holds the content of the dialog.
- AlertDialogHeader: Displays the header section.
- AlertDialogTitle: Shows the title within the header.
- AlertDialogDescription: Adds a description in the header.
- AlertDialogFooter: Contains action buttons like confirm or cancel.

```typescript
import { AlertDialog, AlertDialogTrigger, AlertDialogContent, AlertDialogHeader, AlertDialogTitle, AlertDialogDescription, AlertDialogFooter } from "@/components/ui/alert-dialog";

<AlertDialog>
  <AlertDialogTrigger>Delete</AlertDialogTrigger>
  <AlertDialogContent>
    <AlertDialogHeader>
      <AlertDialogTitle>Are you sure?</AlertDialogTitle>
      <AlertDialogDescription>
        This action cannot be undone. This will permanently delete your data.
      </AlertDialogDescription>
    </AlertDialogHeader>
    <AlertDialogFooter>
      <button className="bg-red-500 text-white">Confirm</button>
      <button>Cancel</button>
    </AlertDialogFooter>
  </AlertDialogContent>
</AlertDialog>
```

### Customization Options

Style the dialog and add icons or custom text for different scenarios:

```typescript
<AlertDialogContent className="bg-red-50 border-red-400">
  <AlertDialogHeader>
    <AlertDialogTitle className="text-red-600">Delete Account</AlertDialogTitle>
    <AlertDialogDescription>
      <ExclamationIcon className="mr-2 text-red-600" />
      You are about to permanently delete your account.
    </AlertDialogDescription>
  </AlertDialogHeader>
</AlertDialogContent>
```

## Toast Component

The Toast component is used for brief notifications that don’t block the user’s workflow.

### Simple Toast

```typescript
import { Toast } from "@/components/ui/toast";

<Toast>Item added to cart.</Toast>
```

### Toast with Title

```typescript
import { Toast, ToastTitle } from "@/components/ui/toast";

<Toast>
  <ToastTitle>Success</ToastTitle>
  Your changes have been saved.
</Toast>
```

### Toast with Action

Include a button for user actions directly within the toast, such as undoing an action.

```typescript
<Toast>
  <ToastTitle>Action Needed</ToastTitle>
  <div>Your session will expire soon.</div>
  <button className="text-blue-500">Extend</button>
</Toast>
```

### Destructive Toast

Use destructive styling for warnings or errors.

```typescript
<Toast className="bg-red-500 text-white">
  <ToastTitle>Error</ToastTitle>
  Failed to save changes. Please try again.
</Toast>
```

### Customization Options

You can customize toast positioning, colors, and animation. For example, place the toast at the bottom of the screen:

```typescript
<Toast className="fixed bottom-4 left-1/2 transform -translate-x-1/2 bg-green-500 text-white">
  Item added to cart.
</Toast>
```

## Sonner Component

The Sonner component offers more advanced toast notifications, with additional features like stacking and animations.

### Basic Sonner Notification

```typescript
import { Sonner } from "@/components/ui/sonner";

<Sonner message="File uploaded successfully!" />
```

### Stacked Notifications

Add multiple Sonner notifications in a stack:

```typescript
<Sonner message="File uploaded successfully!" />
<Sonner message="Settings updated!" />
<Sonner message="Profile saved!" />
```

### Customization Options

Customize the appearance of Sonner notifications with animations and duration adjustments:

```typescript
<Sonner message="Changes saved!" animation="slide-up" duration={5000} className="bg-blue-600 text-white" />
```

## Comprehensive Example

Here’s a combined example with various alert types to showcase different scenarios:

```typescript
function Notifications() {
  return (
    <div>
      {/* Basic Alert */}
      <Alert>
        <AlertTitle>Info</AlertTitle>
        <AlertDescription>Your changes have been saved.</AlertDescription>
      </Alert>

      {/* Confirmation Dialog */}
      <AlertDialog>
        <AlertDialogTrigger>Delete Account</AlertDialogTrigger>
        <AlertDialogContent>
          <AlertDialogHeader>
            <AlertDialogTitle>Are you sure?</AlertDialogTitle>
            <AlertDialogDescription>
              Deleting your account is irreversible.
            </AlertDialogDescription>
          </AlertDialogHeader>
          <AlertDialogFooter>
            <button className="bg-red-500 text-white">Delete</button>
            <button>Cancel</button>
          </AlertDialogFooter>
        </AlertDialogContent>
      </AlertDialog>

      {/* Success Toast */}
      <Toast>
        <ToastTitle>Success</ToastTitle>
        Profile updated successfully.
      </Toast>

      {/* Sonner Notification */}
      <Sonner message="Settings have been saved!" animation="slide-up" />
    </div>
  );
}
```

## Conclusion

The Alert, Alert Dialog, Toast, and Sonner components in shadcn UI provide a wide range of options for displaying notifications and alerts. With flexibility for simple messages, critical confirmations, and advanced notifications, these components can help create a seamless, accessible, and user-friendly experience. Start using these components to improve user feedback and interaction in your application!

