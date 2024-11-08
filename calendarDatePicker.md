# Adding Calendar and Date Picker to Your Application with shadcn UI

Calendars and date pickers are essential UI components for any application that handles date selection. Whether you're creating an appointment scheduler, booking system, or form with date inputs, shadcn UI’s Calendar and Date Picker components offer a simple and customizable solution. This post will walk you through their setup, use cases, customization options, and examples.

## Use Cases

- Calendar: Display monthly views, events, and reminders in applications like event schedulers, personal dashboards, or booking apps.
- Date Picker: Allow users to select single dates, date ranges, or predefined date options in forms or booking systems.

## Installation

Install the Calendar and Date Picker components with the following shadcn CLI commands:

```bash
npx shadcn@latest add calendar
npx shadcn@latest add date-picker
```

These commands will install the necessary files and dependencies.

## Calendar Component

The Calendar component displays a monthly view, making it perfect for apps that need to show events or scheduled activities.

### Tags Explanation and Basic Example

- Calendar: The main container for the calendar.
- CalendarMonth: Contains the grid for days in the selected month.
- CalendarDay: Displays individual day cells within the month grid.

```typescript
import { Calendar } from "@/components/ui/calendar";

<Calendar onSelect={(date) => console.log("Selected date:", date)} />
```

This basic setup displays a calendar and logs the selected date when a day is clicked.

### Customization Options

Customize the Calendar component by styling individual dates, showing event markers, or highlighting specific days. You can use custom CSS classes or Tailwind classes for styling.

```typescript
<Calendar
  className="border border-gray-200 shadow-md"
  onSelect={(date) => console.log("Date selected:", date)}
/>
```

For a more advanced setup, you can style weekends differently or add a tooltip for events on specific dates.

## Date Picker Component

The Date Picker allows users to select dates from a dropdown calendar. It’s ideal for form inputs where date selection is required.

### Simple Date Picker

```typescript
import { DatePicker } from "@/components/ui/date-picker";

<DatePicker onSelect={(date) => console.log("Selected date:", date)} />
```

This example provides a simple date picker input where users can select a date.

### Date Range Picker

Allow users to select a range of dates, suitable for applications like booking systems or trip planners.

```typescript
import { DateRangePicker } from "@/components/ui/date-picker";

<DateRangePicker onSelect={(range) => console.log("Selected range:", range)} />
```

### Date Picker with Presets

Offer quick selection presets (e.g., “Today,” “Last 7 Days”) to improve user experience.

```typescript
<DatePicker
  presets={[
    { label: "Today", value: new Date() },
    { label: "Last 7 Days", value: { start: new Date(Date.now() - 6 * 24 * 60 * 60 * 1000), end: new Date() } },
  ]}
  onSelect={(date) => console.log("Preset or date selected:", date)}
/>
```

### Date Picker in a Form

Integrate the Date Picker within a form, making it easy to gather date information as part of form submissions.

```typescript
import { useForm } from "react-hook-form";
import { DatePicker } from "@/components/ui/date-picker";

function BookingForm() {
  const { register, handleSubmit, setValue } = useForm();

  const onSubmit = (data) => console.log("Form submitted:", data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="startDate">Start Date</label>
      <DatePicker
        onSelect={(date) => setValue("startDate", date)}
      />
      <button type="submit">Book</button>
    </form>
  );
}
```

### Customization Options

You can customize both the Calendar and Date Picker to fit your app’s design requirements.

1. Custom Date Formats

Specify custom date formats for display in the Date Picker using JavaScript’s Intl.DateTimeFormat API or other date libraries.

```typescript
<DatePicker
  format={(date) => new Intl.DateTimeFormat("en-US", { month: "long", day: "2-digit", year: "numeric" }).format(date)}
/>
```

2. Highlight Specific Dates

Use conditional styling to highlight dates for special occasions, events, or holidays.

```typescript
<Calendar
  dayClassName={(date) => date.getDay() === 0 || date.getDay() === 6 ? "bg-blue-100" : ""}
/>
```

3. Customizable Colors and Styles

Apply custom classes to style the Calendar or Date Picker according to your app’s theme, adjusting colors, borders, and hover effects.

```typescript
<DatePicker className="bg-gray-100 border-gray-300 text-gray-800 rounded-lg shadow-md" />
```

### Comprehensive Example

Here’s an example of a date range picker with presets, customized styles, and integrated within a booking form.

```typescript
import { useForm } from "react-hook-form";
import { DateRangePicker, DatePicker } from "@/components/ui/date-picker";

function TravelBookingForm() {
  const { register, handleSubmit, setValue } = useForm();

  const onSubmit = (data) => console.log("Booking data:", data);

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="p-4 bg-gray-100 rounded-md">
      <h2 className="text-xl font-semibold mb-4">Travel Booking</h2>
      
      <label htmlFor="startDate" className="block text-sm mb-1">Start Date</label>
      <DatePicker
        onSelect={(date) => setValue("startDate", date)}
        className="mb-4"
      />

      <label htmlFor="endDate" className="block text-sm mb-1">End Date</label>
      <DateRangePicker
        onSelect={(range) => setValue("dateRange", range)}
        presets={[
          { label: "Next 7 Days", value: { start: new Date(), end: new Date(Date.now() + 7 * 24 * 60 * 60 * 1000) } },
          { label: "Next 30 Days", value: { start: new Date(), end: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000) } },
        ]}
      />

      <button type="submit" className="mt-4 bg-blue-500 text-white p-2 rounded-md">Book Now</button>
    </form>
  );
}
```

In this example:

- The Date Picker is used for selecting a single start date.
- The Date Range Picker allows users to select a range or use presets for quick selection.
- Custom styles are applied to fit the form’s design.

## Conclusion

The Calendar and Date Picker components in shadcn UI provide a streamlined way to manage date inputs in your application. Whether you’re building an event scheduler, booking form, or any interface requiring date selection, these components offer flexibility, customization, and ease of integration. Start implementing these components today to enhance your app’s date-handling capabilities and deliver a more intuitive user experience.




