README_DAVID.md

Course 4, Week 3, 4.3-1 | Hands-on Lab:  React Redux

//Note to self - be careful which file you are updating.  Working directory makes a difference.  There is more than one index.js.  

//Objective:

//After completing this lab, you will be able to use state management to increment the counter using Redux. Redux library has all that it requires for store management while react-redux binds react and redux libraries together. It centralizing an application’s state and logic, thereby making the state accessible outside of the component.

//The store management with redux has 3 main components:

//Actions - are blocks of information that send data from your application to your store. Actions must have a type property that indicates the type of action being performed.

//Reducers -Reducers specify how the application’s state changes in response to actions sent to the store.

//Store -The Store is the object that brings the action and reducer together. The store has the following responsibilities: Holds application state; Allows access to state; Allows state to be updated via dispatch(action);

//Hands-on Lab

//Go to the git repository https://github.com/ibm-developer-skills-network/uqwxd-react_labs.git that contains the starter code needed for this lab and clone the repository.

cd /home/project

git clone https://github.com/ibm-developer-skills-network/uqwxd-react_labs.git

cd uqwxd-react_labs/react-redux-master

//In this application that we are building, to learn the use of redux with react, we will have one MainPanel component which contains two internal Components, MyButton and DivPanel.

//MyButton is a button component. The application maintains a counter which keeps track of the number of times the button is clicked. The value of this counter will be displayed in the DivPanel. The content of DivPanel will be automatically refreshed everytime the counter value changes. These are effectively two different components.

//Install the libraries required for your application using the below command. Once installed, verify if the required packages are installed in the package.json file.

npm install --save -s redux react-redux react react-dom react-scripts react-service-worker web-vitals

//The only action you are going to perform is incrementing of the counter. Edit src/action/index.js and paste the following code in it.  

const increment = (val) => {
    return {
        type : 'INCREMENT',
        inc : val
    }
}

export default increment;

//val is the value you want to increase the counter by everytime the button is clicked. Now that you have your action which defines what is to be done, you will create the reducers which will define how it is done.

//Edit src/reducers/index.js and paste the following code in it. Click the button below to open index.js.

import {combineReducers} from 'redux'

const counter = (state=0,action)=>{
    if(action.type === 'INCREMENT') {
        //This will increase the value of counter by the value passed to the increment method
        return state+action.inc;
    }
    //Returns the current value of the counter
    return state;
}

const myReducers = combineReducers({counter});

export default myReducers;

//Edit src/components/MyButton.js and paste the following code in it. Click the button below to open MyButton.js.

import React from 'react'
import { useDispatch} from 'react-redux';
import increment from '../actions'

const MyButton = ()=>{
    let dispatch = useDispatch();
    return (
        <button onClick={()=>dispatch(increment(1))}>Increase counter</button>
    );
}

export default MyButton;

//useDispatch dispatches the event to the store and finds out what action is to be taken and uses the appropriate reducer to do the same.

//Edit src/components/DivPanel.js and paste the following code in it. Click the button below to open DivPanel.js.

import React from 'react'
import { useSelector } from 'react-redux';

const DivPanel = () =>{
    let counterVal = useSelector(state => state.counter)
    return (
        <div>
            The present value of counter is {counterVal}
        </div>
    );
}

export default DivPanel;

//useSelector is used to select the state from the store whose value you want to access.

//Edit src/components/MainPanel.js and paste the following code in it. Click the button below to open MainPanel.js.

import React from 'react'
import MyButton from './MyButton'
import DivPanel from './DivPanel';

const MainPanel = ()=>{
    return (
        <div>
            This is main panel <MyButton></MyButton>
            <DivPanel></DivPanel>
        </div>
    );
}
export default MainPanel;

//You have all the panels created. Now let’s render the MainPanel through App.js. App.js contains the code give below. 

import React from 'react';
import MainPanel from './components/MainPanel';

function App() {
  return (
      <div>
        <MainPanel/>
      </div>
    );
}

export default App;

//Now for the final set up of the react application. You need to create and set up the store, where you can manage all the states (in this application, the counter) you want. This is done in the main index.js in the src folder.

//In the terminal, ensure you are in the react-redux directory and run the following command to start the server and run the application.

npm start

