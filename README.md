If you want to avoid appending empty parameters to the query string, you can adjust the function to include them only when the corresponding values are present. Here's an updated version of the function that addresses this concern:

```typescript
const rollUpQuery = (
   globalType: string,
   specifiedType: IProductType | null,
   state: IState | null,
): string => {
   let query = '';

   if (globalType && globalType !== allGlobalTypes) {
      query += `globalType=${encodeURIComponent(globalType)}`;
   }

   if (specifiedType && specifiedType.specifiedType !== allSpecifiedTypes.specifiedType) {
      query += `${query.length > 0 ? '&' : ''}specifiedType=${encodeURIComponent(specifiedType.specifiedType)}`;
   }

   if (state && state.abbreviation !== 'All States') {
      query += `${query.length > 0 ? '&' : ''}state=${encodeURIComponent(state.abbreviation)}`;
   }

   return query;
};
```

In this updated version:
- The `query` variable is initialized as an empty string.
- Conditions are used to check if each parameter is present and meets specific criteria before appending it to the query string.
- The ternary operator (`? :`) is utilized to determine whether to include the ampersand (`&`) based on whether the query string is already populated.

This way, the function ensures that only valid and non-empty parameters are included in the generated query string.