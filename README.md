Certainly! Here's the modified code in TypeScript:

```tsx
import React from 'react';
import { Stack, Typography, Popper, Paper, MenuList, MenuItem, ClickAwayListener } from '@mui/material';

interface YourComponentProps {
  user: { email: string; firstName: string; lastName: string };
  anchorEl: null | HTMLElement;
  open: boolean;
  handleActionClick: (option: string) => void;
  handleClick: () => void;
  handleClickAway: () => void;
}

const YourComponent: React.FC<YourComponentProps> = ({
  user,
  anchorEl,
  open,
  handleActionClick,
  handleClick,
  handleClickAway,
}) => {
  return (
    <Stack direction="row" justifyContent="space-between" alignItems="center">

      <Stack direction="row">

        <Typography sx={{ paddingRight: 90 }} className="users-medium">
          {user.email}
        </Typography>

        <Typography className="users-medium">{user.firstName}</Typography>

        <Typography className="users-medium">{user.lastName}</Typography>

        <Typography className="users-medium">Admin</Typography>

        <Stack style={{ position: 'relative' }}>
          {/* Using inline styles for positioning */}
          <ActionButton
            anchorEl={anchorEl}
            menuItems={UserContent.ROW_OPTIONS}
            open={open}
            handleActionClick={handleActionClick}
            handleClick={handleClick}
            handleClickAway={handleClickAway}
            style={{ position: 'absolute', zIndex: 1 }}
          />
        </Stack>

      </Stack>

    </Stack>
  );
};

interface ActionButtonProps {
  anchorEl: null | HTMLElement;
  open: boolean;
  handleActionClick: (option: string) => void;
  handleClick: () => void;
  handleClickAway: () => void;
  menuItems: string[];
}

const ActionButton: React.FC<ActionButtonProps> = ({
  anchorEl,
  open,
  handleActionClick,
  handleClick,
  handleClickAway,
  menuItems,
}) => {
  return (
    <Popper open={open} anchorEl={anchorEl} placement="bottom-end">
      <ClickAwayListener onClickAway={handleClickAway}>
        <Paper style={{ maxHeight: '200px', overflowY: 'auto' }}>
          <MenuList>
            {menuItems.map((option, index) => (
              <MenuItem key={index} onClick={() => handleActionClick(option)}>
                {option}
              </MenuItem>
            ))}
          </MenuList>
        </Paper>
      </ClickAwayListener>
    </Popper>
  );
};
```

Make sure to adapt the code according to your specific requirements and import the necessary modules from Material-UI.