# MobX
#📥 
%%
#topic
#concept

**Related:**
-  

%%

Comprised of state, actions (modify state), and derivations (values that can be immediately computed from state)

- Can define stores at higher levels in the tree so that you can pass it from one [[React]] component to children
- Can put into context

```JSX
import React from "react";
import {useLocalStore, useObserver } from "mobx-react";

const StoreContext = React.createContext();

// Wrapper component
const StoreProvider = ({children}) => {
	// The mobX store
	const store = useLocalStore( () = ({
		Tasks: [Task1], // State
		addTask: task => { store.Tasks.push(task); }, // Action
		get taskCount () { return store.bugs.length; }// Derivation, called like store.taskCount
	}));

	// Context works by wrapping a provider around children components and giving it a value, this value is accessible by any child components
	return <StoreContext.Provider value={store}>{children}</StoreContext.Provider>
};


export default function App() {
	// Store provider is then wrapped around the rest of the app which is passed as a child
	return (
		<StoreProvider>
			<main>
				<BugsList />
			</main>
		</StoreProvider>
	)

}

// To access the store:
const BugsList = () => {
	const store = React.useContext(StoreContext);


	return (
		{store.bugs.map... blah}
	)
}

```