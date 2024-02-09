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