# [FEAT-1235] Add product filter UI to the frontend

## Description

Backend filtering is available on `GET /api/products` via query parameters. Users need a frontend to drive those filters and see filtered results.

## Requirements

Build a product filter UI wired to the backend:

- **Price range controls**: Min and max price
- **Category selector**: Filter by category
- **Search field**: Keyword search on names and descriptions
- **Sort controls**: Sort by price or name
- **Filter actions**: Apply and clear filters

The UI must handle loading states, empty results, and validation errors.

## Acceptance criteria

- [ ] Price filter works and sends correct query parameters
- [ ] Category selection filters correctly
- [ ] Search field filters by keyword
- [ ] Sort options reorder results as expected
- [ ] Multiple filters work together
- [ ] Clearing filters shows all products again
- [ ] Validation errors are shown to users
- [ ] Empty state when no products match
- [ ] Loading state during filter operations
- [ ] All filter interactions logged to the console (structured JSON)

## Technical notes

- Extend the API client to accept filter parameters
- Build the query string from filter values
- Use React Hook Form and Zod for form validation
- Follow existing logging patterns (structured JSON)
- Prefer existing shadcn components where possible

## Definition of done

- All acceptance criteria met
- Backend called with correct query parameters
- Follows existing patterns and conventions
- Manual test checklist completed
