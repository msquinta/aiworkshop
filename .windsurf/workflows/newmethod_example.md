---
description: Add a new method to an existing ABL class
package: business.logic
---

# New Method Addition Workflow

## Package: `business.logic`

This workflow is part of the `business.logic` package, which contains core business logic components for the application. Methods added using this workflow should follow the package's conventions and standards.

## Package-Level Guidelines

1. **Naming Conventions**
   - Use descriptive, action-oriented names (e.g., `CalculateTotal`, `ValidateOrder`)
   - Follow the pattern: `Verb` + `Noun` + `[Qualifier]`
   - Use PascalCase for method names

2. **Access Control**
   - Default to `PROTECTED` for internal methods
   - Use `PUBLIC` only for methods that are part of the public API
   - Mark implementation details as `PRIVATE`

3. **Documentation**
   - Include package name in method documentation
   - Reference related methods in the same package
   - Document any package-level assumptions or requirements

## Adding a New Method to the Current ABL Class

This workflow will add a new method to the currently focused ABL class in Windsurf. You'll need to provide the following information:

1. **Method Name**: Name of the new method
2. **Return Type**: Data type the method returns (use "VOID" if none)
3. **Access Modifier**: PUBLIC, PROTECTED, or PRIVATE
4. **Parameters**: Comma-separated list of parameters in format "name AS type, ..."
5. **Method Body**: The implementation code for the method

## Best Practices

- Group related methods together in the class
- Use PascalCase for method names
- Document all parameters and return values
- Include parameter validation
- Use named buffers for database access
- Implement proper error handling
- Consider thread safety for shared resources
- Keep methods focused on a single responsibility
- Use FINALLY blocks for cleanup code
- Follow the project's coding standards for variable naming and formatting
