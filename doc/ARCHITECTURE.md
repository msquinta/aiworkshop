# ABL Business Entity Architecture

This document provides an overview of the Business Entity architectural pattern used in this project.

## Pattern Overview

The Business Entity pattern separates concerns into three layers:
- **UI Layer**: Presentation and user interaction (CustomerWin.w, ItemWin.w)
- **Business Layer**: Business logic and data access (CustomerEntity.cls, EntityFactory.cls)
- **Data Layer**: Database operations through OpenEdge BusinessEntity base class

## Key Components

### EntityFactory (Singleton)
- Manages lifecycle of all business entities
- Provides centralized access through `GetInstance()`
- Returns singleton entity instances via `GetXxxEntity()` methods

### Business Entities
- Inherit from `OpenEdge.BusinessLogic.BusinessEntity`
- Encapsulate all CRUD operations for a specific entity
- Implement business validation rules
- Use data-sources to connect to database tables

### Datasets and Temp-Tables
- Defined in `.i` include files for sharing between UI and business layers
- Use `BEFORE-TABLE` for change tracking
- Enable efficient batch updates

## Data Flow

### Read Operation
1. UI calls `EntityFactory:GetInstance():GetCustomerEntity()`
2. UI calls `entity:GetCustomerByNumber(id, OUTPUT DATASET)`
3. Entity builds filter and calls inherited `ReadData(filter)`
4. Data populates temp-table in dataset
5. UI accesses data from temp-table

### Update Operation
1. UI retrieves data (read operation)
2. UI enables change tracking: `TEMP-TABLE ttCustomer:TRACKING-CHANGES = TRUE`
3. UI modifies temp-table data
4. UI calls `entity:ValidateCustomer(DATASET BY-REFERENCE, OUTPUT error)`
5. If valid, UI calls `entity:UpdateCustomer(DATASET BY-REFERENCE)`
6. Entity calls inherited `UpdateData()` which uses before-table to generate updates

## Benefits

- **Separation of Concerns**: UI, business logic, and data access are clearly separated
- **Reusability**: Business entities can be used by multiple UI components
- **Testability**: Business logic can be tested independently of UI
- **Maintainability**: Changes to business rules are centralized
- **Consistency**: Singleton pattern ensures consistent state

## Reference Implementation

See `src/business/CustomerEntity.cls` for a complete working example demonstrating:
- Entity class structure
- CRUD operations
- Business validation
- Dataset usage
- Data-source configuration

For complete documentation, see `doc/business-entity-pattern.md`.
