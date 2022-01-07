# Set up NextJs in react
<ul>
  <li>Open your folder in Vscode editor</li>
  <li>run the command <code>npm init</code></li>
  <li>install these packages <code>npm install next react react-dom</code></li>
  <li>Open package.json and add the following scripts:
    <pre>"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}</pre></li>
  <li>add this following dependencies in <code>package.json</code>
    <pre>"dependencies": {
    "next": "^12.0.7",
    "next-redux-wrapper": "^7.0.5",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-redux": "^7.2.4",
    "redux": "^4.1.1",
    "redux-devtools-extension": "^2.13.9",
    "redux-logger": "^3.0.6",
    "redux-persist": "^6.0.0",
    "redux-thunk": "^2.3.0",
    "reselect": "^4.0.0"
  }</pre>
  </li>
  <li>run <code>npm install</code></li>
  <li>create a <code>pages</code> directory in your project</li>
  <li>create a file inside <code>pages</code> <code>index.js</code>(this will be where your root data will be)</li>
  <li>create another file inside <code>pages</code> <code>_app.js</code>
    <ul>Contents (see the source code of this page for correct code)
      <summary>With Redux
        <details><pre>import React from 'react'
import { useStore } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react'
import { wrapper } from '../redux/store';
import { withRouter, Router } from 'next/router'
import "../components/Home.css"
function App({ Component, pageProps }) {
    const store = useStore((state) => state);
    return (
        <>
            <PersistGate persistor={store.__persistor} >
                <Component {...pageProps} />
            </PersistGate>
        </>
    )
}

App.getInitialProps = async ({ Component, ctx }) => {
    const pageProps = Component.getInitialProps ? await Component.getInitialProps(ctx) : {};
    return { pageProps: pageProps };
}

export default withRouter(wrapper.withRedux(App))
</pre></details>
      </summary>
      <summary>Without Redux
        <details><pre>import React from "react";
function App({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
    </>
  );
}

App.getInitialProps = async ({ Component, ctx }) => {
  const pageProps = Component.getInitialProps
    ? await Component.getInitialProps(ctx)
    : {};
  return { pageProps: pageProps };
};

export default App;
</pre></details>
      </summary>
    </ul>
  </li>
  <li>create a folder <code>components</code> which will have all the components in them</li>
  <li>create a folder <code>public</code> which will have all the css in them</li>
  <li>inside <code>pages</code> create [routeName] folder which will then be called by the router to move between the pages</li>
  <li>inside each [routeName] folder there will be an <code>index.js</code> file which will contain all the contents of that page</li>
</ul>
