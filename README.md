Certainly! Here's the entire code for a simple React project with TypeScript, Material-UI, and a single component (`AccessControlComponent`) in a single file (`App.tsx`):

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
  createTheme,
  ThemeProvider,
} from '@mui/material';

const theme = createTheme();

const AccessControlComponent: React.FC = () => {
  const [accessLevels, setAccessLevels] = useState({
    edit: false,
    readOnly: false,
    disabled: false,
  });

  const handleCheckboxChange = (level: keyof typeof accessLevels) => {
    setAccessLevels((prevLevels) => ({
      ...Object.fromEntries(Object.keys(prevLevels).map((key) => [key, key === level])),
    }));
  };

  const handleUpdate = () => {
    // Add your logic to handle the update
    console.log('Updating Access Levels:', accessLevels);
  };

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
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
    </ThemeProvider>
  );
};

ReactDOM.render(
  <AccessControlComponent />,
  document.getElementById('root')
);
```

This single file (`App.tsx`) contains both the main `AccessControlComponent` and the rendering logic using `ReactDOM`. Ensure that you have the necessary dependencies installed:

```bash
npm install react react-dom @mui/material @emotion/react @emotion/styled
```

You can copy and paste this code into your project's `src` folder.


Certainly! Below is the entire file structure along with the contents for a simple React project with TypeScript and Material-UI. You can create a new project folder and organize it like this:

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

Now, let's create the files:

1. **package.json:**
   ```json
   {
     "name": "my-react-project",
     "version": "1.0.0",
     "main": "index.js",
     "license": "MIT",
     "scripts": {
       "start": "react-scripts start",
       "build": "react-scripts build",
       "test": "react-scripts test",
       "eject": "react-scripts eject"
     },
     "dependencies": {
       "@mui/material": "^5.2.3",
       "react": "^17.0.2",
       "react-dom": "^17.0.2",
       "react-scripts": "4.0.3",
       "typescript": "^4.3.5"
     },
     "eslintConfig": {
       "extends": [
         "react-app",
         "react-app/jest"
       ]
     },
     "browserslist": {
       "production": [
         ">0.2%",
         "not dead",
         "not op_mini all"
       ],
       "development": [
         "last 1 chrome version",
         "last 1 firefox version",
         "last 1 safari version"
       ]
     }
   }
   ```

2. **tsconfig.json:**
   ```json
   {
     "compilerOptions": {
       "target": "es5",
       "lib": ["dom", "dom.iterable", "esnext"],
       "allowJs": true,
       "skipLibCheck": true,
       "esModuleInterop": true,
       "strict": true,
       "forceConsistentCasingInFileNames": true,
       "module": "esnext",
       "moduleResolution": "node",
       "resolveJsonModule": true,
       "isolatedModules": true,
       "noEmit": true,
       "jsx": "react-jsx",
       "types": ["node", "react", "@types/react-dom", "@mui/material"]
     },
     "include": ["src"]
   }
   ```

3. **src/App.tsx:**
   ```tsx
   // src/App.tsx
   import React from 'react';
   import ReactDOM from 'react-dom';
   import AccessControlComponent from './AccessControlComponent';
   import './index.css';

   ReactDOM.render(
     <React.StrictMode>
       <AccessControlComponent />
     </React.StrictMode>,
     document.getElementById('root')
   );
   ```

4. **src/AccessControlComponent.tsx:**
   ```tsx
   // src/AccessControlComponent.tsx
   import React, { useState } from 'react';
   import {
     Checkbox,
     Button,
     FormControlLabel,
     FormGroup,
     Grid,
     Paper,
     Typography,
     CssBaseline,
     createTheme,
     ThemeProvider,
   } from '@mui/material';

   const theme = createTheme();

   const AccessControlComponent: React.FC = () => {
     const [accessLevels, setAccessLevels] = useState({
       edit: false,
       readOnly: false,
       disabled: false,
     });

     const handleCheckboxChange = (level: keyof typeof accessLevels) => {
       setAccessLevels((prevLevels) => ({
         ...Object.fromEntries(Object.keys(prevLevels).map((key) => [key, key === level])),
       }));
     };

     const handleUpdate = () => {
       // Add your logic to handle the update
       console.log('Updating Access Levels:', accessLevels);
     };

     return (
       <ThemeProvider theme={theme}>
         <CssBaseline />
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
       </ThemeProvider>
     );
   };

   export default AccessControlComponent;
   ```

5. **src/index.css:**
   ```css
   /* src/index.css */
   /* Add your global styles here */
   ```

Now you can navigate to your project directory and run:

```bash
npm start
```

This will start your development server, and you should see the simple React app with the `AccessControlComponent` in action.