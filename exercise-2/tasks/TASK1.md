# [FEAT-1234] Add product filtering to the Catalog API

## Description

Users must be able to filter and search products in the catalog API. Today, `GET /api/products` returns all 30 products with no filtering.

## Requirements

Add filtering and search to `GET /api/products`:

- **Price filtering**: Min and max price query parameters
- **Category filtering**: Filter by product category
- **Keyword search**: Search in product names and descriptions
- **Sorting**: Sort by price or name (ascending and descending)

All filters must be optional and work when combined.

## Acceptance criteria

- [ ] All filter-related tests pass
- [ ] Invalid input returns correct HTTP 400 responses
- [ ] Backward compatible (no filters = all products)
- [ ] Follows existing patterns and conventions

## Technical notes

- Validate query parameters
- Use appropriate types for money values
- Log filter operations

## Definition of done

- All acceptance criteria met
- All tests pass
  `uv run pytest`
