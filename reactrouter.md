React Router Cheat Checklist
===

[![NPM version](https://img.shields.io/npm/v/react-router-dom.svg?style=flat)](https://npmjs.org/package/react-router-dom)
[![Downloads](https://img.shields.io/npm/dm/react-router-dom.svg?style=flat)](https://www.npmjs.com/package/react-router-dom)
[![Repo Dependents](https://badgen.net/github/dependents-repo/remix-run/react-router)](https://github.com/remix-run/react-router/network/dependents)
[![Github repo](https://badgen.net/badge/icon/Github?icon=github&label)](https://github.com/remix-run/react-router)

Comprehensive [React Router 6.x](https://reactrouter.com/en/main/start/overview) Cheat List for Beginners
<!--rehype:style=padding-top: 12px;-->

getting Started
----

### Install and use

```bash
$ npm create vite@latest myApp --\
     --template react
# Follow the prompts
$ cd <myApp>
$ npm install react-router-dom \
    localforage \
    match-sorter \
    sort-by
$ npm run dev
```

### Add router
<!--rehype:wrap-class=row-span-2-->

```jsx {3-6,8-13,19}
import React from "react";
import ReactDOM from "react-dom/client";
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello world!</div>,
  },
]);

const root=document.getElementById('root');

ReactDOM.createRoot(root).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

### Root route

```jsx {1,6}
import Root from "./routes/root";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
  },
]);
```

### Handling not found errors

```jsx {1,7}
import ErrorPage from "./error-page";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
  },
]);
```

### `contacts` User Interface

```jsx {1,9-12}
import Contact from "./routes/contact";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
  },
  {
    path: "contacts/:contactId",
    element: <Contact />,
  },
]);
```

### Nested routing

`src/main.jsx`

```jsx {6-11}
const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
      },
    ],
  },
]);
```

`src/routes/root.jsx`

```jsx {1,8}
import { Outlet } from "react-router-dom";

export default function Root() {
  return (
    <>
      {/* All other elements*/}
      <div id="detail">
        <Outlet />
      </div>
    </>
  );
}
```

### Client routing

```jsx {2,9,14}
import {
  Outlet, Link
} from "react-router-dom";

export default function Root() {
  return (
    <ul>
      <li>
        <Link to={`contacts/1`}>
          Your Name
        </Link>
      </li>
      <li>
        <Link to={`contacts/2`}>
          Your Friend
        </Link>
      </li>
    </ul>
  );
}
```

### Create Contact
<!--rehype:wrap-class=row-span-2-->

Create action and change `<form>` to `<Form>`

```jsx {5,8,11-14,20-22}
import {
  Outlet,
  Link,
  useLoaderData,
  Form,
} from "react-router-dom";
import {
  getContacts, createContact
} from "../contacts";

export async function action() {
  const contact = await createContact();
  return { contact };
}
export default function Root() {
  const { contacts } = useLoaderData();
  return (
    <div id="sidebar">
      <h1>React Router Contacts</h1>
      <Form method="post">
        <button type="submit">New</button>
      </Form>
    </div>
  );
}
```

Import and set the `action` on the route

```jsx {3,12}
import Root, {
  loader as rootLoader,
  action as rootAction,
} from "./routes/root";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
      },
    ],
  },
]);
```

### URL parameters in loader
<!--rehype:wrap-class=row-span-3-->

```jsx {3}
[
  {
    path: "contacts/:contactId",
    element: <Contact />,
  },
];
```

`:contactId` URL segment. The colon (<pur>:</pur>) has a special meaning, turning it into a "`dynamic segment`"

```jsx {1-4,6-8,11}
import {
  useLoaderData
} from "react-router-dom";
import { getContact } from "../contacts";

export async function loader({ params }) {
  return getContact(params.contactId);
}

export default function Contact() {
  const contact = useLoaderData();
  // existing code
}
```

Configure `loader` on the route

```jsx {2,16}
import Contact, {
  loader as contactLoader,
} from "./routes/contact";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
        loader: contactLoader,
      },
    ],
  },
]);
```

### update data
<!--rehype:wrap-class=row-span-3-->

```jsx
import {
  Form, useLoaderData
} from "react-router-dom";

export default function EditContact() {
  const contact = useLoaderData();

  return (
    <Form method="post" id="contact-form">
      <label>
        <span>Twitter</span>
        <input
          type="text"
          name="twitter"
          placeholder="@jack"
          defaultValue={contact.twitter}
        />
      </label>
      <label>
        <span>Notes</span>
        <textarea
          name="notes"
          defaultValue={contact.notes}
          rows={6}
        />
      </label>
      <p>
        <button type="submit">保存</button>
        <button type="button">取消</button>
      </p>
    </Form>
  );
}
```

Add new edit route

```jsx {1,16-20}
import EditContact from "./routes/edit";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
        loader: contactLoader,
      },
      {
        path: "contacts/:contactId/edit",
        element: <EditContact />,
        loader: contactLoader,
      },
    ],
  },
]);
```

### Active link style

```jsx {2,7-8}
import {
  NavLink,
} from "react-router-dom";

<NavLink
  to={`contacts/${contact.id}`}
  className={({ isActive, isPending }) =>
    isActive
      ? "active"
      : isPending
      ? "pending"
      : ""
  }
>
  {/* other code */}
</NavLink>
```

### Global Pending User Interface

```jsx {7,13-14}
import {
  useNavigation,
} from "react-router-dom";

export default function Root() {
  const { contacts } = useLoaderData();
  const navigation = useNavigation();

  return (
    <div
      id="detail"
      className={
        navigation.state === 'loading'
          ? 'loading' : ''
      }
    >
      <Outlet />
    </div>
  );
}
```

### Use FormData to update contacts
<!--rehype:wrap-class=col-span-2-->

Add an action to the edit module

```jsx {4,6,8-13}
import {
  Form,
  useLoaderData,
  redirect,
} from "react-router-dom";
import { updateContact } from "../contacts";

export async function action({ request, params }) {
  const formData = await request.formData();
  const updates = Object.fromEntries(formData);
  await updateContact(params.contactId, updates);
  return redirect(`/contacts/${params.contactId}`);
}
```

Connect actions to routes

```jsx {2,22}
import EditContact, {
  action as editAction,
} from "./routes/edit";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
        loader: contactLoader,
      },
      {
        path: "contacts/:contactId/edit",
        element: <EditContact />,
        loader: contactLoader,
        action: editAction,
      },
    ],
  },
]);
```

### Delete Record

```jsx {3}
<Form
  method="post"
  action="destroy"
  onSubmit={(event) => {
    if (!confirm("Please confirm that you want to delete this record")) {
      event.preventDefault();
    }
  }}
>
  <button type="submit">删除</button>
</Form>
```

Add destroy action

```jsx
import {redirect} from "react-router-dom";
import {deleteContact} from "../contacts";

export async function action({ params }) {
  await deleteContact(params.contactId);
  return redirect("/");
}
```

Add the `destroy` route to the routing configuration

```jsx {2,9-12}
import {
  action as destroyAction
} from "./routes/destroy";

const router = createBrowserRouter([
  {
    path: "/",
    children: [
      {
       path: "contacts/:contactId/destroy",
       action: destroyAction,
      },
    ],
  },
]);
```

### Context error

```jsx {2}
export async function action({ params }) {
  throw new Error("oh dang!");
  await deleteContact(params.contactId);
  return redirect("/");
}
```

Let's create a contextual error message for the `destroy` route:

```jsx {5}
[
  {
    path: "contacts/:contactId/destroy",
    action: destroyAction,
    errorElement: <div>Oops! There is an error</div>,
  },
];
```

### Home page routing

```jsx {1,11}
import Index from "./routes/index";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      { index: true, element: <Index /> },
    ],
  },
]);
```

### Cancel button

```jsx {5,10,18-20}
import {
  Form,
  useLoaderData,
  redirect,
  useNavigate,
} from "react-router-dom";

export default function Edit() {
  const contact = useLoaderData();
  const navigate = useNavigate();

  return (
    <Form method="post" id="contact-form">
      <div>
        <button type="submit">保存</button>
        <button
          type="button"
          onClick={() => {
            navigate(-1);
          }}
        >
          Cancel
        </button>
      </div>
    </Form>
  );
}
```

### Get submissions using client routing
<!--rehype:wrap-class=row-span-2-->

Change `<form>` to `<Form>`

```jsx {1,9}
<Form id="search-form" role="search">
  <input
    id="q"
    aria-label="Search contacts"
    placeholder="Search"
    type="search"
    name="q"
  />
</Form>
```

If there is a `URLSearchParams` filter list

```jsx {1,4}
export async function loader({ request }) {
  const url = new URL(request.url);
  const q = url.searchParams.get("q");
  const contacts = await getContacts(q);
  return { contacts };
}
```

### Synchronize URL to form state
<!--rehype:wrap-class=row-span-2-->

```jsx {5,9,20}
export async function loader({ request }) {
  const url = new URL(request.url);
  const q = url.searchParams.get("q");
  const contacts = await getContacts(q);
  return { contacts, q };
}

export default function Root() {
  const { contacts, q } = useLoaderData();
  const navigation = useNavigation();

  return (
    <Form id="search-form" role="search">
      <input
        id="q"
        aria-label="Search contacts"
        placeholder="Search"
        type="search"
        name="q"
        defaultValue={q}
      />
      {/* existing code */}
    </Form>
  );
}
```

### Synchronize input values ​​with URL search parameters

```jsx {1,7-9}
import { useEffect } from "react";

export default function Root() {
  const { contacts, q } = useLoaderData();
  const navigation = useNavigation();

  useEffect(() => {
    document.getElementById("q").value = q;
  }, [q]);
}
```

### Submit change Forms

```jsx {2,8,19-21}
import {
  useSubmit,
} from "react-router-dom";

export default function Root() {
  const { contacts, q } = useLoaderData();
  const navigation = useNavigation();
  const submit = useSubmit();

  return (
    <Form id="search-form" role="search">
      <input
        id="q"
        aria-label="Search contacts"
        placeholder="Search"
        type="search"
        name="q"
        defaultValue={q}
        onChange={(event) => {
          submit(event.currentTarget.form);
        }}
      />
      {/* existing code */}
    </Form>
  );
}
```

Routers
---

### Select router

In v6.4, new routers supporting new data APIs were introduced:

:-- | --
:-- | --
`createBrowserRouter` | [#](https://reactrouter.com/en/main/routers/create-browser-router)
`createMemoryRouter` | [#](https://reactrouter.com/en/main/routers/create-memory-router)
`createHashRouter` | [#](https://reactrouter.com/en/main/routers/create-hash-router)

The following routers do not support the data API:

:-- | --
:-- | --
`<BrowserRouter>` | [#](https://reactrouter.com/en/main/router-components/browser-router)
`<MemoryRouter>` | [#](https://reactrouter.com/en/main/router-components/memory-router)
`<HashRouter>` | [#](https://reactrouter.com/en/main/router-components/hash-router)
`<NativeRouter>` | [#](https://reactrouter.com/en/main/router-components/native-router)
`<StaticRouter>` | [#](https://reactrouter.com/en/main/router-components/static-router)

### Routing example
<!--rehype:wrap-class=col-span-2-->

The easiest way to quickly update to v6.4 is to get help from createRoutesFromElements, so you don't need to convert the `<Route>` elements into route objects

```jsx
import {
  createBrowserRouter,
  createRoutesFromElements,
  Route,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<Root />}>
      <Route path="dashboard" element={<Dashboard />} />
      {/* ... etc. */}
    </Route>
  )
);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

### createBrowserRouter
<!--rehype:wrap-class=row-span-2-->

```jsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

import Root, {rootLoader} from "./root";
import Team, {teamLoader} from "./team";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    loader: rootLoader,
    children: [
      {
        path: "team",
        element: <Team />,
        loader: teamLoader,
      },
    ],
  },
]);

const root=document.getElementById('root');

ReactDOM.createRoot(root).render(
  <RouterProvider router={router} />
);
```

Type Declaration

```jsx
function createBrowserRouter(
  routes: RouteObject[],
  opts?: {
    basename?: string;
    window?: Window;
  }
): RemixRouter;
```

routes

```jsx
createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    loader: rootLoader,
    children: [
      {
        path: "events/:id",
        element: <Event />,
        loader: eventLoader,
      },
    ],
  },
]);
```

`basename` is used when you cannot deploy to the root of the domain, but instead deploy to a subdirectory

```jsx
createBrowserRouter(routes, {
  basename: "/app",
});

createBrowserRouter(routes, {
  basename: "/app",
});
<Link to="/" />;
// results in <a href="/app" />

createBrowserRouter(routes, {
  basename: "/app/",
});
<Link to="/" />;
// results in <a href="/app/" />
```

### createHashRouter

```jsx {4,11}
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  createHashRouter,
  RouterProvider,
} from "react-router-dom";

import Root, { rootLoader } from "./root";
import Team, { teamLoader } from "./team";

const router = createHashRouter([
  {
    path: "/",
    element: <Root />,
    loader: rootLoader,
    children: [
      {
        path: "team",
        element: <Team />,
        loader: teamLoader,
      },
    ],
  },
]);

const root=document.getElementById('root');

ReactDOM.createRoot(root).render(
  <RouterProvider router={router} />
);
```

### createMemoryRouter
<!--rehype:wrap-class=row-span-2-->

```jsx {2-3,24-27}
import {
  RouterProvider,
  createMemoryRouter,
} from "react-router-dom";
import * as React from "react";
import {
  render,
  waitFor,
  screen,
} from "@testing-library/react";
import "@testing-library/jest-dom";
import CalendarEvent from "./event";

test("event route", async () => {
  const FAKE_EVENT = { name: "Test event" };
  const routes = [
    {
      path: "/events/:id",
      element: <CalendarEvent />,
      loader: () => FAKE_EVENT,
    },
  ];

  const router=createMemoryRouter(routes,{
    initialEntries: ["/", "/events/123"],
    initialIndex: 1,
  });

  render(
    <RouterProvider router={router} />
  );

  await waitFor(
    () => screen.getByRole("heading")
  );
  expect(screen.getByRole("heading"))
    .toHaveTextContent(
    FAKE_EVENT.name
  );
});
```

initialEntries

```jsx
createMemoryRouter(routes, {
  initialEntries: ["/", "/events/123"],
});
```

initialIndex

```jsx {3}
createMemoryRouter(routes, {
  initialEntries: ["/", "/events/123"],
  initialIndex: 1,
  // start at "/events/123"
});
```

### \<RouterProvider>

```jsx {26}
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    children: [
      {
        path: "dashboard",
        element: <Dashboard />,
      },
      {
        path: "about",
        element: <About />,
      },
    ],
  },
]);

const root=document.getElementById('root');

ReactDOM.createRoot(root).render(
  <RouterProvider
    router={router}
    fallbackElement={<BigSpinner />}
  />
);
```

`fallbackElement` If you are not server rendering your application, DataBrowserRouter will start all matching route loaders on installation. During this time, you can provide a fallbackElement to indicate to the user that the application is running

```jsx {3}
<RouterProvider
  router={router}
  fallbackElement={<SpinnerOfDoom />}
/>
```

Router Components
---

### \<BrowserRouter>

```jsx {4}
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  BrowserRouter
} from "react-router-dom";

const root=document.getElementById('root');
ReactDOM.createRoot(root).render(
  <HashRouter>
    {/* The rest of your application goes here */}
  </HashRouter>,
);
```

`<BrowserRouter>` uses a clean `URL` to store the current location in the browser's address bar and navigate using the browser's built-in history stack

### \<HashRouter>

```jsx {4}
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  HashRouter
} from "react-router-dom";

const root=document.getElementById('root');
ReactDOM.createRoot(root).render(
  <HashRouter>
    {/* The rest of your application goes here */}
  </HashRouter>,
);
```

`<HashRouter>` is for web browsers that for some reason should not (or cannot) send the URL to the server

### \<NativeRouter>

```jsx {3}
import * as React from "react";
import {
  NativeRouter
} from "react-router-native";

function App() {
  return (
    <NativeRouter>
      {/* The rest of your application goes here */}
    </NativeRouter>
  );
}
```

`<NativeRouter>` is the recommended interface for running React Router in React Native applications

### \<MemoryRouter>
<!--rehype:wrap-class=col-span-2 row-span-2-->

```jsx
import * as React from "react";
import { create } from "react-test-renderer";
import {
  MemoryRouter,
  Routes,
  Route,
} from "react-router-dom";

describe("My app", () => {
  it("renders correctly", () => {
    let renderer = create(
      <MemoryRouter initialEntries={["/users/mjackson"]}>
        <Routes>
          <Route path="users" element={<Users />}>
            <Route path=":id" element={<UserProfile />} />
          </Route>
        </Routes>
      </MemoryRouter>
    );

    expect(renderer.toJSON()).toMatchSnapshot();
  });
});
```

`<MemoryRouter>` internally stores its location in an array. Unlike `<BrowserHistory>` and `<HashHistory>`, it does not rely on external sources, such as the history stack in the browser. This makes it ideal for scenarios where full control over the history stack is required, such as testing

### \<Router>

`<Router>` is a low-level interface shared by all router components such as `<BrowserRouter>` and `<StaticRouter>`. In the case of React, `<Router>` is a context provider that provides routing information to the rest of the application

### \<StaticRouter>

```jsx
import * as React from "react";
import * as ReactDOMServer from "react-dom/server";
import { StaticRouter } from "react-router-dom/server";
import http from "http";

function requestHandler(req, res) {
  let html = ReactDOMServer.renderToString(
    <StaticRouter location={req.url}>
      {/* The rest of your application goes here */}
    </StaticRouter>
  );

  res.write(html);
  res.end();
}

http.createServer(requestHandler)
    .listen(3000);
```
<!--rehype:className=wrap-text-->

See also
---

- [React Router official website](https://reactrouter.com/)
