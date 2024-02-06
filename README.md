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





+
j
j
j
Certainly! Here's a single-page React-Typescript component that includes the desired functionality using Material-UI:

```tsx
// AccessControlComponent.tsx
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

export default AccessControlComponent;
```

You can copy and paste this entire component into a single file, for example, `AccessControlComponent.tsx`, and then use it in your project. Make sure you have the required dependencies (React, Material-UI) installed in your project. You can install them using:

```bash
npm install react @mui/material @emotion/react @emotion/styled
```

Once installed, you can import and use `AccessControlComponent` in your main application file.

Certainly! Here's the modified content for your `App.tsx` file, which includes the `AccessControlComponent`:

```tsx
// App.tsx
import React from 'react';
import ReactDOM from 'react-dom';
import AccessControlComponent from './AccessControlComponent';
import { CssBaseline, ThemeProvider, createTheme } from '@mui/material';

const theme = createTheme();

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

Ensure that you have the required dependencies installed in your project. If not, you can install them using:

```bash
npm install react react-dom @mui/material @emotion/react @emotion/styled
```

After pasting this content into your `App.tsx` file, you should have the `AccessControlComponent` integrated into your main application. Remember to update your `index.html` file to have a root element with the id "root" where React will mount the application.