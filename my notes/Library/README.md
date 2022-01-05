# Make and publish react component library
<summary>Make the package
        <details>
          <ul>
  <li>create an empty folder</li>
  <li>open that folder in vscode and in the terminal type <code>npm init</code></li>
  <li>folder structure for the library
    <ul>
      <li>src
        <ul>
          <li>components
            <ul>
              <li>[ComponentName]
                <ul>
                  <li>index.js
                    <ul>
                      <li>Contents <code>export * from './[ComponentName]'</code></li>
                    </ul>
                  </li>
                  <li>[ComponentName].js
                    <ul>
                      <li>Contents <pre>export const TextBox = () => {
    return (
        <>
            <div>
            See this file's raw code for the actual code
                <input type='text' />
            </div>
        </>
    )
}</pre></li>
                    </ul>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li>index.js
          <ul>
                      <li>Contents <pre>export * from './components/[componentName1]'
export * from './components/[componentName2]'</pre></li>
                    </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li>install the following dependencies
    <ul>
      <code>npm install --save-dev react react-dom</code>
    </ul>
  </li>
  <li>open <code>package.json</code> file and add peer dependencies
    <ul>
      <pre>"peerDependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  },</pre>
    </ul>
  </li>
  <li>install storybook (live-server version of libraries)<code>npx sb init</code></li>
  <li>right-click on the stories and create a file <code>Playground.stories.js</code>
    <ul>
      <li>Contents
        <pre>import React from "react";
import { storiesOf } from '@storybook/react'
import { SelectBox, TextBox } from '../../dist'

const stories = storiesOf('Kamsoft', module)

stories.add('Lib Test', () => {
    return (<>Your Logic here</>)
})
</pre>
      </li>
    </ul>
  </li>
      <li>run the command <code>npm run storybook</code></li>
    </ul>
        </details>
      </summary>
      <summary>Publish the package
        <details>
<ul>
 <li>install this packages <code>npm install rollup rollup-plugin-babel @rollup/plugin-node-resolve rollup-plugin-peer-deps-external --save-dev</code></li>
  <li><code>npm install --save-dev @babel/preset-react</code></li>
  <li><code>npm install --save-dev rollup-plugin-postcss</code></li>
  <li><code>npm install --save-dev rollup-plugin-terser</code></li>
  <li>right click on the src folder and create file <code>rollup.config.js</code>
    <ul>
      <li>contents
        <ul>
          <pre>import babel from 'rollup-plugin-babel'
import resolve from '@rollup/plugin-node-resolve'
import external from 'rollup-plugin-peer-deps-external'
import { terser } from 'rollup-plugin-terser';
import postcss from 'rollup-plugin-postcss'

export default [
    {
        input: './src/index.js',
        output: [
            {
                file: 'dist/index.js',
                format: 'cjs'
            },
            {
                file: 'dist/index.es.js',
                format: 'es',
                exports: 'named'
            }
        ],
        plugins: [
            postcss({
                plugins: [],
                minimize: true,
            }),
            babel({
                exclude: 'node_modules/**',
                presets: [["@babel/preset-react", { runtime: "automatic" }]]
            }),
            external(),
            resolve(),
            terser(),
        ]
    }
]</pre>
        </ul>
      </li>
    </ul>
  </li>
  <li>edit <code>package.json</code> add
    <pre>"scripts": {
    "build-lib": "rollup -c"
  }</pre>
  </li>
  <li>change <code>package.json</code>
    <ul>
      <pre> "main": "dist/index.js",
  "module": "dist/index.es.js",</pre>
    </ul>
  </li>
  <li>and finally <code>npm publish</code></li>
</ul>
  </details>
      </summary>
