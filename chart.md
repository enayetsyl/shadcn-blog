# Visualizing Data with shadcn UI Charts: A Comprehensive Guide

Charts are essential for visualizing data in any application, providing insights at a glance. The Chart component in shadcn UI offers a powerful and customizable charting solution with support for grids, axes, tooltips, and legends. In this guide, we’ll walk through setting up a chart, configuring its appearance, and implementing advanced customizations.

## Use Cases

Charts are ideal for applications that need to display data in a visually meaningful way, such as:

- Dashboards: Show metrics and KPIs in real time.
- E-commerce: Display sales trends, conversion rates, and customer analytics.
- Finance: Visualize stock performance, portfolio breakdowns, or spending trends.
- Healthcare: Track patient metrics, medical statistics, and treatment outcomes.
- Education: Display student performance and progress in a class.


## Installation

To add the chart component, run the following command:

```bash
npx shadcn@latest add chart
```

This installs the required files and configurations for creating interactive charts.

## Basic Setup and Configuration

Once installed, you can begin setting up a chart with axes, grid, tooltips, and legends. Here’s how each feature works and how to configure it.

### Adding a Grid

A grid provides a visual structure, helping users to interpret data more easily. To add a grid, configure it in your chart setup:


```typescript
import { Chart, Grid } from "@/components/ui/chart";

<Chart>
  <Grid lines="horizontal" />
</Chart>
```

- Lines: Define grid lines as horizontal, vertical, or both for better visual guidance.

### Adding Axes

Axes label data points, making the chart readable and informative.

```typescript
import { Axis } from "@/components/ui/chart";

<Chart>
  <Axis type="x" label="Months" />
  <Axis type="y" label="Revenue ($)" />
</Chart>
```

- Type: Specify x or y axis to position it horizontally or vertically.
- Label: Label your axes to provide context to the data being visualized.

### Adding Tooltips

Tooltips display additional information when hovering over data points, enhancing the interactivity of the chart.

```typescript
import { Tooltip } from "@/components/ui/chart";

<Chart>
  <Tooltip content="Revenue for {x} month is {y}" />
</Chart>
```

- Content: Use placeholders like {x} and {y} to display dynamic values.
- Props: Customize tooltips with properties like backgroundColor, borderRadius, or padding to match your theme.

### Adding a Legend

Legends provide descriptions for the data series in a chart, aiding interpretation, especially with multiple data sets.

```typescript
import { Legend } from "@/components/ui/chart";

<Chart>
  <Legend position="top" align="center" />
</Chart>
```

- Position: Define legend position (top, bottom, left, right).
- Align: Control the alignment (center, start, end) for better layout management.

## Configuring the Chart

### Using CSS Variables

CSS variables provide a flexible way to manage colors, padding, and other styles consistently across components. Here’s an example setup

```typescript
:root {
  --chart-background: 0 0% 98%;
  --chart-accent: 220 70% 50%;
  --chart-axis-color: 0 0% 30%;
}

.dark {
  --chart-background: 220 15% 15%;
  --chart-accent: 220 80% 70%;
  --chart-axis-color: 0 0% 90%;
}
```

These variables can be applied in your chart components to maintain consistency:

```typescript
<Chart style={{ backgroundColor: "var(--chart-background)" }}>
  <Grid lines="both" color="var(--chart-axis-color)" />
</Chart>
```

### Using Hex, HSL, and OKLCH

With shadcn UI, you can use various color models to achieve unique looks.

- Hex: #ff5733 - Use traditional hex codes for colors.
- HSL: hsl(220, 70%, 50%) - Control hue, saturation, and lightness for nuanced colors.
- OKLCH: oklch(0.5 0.15 250) - A modern color space that provides better color accuracy and vibrancy.

Example:

```typescript
<Chart>
  <Grid color="hsl(220, 70%, 50%)" />
  <Axis color="oklch(0.5 0.15 250)" />
</Chart>
```

### Color Configuration

Setting consistent color schemes across the chart’s elements ensures that data is easily distinguishable.

```typescript
<Chart>
  <Axis color="var(--chart-axis-color)" />
  <Tooltip backgroundColor="var(--chart-accent)" />
  <Legend color="hsl(210, 20%, 50%)" />
</Chart>
```

## Customizing Tooltips and Legends

### Tooltip Properties

Tooltips can be customized with properties to make them more accessible and visually appealing:

```typescript
<Tooltip
  content="Value: {y}"
  backgroundColor="var(--chart-background)"
  borderColor="#ccc"
  borderRadius="4px"
  padding="8px"
/>
```

### Custom Tooltip

A custom tooltip allows you to display unique information. Here’s an example of a custom tooltip component:

```typescript
import { Tooltip } from "@/components/ui/chart";

function CustomTooltip({ x, y }) {
  return (
    <Tooltip>
      <div style={{ backgroundColor: "#fff", padding: "10px", borderRadius: "4px" }}>
        <strong>Month:</strong> {x} <br />
        <strong>Revenue:</strong> ${y}
      </div>
    </Tooltip>
  );
}
```

### Legend Colors and Custom Legends
Customize legend colors to improve clarity, especially when multiple series are present.

```typescript
<Legend color="var(--chart-accent)" />
```

For a custom legend, you can render items with icons, labels, and values:

```typescript
import { Legend } from "@/components/ui/chart";

function CustomLegend({ series }) {
  return (
    <Legend>
      {series.map((item) => (
        <div key={item.name} style={{ color: item.color }}>
          <span style={{ marginRight: "8px" }}>{item.icon}</span>
          {item.name}: {item.value}
        </div>
      ))}
    </Legend>
  );
}
```

## Comprehensive Example

Below is a complete example that combines all the discussed features into a single, functional chart.

```typescript
import {
  Chart,
  Grid,
  Axis,
  Tooltip,
  Legend,
} from "@/components/ui/chart";

const data = [
  { month: "Jan", revenue: 1200 },
  { month: "Feb", revenue: 2100 },
  { month: "Mar", revenue: 800 },
  // Add more data points as needed
];

export default function RevenueChart() {
  return (
    <Chart style={{ backgroundColor: "var(--chart-background)" }}>
      <Grid lines="both" color="var(--chart-axis-color)" />
      <Axis type="x" label="Months" color="var(--chart-axis-color)" />
      <Axis type="y" label="Revenue ($)" color="var(--chart-axis-color)" />

      <Tooltip content="Revenue for {x} is ${y}" backgroundColor="hsl(220, 70%, 95%)" />

      <Legend position="top" align="center" color="var(--chart-accent)" />

      {data.map((point) => (
        <Tooltip key={point.month} content={`Revenue: ${point.revenue}`} />
      ))}
    </Chart>
  );
}
```

This example includes a grid, axes, tooltips, and a legend, making it a comprehensive solution for most data visualization needs.

## Conclusion

The Chart component in shadcn UI is a versatile tool for adding data visualization to your application. With options for grids, axes, tooltips, legends, and color schemes, you can create charts that are both informative and visually appealing. Start experimenting with colors, tooltips, and legends to customize your charts, and create a data-rich experience for your users.