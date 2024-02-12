
```jsx
import React, { useState } from 'react';
import Checkbox from '@mui/material/Checkbox';
import Typography from '@mui/material/Typography';
import RadioButtonUnchecked from '@mui/icons-material/RadioButtonUnchecked';
import RadioButtonCheckedRounded from '@mui/icons-material/RadioButtonCheckedRounded';

const YourComponent = () => {
  const [isChecked, setChecked] = useState(false);

  const handleCheckboxClick = () => {
    setChecked(!isChecked);
  };

  const handleRadioClick = () => {
    // Uncheck the checkbox when the radio button is clicked
    setChecked(false);
  };

  return (
    <div>
      <Typography className="users-medium">
        <Checkbox
          icon={<RadioButtonUnchecked fontSize="medium" />}
          checkedIcon={<RadioButtonCheckedRounded fontSize="medium" />}
          sx={{ mr: '10px' }}
          checked={isChecked}
          onClick={handleCheckboxClick}
        />
      </Typography>

      <label>
        <input type="radio" onClick={handleRadioClick} />
        Radio Button
      </label>
      
      <label>
        <input type="radio" />
        Another Radio Button
      </label>
    </div>
  );
};

export default YourComponent;
```



```jsx
import React, { useState } from 'react';
import Checkbox from '@mui/material/Checkbox';
import Typography from '@mui/material/Typography';
import RadioButtonUnchecked from '@mui/icons-material/RadioButtonUnchecked';
import RadioButtonCheckedRounded from '@mui/icons-material/RadioButtonCheckedRounded';

const YourComponent = () => {
  const [isCheckboxDisabled, setCheckboxDisabled] = useState(false);

  const handleButtonClick = () => {
    // Disable the checkbox when the button is clicked
    setCheckboxDisabled(true);
  };

  return (
    <div>
      <Typography className="users-medium">
        <Checkbox
          icon={<RadioButtonUnchecked fontSize="medium" />}
          checkedIcon={<RadioButtonCheckedRounded fontSize="medium" />}
          sx={{ mr: '10px' }}
          disabled={isCheckboxDisabled}
        />
      </Typography>

      <button onClick={handleButtonClick}>Click me to disable Checkbox</button>
    </div>
  );
};

export default YourComponent;


```

Certainly! If you don't need the first name and last name in the `User` interface, you can simplify it. Here's the modified code:

1. **Update `accessLevels.ts`:**

   ```typescript
   // accessLevels.ts

   export interface AccessLevel {
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

2. **Update `YourComponent.tsx`:**

   ```tsx
   // YourComponent.tsx

   import React from 'react';
   import { Box, Paper, Stack } from '@material-ui/core';
   import { AccessLevel } from './path-to-accessLevels/accessLevels'; // Update the path accordingly

   // Assume you have UserItemSkeleton and AdminUserItem components defined

   interface User {
     accessLevels: AccessLevel[];
   }

   interface YourComponentProps {
     loading: { users: boolean };
     users: User[];
   }

   const YourComponent: React.FC<YourComponentProps> = ({ loading, users }) => {
     return (
       <Stack paddingTop={10}>
         <Paper className="section-container-user-edit-screen">
           {/* Your other components */}
           <UserListHeaderAdminAccess />
           <Box className="users-box">
             {loading.users ? (
               Array.from({ length: 9 }, (v, i) => <UserItemSkeleton key={i} />)
             ) : (
               users.map((user, index) => (
                 <AdminUserItem user={user} key={index} />
               ))
             )}
           </Box>
         </Paper>
       </Stack>
     );
   };

   export default YourComponent;
   ```

3. **Update `App.tsx`:**

   ```tsx
   // App.tsx

   import React from 'react';
   import YourComponent from './path-to-your-component/YourComponent'; // Update the path accordingly
   import { accessLevels } from './path-to-accessLevels/accessLevels'; // Update the path accordingly

   const App: React.FC = () => {
     const loading = { users: false }; // Assume loading state
     const users = [
       {
         accessLevels: [accessLevels[0], accessLevels[1]], // Add the relevant access levels
       },
       // Add more users as needed
     ];

     return (
       <div>
         {/* Other components */}
         <YourComponent loading={loading} users={users} />
       </div>
     );
   };

   export default App;
   ```

This way, the `User` interface only includes the `accessLevels` property, and you can update the `users` array accordingly.
