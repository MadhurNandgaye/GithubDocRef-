Certainly! If you want to maintain the same naming convention for the loading logic, you can structure the code like this:

```tsx
import React from 'react';
import { Box } from 'your-component-library'; // Make sure to import your component library
import { AccessLevel } from './types';
import UserItemSkeleton from './UserItemSkeleton';
import AdminUserItem from './AdminUserItem';

interface UsersComponentProps {
  loading: {
    users: boolean;
  };
  users: AccessLevel[]; // Assuming users have the same structure as AccessLevel
}

const UsersComponent: React.FC<UsersComponentProps> = ({ users, loading }) => {
  return (
    <Box className="users-box">
      {loading.users ? (
        Array.from({ length: 9 }, (_, index) => (
          <UserItemSkeleton key={index} />
        ))
      ) : (
        users.map((user) => (
          <AdminUserItem user={user} key={user.level} />
        ))
      )}
    </Box>
  );
};

export default UsersComponent;
```

In this example, I've assumed that the structure of your users matches the `AccessLevel` interface. Adjust the `users` prop type according to your actual user data structure. The key for each `AdminUserItem` is set to `user.level` based on the assumption that `level` is a unique identifier for each user. Update it according to your actual data structure.



Certainly! You can define a TypeScript interface for the access levels and then use it in your constant. Here's the updated file:

```typescript
// accessLevels.ts

interface AccessLevel {
  level: string;
  action: string;
}

export const accessLevels: AccessLevel[] = [
  { level: 'Users + Access', action: 'Can adjust user access' },
  { level: 'Actions', action: 'Can change action status' },
  { level: 'Orders', action: 'Can add price exceptions' },
  { level: 'Holidays', action: 'Can add/delete holidays' },
  { level: 'SLAS', action: 'Can change SLAS' },
  { level: 'Product Groups', action: 'Can create and adjust groups' },
  { level: 'Enable Vendor', action: 'Can enable or disable a vendor' },
  { level: 'Vendor Profile Main', action: 'Can adjust contact, account, notes, and document info' },
  { level: 'Vendor Capacity', action: 'Can add and adjust capacity' },
  { level: 'Vendor Products & Pricing', action: 'Can add and adjust pricing' },
  { level: 'Vendor Product Enabling', action: 'Can enable/disable products' },
  { level: 'Vendor Billing', action: 'Can export/import billing details from vendor' },
  { level: 'Vendor Billing Reconciliation', action: 'Can approve billing exceptions' },
];
```

Now, you have a clear TypeScript interface (`AccessLevel`) for your access levels. This will help in maintaining type safety throughout your React project.

Certainly! You can store this data in a TypeScript file as a constant and then import it into your React project. Here's an example file named `accessLevels.ts`:

```typescript
// accessLevels.ts

export const accessLevels = [
  { level: 'Users + Access', action: 'Can adjust user access' },
  { level: 'Actions', action: 'Can change action status' },
  { level: 'Orders', action: 'Can add price exceptions' },
  { level: 'Holidays', action: 'Can add/delete holidays' },
  { level: 'SLAS', action: 'Can change SLAS' },
  { level: 'Product Groups', action: 'Can create and adjust groups' },
  { level: 'Enable Vendor', action: 'Can enable or disable a vendor' },
  { level: 'Vendor Profile Main', action: 'Can adjust contact, account, notes, and document info' },
  { level: 'Vendor Capacity', action: 'Can add and adjust capacity' },
  { level: 'Vendor Products & Pricing', action: 'Can add and adjust pricing' },
  { level: 'Vendor Product Enabling', action: 'Can enable/disable products' },
  { level: 'Vendor Billing', action: 'Can export/import billing details from vendor' },
  { level: 'Vendor Billing Reconciliation', action: 'Can approve billing exceptions' },
];
```

You can then import this constant in your React component:

```typescript
// Your React Component

import React from 'react';
import { accessLevels } from './accessLevels';

const YourComponent: React.FC = () => {
  return (
    <div>
      <h1>Access Levels</h1>
      <table>
        <thead>
          <tr>
            <th>Access Level</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {accessLevels.map((level, index) => (
            <tr key={index}>
              <td>{level.level}</td>
              <td>{level.action}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default YourComponent;
```

Make sure to adjust the paths and file names according to your project structure.




Access Levels

Users + Access

Can adjust user access

Actions

Can change action status

Orders

Can add price exceptions

Holidays

Can add/delete holidays

SLAS

Can change SLAS

Product Groups

Can create and adjust groups

Enable Vendor

Can enable or disable a vendor

Vendor Profile Main

Can adjust contact, account, notes, and document info

Vendor Capacity

Can add and adjust capacity

Vendor Products & Pricing

Can Add and adjust pricing

Vendor Product Enabling

Can enable/disable products

Vendor Billing

Can export/import billing detalls from vendor

Vendor Billing Reconciliation

Can approve billing exceptions