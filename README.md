Certainly! Let's simplify the project structure further. Create a file named `App.tsx` with the following content:

```tsx
// App.tsx
import React, { useState } from 'react';
import { Checkbox, Button, FormControlLabel, FormGroup, Grid, Paper, Typography, CssBaseline } from '@mui/material';

const AccessControlComponent: React.FC = () => {
  const [accessLevels, setAccessLevels] = useState({
    edit: false,
    readOnly: false,
    disabled: false,
  });

  const handleCheckboxChange = (level: keyof typeof accessLevels) => {
    setAccessLevels((prevLevels) => ({ ...Object.fromEntries(Object.keys(prevLevels).map((key) => [key, key === level])) }));
  };

  const handleUpdate = () => {
    console.log('Updating Access Levels:', accessLevels);
    // Add your logic to handle the update
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

Now, create an `index.tsx` file:

```tsx
// index.tsx
import React from 'react';
import ReactDOM from 'react-dom';
import AccessControlComponent from './App';
import { CssBaseline, ThemeProvider, createTheme } from '@mui/material';

const theme = createTheme();

ReactDOM.render(
  <ThemeProvider theme={theme}>
    <CssBaseline />
    <AccessControlComponent />
  </ThemeProvider>,
  document.getElementById('root')
);
```

Create a simple `index.css` file (if needed):

```css
/* index.css */
/* Add your global styles here */
```

Your project structure should look like this:

```plaintext
my-react-project/
|-- src/
|   |-- App.tsx
|   |-- index.tsx
|   |-- index.css
|-- package.json
|-- tsconfig.json
|-- node_modules/
```

Make sure to install the dependencies:

```bash
npm install react react-dom @mui/material @emotion/react @emotion/styled
```

Now, you can run your project with:

```bash
npm start
```

This simplified structure has only three files, making it easy to manage.