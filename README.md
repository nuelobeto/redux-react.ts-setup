FOLDER STRUCTURE: 
- src
  - app
    - store.ts
    - hooks.ts
  - features
    - resource: eg: todos
      - resourceslice.js eg: todoSlice.ts
  - components

STEPS: 
1. install react.ts: npm create vite@latest app_name
2. select react > react_ts
3. install dependencies: npm install
4. install redux toolkit and react-redux: npm i @reduxjs/toolkit react-redux
5. import {Provider} from react-redux inside main.tsx
6. create slices and reducers: 
   6a. import { createSlice, PayloadAction } from "@reduxjs/toolkit";
   6b. create state type: e.g: type InitialStateType = {abcd: number};
   6c. create state using state type: e.g: const initialState: InitialStateType ={abcd: 10}
   6d. create slice: const xxxSlice = createSlice({
			name: "name_of_resources",
			initialState,
			reducers: {
			    actionName: (state, action: PayloadAction<payloadType>) => {
			      // update state
			      e.g: state.abcd = action.payload
			    }
			  }
			})
			
			export default xxxSlice.reducer
			// export all action names
		        export const {actionName} = xxxSlice.actions
7. create store:
   7a. import { configureStore } from "@reduxjs/toolkit";
   7b. import the xxxSlice created as xxxReducer
   7c. const store = configureStore({
	 reducer: {
	   // name the reducer for the slice
	   xxx: xxxReducer  
         }
       })
       export default store
       export type RootState = ReturnType<typeof store.getState>
       export type AppDispatch = typeof store.dispatch
8. create useSelector and useDispatch typed hooks:
   8a. import { TypedUseSelectorHook, useDispatch, useSelector } from "react-redux"
   8b. import type { RootState, AppDispatch } from "./store"
   8c. export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector
   8d. export const useAppDispatch = () => useDispatch<AppDispatch>()
9. import store in main.tsx
10. wrap App with Provider: <Provider store={store}><App /></Provider>
11. import useAppSelector and useAppDispatch along side with the actions in the necessary components:
    11a. import { useAppSelector, useAppDispatch } from "../../app/hooks";
    11b. import { actionName1, actionName2 } from "./xxxSlice";
    11c. initialize useAppSelector: const customName = useAppSelector((state) => state.xxx.abcd)
    11d. initialize useAppDispatch: const dispatch = useAppDispatch()
