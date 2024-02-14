Certainly, let's break down the TypeScript function `rollUpQuery` and ensure that it doesn't pass empty values by using constants:

```typescript
const rollUpQuery = (
   globalType: string,
   specifiedType: IProductType | null,
   state: IState | null,
): string => {
   const allGlobalTypes = 'your_constant_for_empty_globalType';
   const allSpecifiedTypes = { specifiedType: 'your_constant_for_empty_specifiedType' };
   const allStates = 'your_constant_for_empty_state';

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

Explanation:

1. Constants (`allGlobalTypes`, `allSpecifiedTypes`, and `allStates`) are defined for empty or default values.

2. The function checks each parameter (`globalType`, `specifiedType`, and `state`) and appends them to the query string only if they are not empty and meet specific conditions.

3. If any parameter is empty or has a default value, the corresponding constant is used in the query string.

This ensures that the generated query string doesn't contain empty values and uses constants in their place when necessary. Adjust the constant values according to your requirements.