# Implementing Pagination in shadcn UI: A Complete Guide

Pagination is an essential feature for displaying large datasets in a manageable format. With shadcn UI, implementing pagination is straightforward and efficient. In this post, we’ll explore common use cases, set up pagination, understand key tags, and address a notable exception for Next.js.

## Use Cases for Pagination

Pagination improves user experience by breaking down large datasets, allowing users to navigate content in segments rather than loading everything at once. Some common use cases include:

- Product Listings: In e-commerce platforms, pagination organizes product displays.
- Blog Archives: Paginating blog posts lets users browse older entries without overwhelming the page.
- User Management: Admin dashboards benefit from paginated user lists for easier data management.
- Search Results: Pagination enables manageable, ordered search results, reducing page load time.

## Installation

To add pagination to your project, use the following shadcn CLI command:

```bash
npx shadcn@latest add pagination
```

This installs the core pagination component and dependencies in your project.

## Pagination Tags and Structure

The pagination component is composed of several key tags that help create navigable, interactive page controls. Here’s a breakdown of each:

- Pagination: The main container, which holds all pagination elements.
- PaginationButton: Renders individual page buttons.
- PaginationNext and PaginationPrevious: Special buttons for navigating to the next or previous page.
- PaginationEllipsis: Adds ellipses to indicate truncated sections, useful for long pagination ranges.

### Example Setup

Here’s a basic example of a pagination setup:

```typescript
import { Pagination, PaginationButton, PaginationNext, PaginationPrevious, PaginationEllipsis } from "@/components/ui/pagination";

function BasicPagination() {
  return (
    <Pagination>
      <PaginationPrevious>Previous</PaginationPrevious>
      <PaginationButton page={1} />
      <PaginationButton page={2} />
      <PaginationButton page={3} />
      <PaginationEllipsis />
      <PaginationButton page={10} />
      <PaginationNext>Next</PaginationNext>
    </Pagination>
  );
}
```

In this example:

- PaginationPrevious and PaginationNext handle navigation between pages.
- PaginationButton accepts a page prop to define page numbers.
- PaginationEllipsis indicates a gap in page numbers when there are many pages, keeping the display concise.
  
## Advanced Pagination with Dynamic Data

To make pagination more dynamic, you can integrate it with a backend or API to fetch data based on the current page. Here’s an example using state to handle current page selection and a mock data fetch:

```typescript
import { useState } from "react";
import { Pagination, PaginationButton, PaginationNext, PaginationPrevious, PaginationEllipsis } from "@/components/ui/pagination";

function DynamicPagination() {
  const [currentPage, setCurrentPage] = useState(1);
  const totalPages = 20;

  const handlePageChange = (page: number) => {
    setCurrentPage(page);
    // Call your data-fetching function here, e.g., fetchPageData(page);
  };

  return (
    <Pagination>
      <PaginationPrevious onClick={() => handlePageChange(currentPage - 1)} disabled={currentPage === 1}>Previous</PaginationPrevious>
      
      {[...Array(totalPages).keys()].map(page => (
        <PaginationButton
          key={page + 1}
          page={page + 1}
          active={currentPage === page + 1}
          onClick={() => handlePageChange(page + 1)}
        />
      ))}

      <PaginationNext onClick={() => handlePageChange(currentPage + 1)} disabled={currentPage === totalPages}>Next</PaginationNext>
    </Pagination>
  );
}
```

In this setup:

- Pagination State: The currentPage state controls the active page.
- Dynamic Page Buttons: Generates page buttons dynamically based on the total page count.
- Data Fetching: Call a data-fetching function (e.g., fetchPageData(page)) to retrieve content based on the selected page.

## Next.js Exception

In Next.js, when handling pagination, server-side rendering (SSR) may pose a challenge for dynamic data loading. Next.js’s SSR does not natively support client-side state changes (such as pagination) out of the box in the same way that single-page applications (SPAs) do.

### Solutions for Next.js

- Client-Side Pagination: If the data is fully available on the client side, handle pagination directly in the component using client-side state management (e.g., useState).

- Server-Side Pagination: Fetch only a limited number of items based on the current page via getServerSideProps or getStaticProps. Use query parameters (?page=1) to determine the current page and adjust the server-side fetch accordingly:

```typescript
export async function getServerSideProps(context) {
  const page = context.query.page || 1;
  const res = await fetch(`https://api.example.com/items?page=${page}`);
  const data = await res.json();

  return {
    props: {
      items: data.items,
      totalPages: data.totalPages,
    },
  };
}
```

- Client-Side Navigation with Server Data: Combine SSR with client-side pagination by pre-fetching a few pages and switching between them without needing a server request for every interaction.

## Conclusion

The Pagination component in shadcn UI provides a robust, flexible approach to data navigation. By integrating this component with state management or dynamic data-fetching functions, you can create responsive, user-friendly paginated displays. Be mindful of SSR limitations in Next.js, and adapt your pagination strategy accordingly for the best results.

This setup will enhance user experience by breaking large datasets into manageable sections, allowing users to navigate through content easily.











