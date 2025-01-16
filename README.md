## React Redux JWT Authentication & Authorization Example (Updated)

This project demonstrates a React Redux application with JWT Authentication and Authorization using modern tools and libraries. Below are the features of the updated project:

### **What's New in This Version**

1. **Updated Router to `createBrowserRouter`**
   - Migrated from traditional `Router`/`BrowserRouter` to `createBrowserRouter` for better route handling and support for data-driven routing in React Router.
   - Enhanced flexibility in defining routes and route-specific logic.

2. **Added Formik for Form Management**
   - Integrated **Formik** to manage form state, validation, and submission.
   - Simplified form handling for login, signup, and other forms with concise and declarative code.

3. **Added TanStack Query (React Query)**
   - Integrated **TanStack Query** for efficient server state management.
   - Simplified API data fetching, caching, and synchronization between the client and server.

4. **Implemented Redux Slices**
   - Reorganized Redux state management by creating **slices** using Redux Toolkit.
   - Improved readability and maintainability of the Redux store with `createSlice` for actions and reducers.

---

### **Key Features**

- JWT Authentication Flow for User Signup & Login.
- State management with Redux and slices for modularity.
- Protected routes with authorization checks.
- Form handling with **Formik** for clean and robust forms.
- Efficient API data handling with **TanStack Query**.
- Modern routing setup with `createBrowserRouter`.

---

### **User Registration and Login Flow**
For JWT Authentication, the app interacts with the following API endpoints:

- `POST api/auth/signup` for User Registration.
- `POST api/auth/signin` for User Login.

#### Workflow
- The React Client sends a request with user credentials and receives a JWT token.
- The JWT token is stored in `localStorage` and added to the HTTP headers for accessing protected resources.

---

### **How to Set Up the Project**

#### **1. Install Dependencies**
In the project directory, run:
```bash
npm install
# or
yarn install
```

#### **2. Start the Development Server**
```bash
npm start
# or
yarn start
```

Access the app at [http://localhost:8081](http://localhost:8081).

---

### **Key Libraries Used**

1. **React Router (createBrowserRouter)**
   - Enables dynamic and data-driven routing with improved API structure.

2. **Formik**
   - Simplifies form state management and validation.
   - Used for login, signup, and other interactive forms.

3. **TanStack Query (React Query)**
   - Handles server state efficiently with caching, background fetching, and synchronization.

4. **Redux Toolkit (with Slices)**
   - Modular and maintainable state management using `createSlice`.

---

### **Example Code Snippets**

#### **Router Setup with `createBrowserRouter`**
```javascript
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([
  {
    path: '/',
    element: <App />,
    children: [
      { path: 'login', element: <Login /> },
      { path: 'signup', element: <Signup /> },
      { path: 'dashboard', element: <ProtectedRoute><Dashboard /></ProtectedRoute> },
    ],
  },
]);

export default function Root() {
  return <RouterProvider router={router} />;
}
```

#### **Formik Example for Login Form**
```javascript
import { Formik, Form, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup';

const Login = () => {
  const initialValues = { email: '', password: '' };

  const validationSchema = Yup.object({
    email: Yup.string().email('Invalid email').required('Required'),
    password: Yup.string().min(6, 'Too short').required('Required'),
  });

  const onSubmit = (values) => {
    console.log(values);
  };

  return (
    <Formik initialValues={initialValues} validationSchema={validationSchema} onSubmit={onSubmit}>
      <Form>
        <Field type="email" name="email" placeholder="Email" />
        <ErrorMessage name="email" component="div" />

        <Field type="password" name="password" placeholder="Password" />
        <ErrorMessage name="password" component="div" />

        <button type="submit">Login</button>
      </Form>
    </Formik>
  );
};

export default Login;
```

#### **Using TanStack Query for Data Fetching**
```javascript
import { useQuery } from '@tanstack/react-query';

const fetchUserData = async () => {
  const response = await fetch('/api/user');
  if (!response.ok) throw new Error('Network response was not ok');
  return response.json();
};

const UserProfile = () => {
  const { data, error, isLoading } = useQuery(['user'], fetchUserData);

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return <div>Welcome, {data.name}!</div>;
};

export default UserProfile;
```

---

### **Environment Variables**
To set a custom port, create a `.env` file in the root directory and add:
```bash
PORT=8081
```

---

### **Conclusion**
This updated project integrates modern tools and practices, making it more scalable and maintainable. Feel free to explore and enhance it further!

If you have any questions or issues, check the [GitHub Discussions](https://github.com/erdemygt/react-redux-jwt-auth/discussions).

