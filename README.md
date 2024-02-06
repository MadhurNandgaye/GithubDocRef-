Certainly! Here's a simple example of a React-Typescript project with the `AccessControlComponent` all in a single file:

```tsx
// App.tsx
import React, { useState } from 'react';
import {
  Checkbox,
  Button,
  FormControlLabel,
  FormGroup,
  Grid,
  Paper,
  Typography,
} from '@mui/material';

interface AccessLevels {
  edit: boolean;
  readOnly: boolean;
  disabled: boolean;
}

const AccessControlComponent: React.FC = () => {
  const [accessLevels, setAccessLevels] = useState<AccessLevels>({
    edit: false,
    readOnly: false,
    disabled: false,
  });

  const handleCheckboxChange = (level: keyof AccessLevels) => {
    setAccessLevels((prevLevels) => ({
      ...prevLevels,
      [level]: !prevLevels[level],
    }));
  };

  const handleUpdate = () => {
    // Add your logic to handle the update
    console.log('Updating Access Levels:', accessLevels);
  };

  return (
    <Grid container justifyContent="center" alignItems="center" style={{ height: '100vh' }}>
      <Grid item xs={10} md={6} lg={4}>
        <Paper elevation={3} style={{ padding: '20px' }}>
          <Typography variant="h5" gutterBottom>
            Access Levels
          </Typography>
          <FormGroup>
            <FormControlLabel
              control={
                <Checkbox
                  checked={accessLevels.edit}
                  onChange={() => handleCheckboxChange('edit')}
                />
              }
              label="Edit"
            />
            <FormControlLabel
              control={
                <Checkbox
                  checked={accessLevels.readOnly}
                  onChange={() => handleCheckboxChange('readOnly')}
                />
              }
              label="Read Only"
            />
            <FormControlLabel
              control={
                <Checkbox
                  checked={accessLevels.disabled}
                  onChange={() => handleCheckboxChange('disabled')}
                />
              }
              label="Disabled"
            />
          </FormGroup>
          <Button
            variant="contained"
            color="primary"
            onClick={handleUpdate}
            style={{ marginTop: '10px' }}
          >
            Update
          </Button>
        </Paper>
      </Grid>
    </Grid>
  );
};

// index.tsx
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <React.StrictMode>
    <AccessControlComponent />
  </React.StrictMode>,
  document.getElementById('root')
);
```

This single file includes the `AccessControlComponent` and the `ReactDOM.render` part to render it. Keep in mind that as your project grows, it's recommended to organize your code into separate files and folders for better maintainability.