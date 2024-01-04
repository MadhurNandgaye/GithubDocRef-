Sure, let's break down the project into different files to organize the code better. Here's a more structured approach:

### 1. File Structure:

```
src/
|-- components/
|   |-- CommentSection.tsx
|   |-- LoginForm.tsx
|-- App.tsx
|-- index.tsx
|-- types.ts
```

### 2. types.ts
This file will contain TypeScript interfaces for comments and users.

```typescript
// types.ts

export interface Comment {
  user: string;
  text: string;
  replies: Comment[];
}

export interface User {
  username: string;
  password: string;
}
```

### 3. components/LoginForm.tsx
This component handles user authentication.

```tsx
// components/LoginForm.tsx

import React, { useState } from 'react';
import { User } from '../types';

interface LoginFormProps {
  onLogin: (user: User) => void;
}

const LoginForm: React.FC<LoginFormProps> = ({ onLogin }) => {
  const [username, setUsername] = useState<string>('');
  const [password, setPassword] = useState<string>('');

  const handleLogin = () => {
    const user: User = { username, password };
    onLogin(user);
  };

  return (
    <div>
      <input type="text" placeholder="Username" onChange={(e) => setUsername(e.target.value)} />
      <input type="password" placeholder="Password" onChange={(e) => setPassword(e.target.value)} />
      <button onClick={handleLogin}>Login</button>
    </div>
  );
};

export default LoginForm;
```

### 4. components/CommentSection.tsx
This component manages comments and replies.

```tsx
// components/CommentSection.tsx

import React, { useState } from 'react';
import { Comment } from '../types';

interface CommentSectionProps {
  user: string;
}

const CommentSection: React.FC<CommentSectionProps> = ({ user }) => {
  const [comments, setComments] = useState<Comment[]>([]);
  const [newComment, setNewComment] = useState<string>('');

  const addComment = () => {
    const comment: Comment = {
      user,
      text: newComment,
      replies: [],
    };
    setComments([...comments, comment]);
    setNewComment('');
  };

  const addReply = (index: number, replyText: string) => {
    const updatedComments = [...comments];
    updatedComments[index].replies.push({
      user,
      text: replyText,
      replies: [],
    });
    setComments(updatedComments);
  };

  return (
    <div>
      <textarea value={newComment} onChange={(e) => setNewComment(e.target.value)} placeholder="Add a comment"></textarea>
      <button onClick={addComment}>Add Comment</button>

      {comments.map((comment, index) => (
        <div key={index}>
          <strong>{comment.user}</strong>: {comment.text}
          <button onClick={() => /* Implement reply functionality */}>Reply</button>
          {/* Render replies here */}
        </div>
      ))}
    </div>
  );
};

export default CommentSection;
```

### 5. App.tsx
The main component that ties everything together.

```tsx
// App.tsx

import React, { useState } from 'react';
import LoginForm from './components/LoginForm';
import CommentSection from './components/CommentSection';
import { User } from './types';

const App: React.FC = () => {
  const [user, setUser] = useState<string | null>(null);

  const handleLogin = (loggedInUser: User) => {
    // Here, you can add actual authentication logic.
    // For simplicity, we are just setting the user.
    setUser(loggedInUser.username);
  };

  return (
    <div>
      {!user ? (
        <LoginForm onLogin={handleLogin} />
      ) : (
        <CommentSection user={user} />
      )}
    </div>
  );
};

export default App;
```

This provides a basic structure to get started with the comment section, user authentication, and reply functionality. You would still need to expand upon this foundation by implementing more features, refining the UI, and adding actual authentication logic.