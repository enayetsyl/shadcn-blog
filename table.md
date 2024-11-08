# Building Interactive Data Tables with shadcn UI and TanStack Table

Data tables are essential for displaying and organizing structured information in web applications. The Data Table and Table components in shadcn UI offer accessible, customizable solutions for building tables with sorting, filtering, and pagination. In this post, we’ll explore the use cases, installation process, core tags, integration with TanStack Table, and a comprehensive example.

## Use Cases

Data tables are ideal for displaying large datasets in a structured, readable format. Here are some common use cases:

- Admin Dashboards: To list users, transactions, or analytics data.
- E-commerce: To display product lists with details like price, stock, and categories.
- Project Management: To manage tasks, projects, or time logs.
- Inventory Management: For showing product quantities, suppliers, and locations.

## Installation

Install the Data Table and Table components with the shadcn CLI:

```bash
npx shadcn@latest add data-table
npx shadcn@latest add table
```

These commands will add the necessary files and dependencies to your project.

## Basic Table Structure and Tags

The Table component in shadcn UI provides a simple, responsive structure for creating basic tables. Here’s a breakdown of the key tags:

- Table: The main table container.
- TableHeader: Wraps the header rows.
- TableRow: Defines a single row.
- TableCell: Defines an individual cell within a row.
- TableHead: Marks a cell as a header within a header row.
- TableBody: Wraps all table data rows.

### Basic Example

```typescript
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";

function BasicTable() {
  return (
    <Table>
      <TableHeader>
        <TableRow>
          <TableHead>Name</TableHead>
          <TableHead>Age</TableHead>
          <TableHead>Occupation</TableHead>
        </TableRow>
      </TableHeader>
      <TableBody>
        <TableRow>
          <TableCell>Jane Doe</TableCell>
          <TableCell>28</TableCell>
          <TableCell>Software Engineer</TableCell>
        </TableRow>
        <TableRow>
          <TableCell>John Smith</TableCell>
          <TableCell>34</TableCell>
          <TableCell>Product Manager</TableCell>
        </TableRow>
      </TableBody>
    </Table>
  );
}
```

This basic setup creates a simple table with three columns: Name, Age, and Occupation.

## Advanced Data Tables with TanStack Table

To implement advanced features like sorting, filtering, and pagination, shadcn UI can be combined with TanStack Table (formerly React Table). TanStack Table offers extensive table management tools, allowing you to customize the functionality and appearance of your tables.

### Integrating TanStack Table

First, install the TanStack Table dependency:

```bash
npm install @tanstack/react-table
```

### Setting Up TanStack Table with shadcn’s <Table />

In this example, we’ll create a table with sortable and filterable columns using TanStack Table and shadcn UI’s <Table /> component.

```typescript
import { useMemo } from "react";
import { useTable, useSortBy, useFilters } from "@tanstack/react-table";
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";

function DataTable() {
  // Sample data
  const data = useMemo(() => [
    { name: "Jane Doe", age: 28, occupation: "Software Engineer" },
    { name: "John Smith", age: 34, occupation: "Product Manager" },
    { name: "Alice Johnson", age: 30, occupation: "Designer" },
  ], []);

  // Define columns
  const columns = useMemo(() => [
    {
      Header: "Name",
      accessor: "name",
    },
    {
      Header: "Age",
      accessor: "age",
    },
    {
      Header: "Occupation",
      accessor: "occupation",
    },
  ], []);

  // Create table instance with sorting and filtering
  const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } = useTable({ columns, data }, useSortBy, useFilters);

  return (
    <Table {...getTableProps()}>
      <TableHeader>
        {headerGroups.map(headerGroup => (
          <TableRow {...headerGroup.getHeaderGroupProps()}>
            {headerGroup.headers.map(column => (
              <TableHead {...column.getHeaderProps(column.getSortByToggleProps())}>
                {column.render("Header")}
              </TableHead>
            ))}
          </TableRow>
        ))}
      </TableHeader>
      <TableBody {...getTableBodyProps()}>
        {rows.map(row => {
          prepareRow(row);
          return (
            <TableRow {...row.getRowProps()}>
              {row.cells.map(cell => (
                <TableCell {...cell.getCellProps()}>
                  {cell.render("Cell")}
                </TableCell>
              ))}
            </TableRow>
          );
        })}
      </TableBody>
    </Table>
  );
}
```

In this example:

- useTable: Creates the table instance, including sorting and filtering hooks.
- getTableProps and getTableBodyProps: Provide properties for the table and table body elements.
- headerGroups: Array of header rows, which allows us to map through each column header.
- rows: Array of row data, processed by TanStack Table.

### Customization Options

With TanStack Table, you can customize the table extensively.

- Sorting: Toggle sorting on headers by calling column.getSortByToggleProps().
- Filtering: Use column.getFilterProps() to add filtering inputs.
- Pagination: Implement pagination controls by managing page state and setting pageOptions.

### Comprehensive Example

Here’s an extended example integrating more features:

```typescript
import { useMemo } from "react";
import { useTable, useSortBy, useFilters, usePagination } from "@tanstack/react-table";
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";
import { Button } from "@/components/ui/button";

function PaginatedDataTable() {
  const data = useMemo(() => [
    // Sample data entries
  ], []);

  const columns = useMemo(() => [
    { Header: "Name", accessor: "name" },
    { Header: "Age", accessor: "age" },
    { Header: "Occupation", accessor: "occupation" },
  ], []);

  const {
    getTableProps,
    getTableBodyProps,
    headerGroups,
    page,
    prepareRow,
    canPreviousPage,
    canNextPage,
    nextPage,
    previousPage,
  } = useTable({ columns, data }, useSortBy, useFilters, usePagination);

  return (
    <>
      <Table {...getTableProps()}>
        <TableHeader>
          {headerGroups.map(headerGroup => (
            <TableRow {...headerGroup.getHeaderGroupProps()}>
              {headerGroup.headers.map(column => (
                <TableHead {...column.getHeaderProps(column.getSortByToggleProps())}>
                  {column.render("Header")}
                </TableHead>
              ))}
            </TableRow>
          ))}
        </TableHeader>
        <TableBody {...getTableBodyProps()}>
          {page.map(row => {
            prepareRow(row);
            return (
              <TableRow {...row.getRowProps()}>
                {row.cells.map(cell => (
                  <TableCell {...cell.getCellProps()}>
                    {cell.render("Cell")}
                  </TableCell>
                ))}
              </TableRow>
            );
          })}
        </TableBody>
      </Table>
      <div className="flex justify-between mt-2">
        <Button onClick={previousPage} disabled={!canPreviousPage}>
          Previous
        </Button>
        <Button onClick={nextPage} disabled={!canNextPage}>
          Next
        </Button>
      </div>
    </>
  );
}
```

In this example:

- Pagination: Added pagination with usePagination from TanStack Table. previousPage and nextPage functions manage navigation, while canPreviousPage and canNextPage determine button states.
- Button Integration: Uses shadcn UI’s <Button /> component for pagination controls.

## Conclusion

The Table and Data Table components in shadcn UI are powerful tools for displaying structured data. By integrating TanStack Table, you can expand functionality with sorting, filtering, and pagination to create fully interactive tables. Whether you need a basic or complex table, shadcn UI and TanStack Table make it easy to provide a clean, accessible, and dynamic experience. Start implementing data tables in your projects today and elevate your data presentation!






























