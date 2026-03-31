# AI Workshop - OpenEdge ABL Project

This repository contains an OpenEdge ABL project demonstrating the Business Entity architectural pattern for building maintainable, testable applications with proper separation of concerns.

## Project Overview

This project showcases modern ABL development practices including:
- **Business Entity Pattern**: Separation of UI, business logic, and data access layers
- **Singleton Factory Pattern**: Centralized entity management
- **Dataset-based Architecture**: Temp-tables with change tracking for efficient data operations
- **Object-Oriented Design**: Classes, interfaces, and proper encapsulation

## Project Structure

```
src/
├── business/           # Business layer
│   ├── EntityFactory.cls       # Singleton factory for entities
│   ├── CustomerEntity.cls      # Customer business entity
│   ├── CustomerDataset.i       # Customer dataset definition
│   └── ItemEntity.cls          # Item business entity (to be added)
├── CustomerWin.w       # Customer UI window
└── ItemWin.w          # Item UI window

.windsurf/
├── rules/             # Development rules and guidelines
└── workflows/         # Automated workflows

doc/
└── business-entity-pattern.md  # Complete pattern documentation

dump/
└── sports2000.df      # Database schema
```

## Key Features

### Business Entity Pattern
- **Factory Pattern**: `EntityFactory` provides singleton instances of business entities
- **Entity Classes**: Inherit from `OpenEdge.BusinessLogic.BusinessEntity`
- **Dataset Definitions**: Shared temp-table definitions between UI and business layers
- **Validation**: Business rules centralized in entity methods
- **Change Tracking**: Before-tables enable efficient database updates

### Example Usage

```abl
/* Get entity through factory */
VAR EntityFactory objFactory = EntityFactory:GetInstance().
VAR CustomerEntity objEntity = objFactory:GetCustomerEntity().

/* Read operation */
VAR LOGICAL lFound = objEntity:GetCustomerByNumber(123, OUTPUT DATASET dsCustomer).

/* Update operation */
TEMP-TABLE ttCustomer:TRACKING-CHANGES = TRUE.
ttCustomer.Name = "New Name".

VAR CHARACTER cError.
IF objEntity:ValidateCustomer(DATASET dsCustomer BY-REFERENCE, OUTPUT cError) THEN
    objEntity:UpdateCustomer(DATASET dsCustomer BY-REFERENCE).
```

## Documentation

See `doc/business-entity-pattern.md` for comprehensive documentation including:
- Mandatory rules and best practices
- Step-by-step implementation guide
- Common patterns for CRUD operations
- Anti-patterns to avoid
- Migration strategy from legacy code

## Database

The project uses the sports2000 database. Schema is available in `dump/sports2000.df`.

## Getting Started

1. Ensure OpenEdge 12.8+ is installed
2. Create the sports2000 database using the provided schema
3. Configure database connection in `openedge-project.json`
4. Build the project using `build.xml`

## Development Guidelines

This project follows the Business Entity pattern as documented in `doc/business-entity-pattern.md`. Key principles:

- ✅ Use factory pattern for entity instantiation
- ✅ Separate business logic from UI
- ✅ Enable change tracking before updates
- ✅ Validate before persistence
- ❌ No direct database access in UI
- ❌ No business logic in UI code

## License

This is a workshop/training project demonstrating ABL best practices.
