Certainly! Here's the simplified project structure with each file content:

1. **App.tsx:**
   ```tsx
   // src/App.tsx
   import React, { useState } from 'react';
   import { Checkbox, Button, FormControlLabel, FormGroup, Grid, Paper, Typography, CssBaseline } from '@mui/material';

   const AccessControlComponent: React.FC = () => {
     const [accessLevels, setAccessLevels] = useState({
       edit: false,
       readOnly: false,
       disabled: false,
     });

     const handleCheckboxChange = (level: keyof typeof accessLevels) => {
       setAccessLevels((prevLevels) => ({ ...prevLevels, [level]: !prevLevels[level] }));
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

2. **index.tsx:**
   ```tsx
   // src/index.tsx
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

3. **index.css:**
   ```css
   /* src/index.css */
   /* Add your global styles here */
   ```

Make sure you have the necessary dependencies installed:

```bash
npm install react react-dom @mui/material @emotion/react @emotion/styled
```

This simplified project structure contains only three files, making it easy to manage. Feel free to copy and paste this code into your project. If you have any further questions or requests, let me know!