Certainly! Here's the entire code for the `App.tsx` file, including the `AccessControlComponent`:

```tsx
// App.tsx
import React, { useState } from 'react';
import ReactDOM from 'react-dom';
import {
  Checkbox,
  Button,
  FormControlLabel,
  FormGroup,
  Grid,
  Paper,
  Typography,
  CssBaseline,
  ThemeProvider,
  createTheme,
} from '@mui/material';

interface AccessLevels {
  edit: boolean;
  readOnly: boolean;
  disabled: boolean;
}

const theme = createTheme();

const AccessControlComponent: React.FC = () => {
  const [accessLevels, setAccessLevels] = useState<AccessLevels>({
    edit: false,
    readOnly: false,
    disabled: false,
  });

  const handleCheckboxChange = (level: keyof AccessLevels) => {
    setAccessLevels((prevLevels) => ({
      edit: level === 'edit' ? !prevLevels.edit : false,
      readOnly: level === 'readOnly' ? !prevLevels.readOnly : false,
      disabled: level === 'disabled' ? !prevLevels.disabled : false,
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
              control={<Checkbox checked={accessLevels.edit} onChange={() => handleCheckboxChange('edit')} />}
              label="Edit"
            />
            <FormControlLabel
              control={<Checkbox checked={accessLevels.readOnly} onChange={() => handleCheckboxChange('readOnly')} />}
              label="Read Only"
            />
            <FormControlLabel
              control={<Checkbox checked={accessLevels.disabled} onChange={() => handleCheckboxChange('disabled')} />}
              label="Disabled"
            />
          </FormGroup>
          <Button variant="contained" color="primary" onClick={handleUpdate} style={{ marginTop: '10px' }}>
            Update
          </Button>
        </Paper>
      </Grid>
    </Grid>
  );
};

const App: React.FC = () => {
  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <AccessControlComponent />
    </ThemeProvider>
  );
};

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

You can copy and paste this entire code into your `App.tsx` file. Make sure to install the required dependencies if you haven't already:

```bash
npm install react react-dom @mui/material @emotion/react @emotion/styled
```

This code includes both the main `App` component and the `AccessControlComponent` in a single file.