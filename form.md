# Building Robust Forms in shadcn UI with React Hook Form

Forms are the backbone of data collection in web applications, and shadcn UI provides an intuitive way to build accessible, visually consistent forms. In this post, we’ll explore use cases for forms, set up a form with React Hook Form for state management, and build a comprehensive form using various components such as checkboxes, date pickers, and more.

## Use Cases for Forms

Forms are essential for:

- User Registration and Login: To collect and authenticate user credentials.
- Order and Checkout Forms: For e-commerce applications to gather billing, shipping, and payment details.
- Surveys and Feedback: To collect user feedback, preferences, and data.
- Admin Dashboards: For managing and editing data, such as user profiles and product details.

## Installation

First, install the form and required components using the shadcn CLI:

```bash
npx shadcn@latest add form
npx shadcn@latest add input checkbox date-picker radio-group select switch textarea combobox
```

This command installs the core form structure and various input elements used in complex forms.

## Setting Up a Form with React Hook Form

Using React Hook Form with shadcn UI streamlines form validation and state management, making it easier to handle user input efficiently.

### Basic Form Setup

- Install React Hook Form:

```bash
npm install react-hook-form
```

- Set Up the Form:

```typescript
import { useForm, SubmitHandler } from "react-hook-form";
import { Input, Label, Button } from "@/components/ui";

type FormData = {
  name: string;
  email: string;
};

export default function SimpleForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>();
  const onSubmit: SubmitHandler<FormData> = data => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Label htmlFor="name">Name</Label>
      <Input id="name" {...register("name", { required: "Name is required" })} />
      {errors.name && <p>{errors.name.message}</p>}

      <Label htmlFor="email">Email</Label>
      <Input id="email" {...register("email", { required: "Email is required" })} />
      {errors.email && <p>{errors.email.message}</p>}

      <Button type="submit">Submit</Button>
    </form>
  );
}
```

### Explanation

- useForm: Initializes form handling, providing methods like register and handleSubmit.
- register: Binds input elements to form state and validation rules.
- handleSubmit: Handles form submission, invoking the onSubmit function if validation passes.
- errors: Displays validation errors if inputs don’t meet specified criteria.

## Building a Comprehensive Form

Now, let's create a more complex form using various input types available in shadcn UI.

### Comprehensive Form Example

```typescript
import { useForm, SubmitHandler } from "react-hook-form";
import { Input, Checkbox, DatePicker, RadioGroup, Select, Switch, Textarea, Combobox, Label, Button } from "@/components/ui";

type FormData = {
  username: string;
  email: string;
  agreeToTerms: boolean;
  birthdate: Date;
  gender: string;
  country: string;
  notifications: boolean;
  bio: string;
  skills: string[];
};

export default function ComprehensiveForm() {
  const { register, handleSubmit, control, formState: { errors } } = useForm<FormData>();
  const onSubmit: SubmitHandler<FormData> = data => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      
      <Label htmlFor="username">Username</Label>
      <Input id="username" {...register("username", { required: "Username is required" })} />
      {errors.username && <p>{errors.username.message}</p>}

      <Label htmlFor="email">Email</Label>
      <Input id="email" {...register("email", { required: "Email is required" })} />
      {errors.email && <p>{errors.email.message}</p>}

      <Checkbox {...register("agreeToTerms")} />
      <Label htmlFor="agreeToTerms">Agree to Terms and Conditions</Label>

      <Label htmlFor="birthdate">Birthdate</Label>
      <DatePicker control={control} name="birthdate" />

      <Label>Gender</Label>
      <RadioGroup {...register("gender")}>
        <RadioGroup.Item value="male" label="Male" />
        <RadioGroup.Item value="female" label="Female" />
      </RadioGroup>

      <Label>Country</Label>
      <Select {...register("country")}>
        <option value="USA">United States</option>
        <option value="CA">Canada</option>
      </Select>

      <Label>Receive Notifications</Label>
      <Switch {...register("notifications")} />

      <Label htmlFor="bio">Bio</Label>
      <Textarea id="bio" {...register("bio")} placeholder="Tell us about yourself" />

      <Label htmlFor="skills">Skills</Label>
      <Combobox id="skills" {...register("skills")} placeholder="Select skills" options={["JavaScript", "React", "CSS"]} multiple />

      <Button type="submit">Submit</Button>
    </form>
  );
}
```

### Explanation of Key Components

- Checkbox: Used for consent or agreement toggles. Here, it’s tied to agreeToTerms.
- DatePicker: Allows date selection, such as birthdate. Integrated using control from React Hook Form.
- RadioGroup: Defines mutually exclusive options. Here, it’s used to select gender.
- Select: Creates a dropdown, suitable for country or region selection.
- Switch: Toggles binary options, like receiving notifications.
- Textarea: Allows multi-line input for larger text fields.
- Combobox: Creates a searchable dropdown with multi-select support, ideal for skill selection.

## Conclusion

Using shadcn UI components with React Hook Form makes building complex, accessible forms easy. By combining shadcn’s UI components and React Hook Form’s validation, you can build interactive forms that collect a wide range of data efficiently. Try integrating these components in your project to enhance user experience in data collection.


















