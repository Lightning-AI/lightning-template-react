# React Template Application in 3 steps

## 1. Setup

To run the following application, you would need to install

- [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- [yarn](https://classic.yarnpkg.com/lang/en/docs/install)

## 2. Build the React Application

To build the react website, simply run the following commands

```bash
cd react
yarn install
yarn build
```

## 3. Run Your React Application

Use lightning cli to run your application.

```bash
cd ..
lightning build app app.py
```

#### Application Folder Structure

You would find the following structure in the folder `/react`.

```
react
├── dist
├── index.html
├── node_modules
├── package.json
├── src
│   ├── App.css
│   ├── App.tsx
│   ├── hooks
│   ├── index.css
│   ├── main.tsx
│   ├── types
│   └── vite-env.d.ts
├── tsconfig.json
├── tsconfig.node.json
├── vite.config.ts
└── yarn.lock
```

In the file `App.tsx`, you can find the following. By using `useLightningState` and `updateLightningState` in your React component,
you can interact with your application state.

```js
import { useLightningState } from "./hooks/useLightningState";
import cloneDeep from "lodash/cloneDeep";

function App() {
  const { lightningState, updateLightningState } = useLightningState();

  const modify_and_send_back_the_state = async (event: ChangeEvent<HTMLInputElement>) => {
    if (lightningState) {
      const newLightningState = cloneDeep(lightningState);
      // Update the state and send it back.
      newLightningState.flows.counter += 1

      updateLightningState(newLightningState);
    }
  };

  return (
    <div className="App">
    </div>
  );
}

export default App;
```

In the file `app.py`, simply point the `StaticWebFrontend` to the `dist/` folder generated by yarn after building your react website.

```py
from lightning.frontend import StaticWebFrontend


class ReactUI(LightningFlow):

    def configure_layout(self):
        return StaticWebFrontend(Path(__file__).parent / "react/dist")
```
