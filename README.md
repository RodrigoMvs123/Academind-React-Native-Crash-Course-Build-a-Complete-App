# Academind-React-Native-Crash-Course-Build-a-Complete-App

https://www.youtube.com/watch?v=VozPNrt-LfE


React Native Crash Course | Build a Complete App

React Native Crash Course | Build a Complete App


What is React Native ?

React.js + React Native -> Real Native Mobile Apps ( IOS / Android ) 

React.js 
R: A JavaScript library for building user interfaces. 
Typically used for web development.
React-Dom adds web support.

React Native 
A collection of “especial” React components 
Components are compiled to native UI elements 
Native platform APIs exposed to JavaScript 

React + React Native App 

const App = props => {
return(
<View> 
<Text>Hello there!</Text>
);
};

https://reactnative.dev/
https://reactnative.dev/docs/environment-setup
install -g expo-cli 

Expo CLI ( “Expo” )    -    React Native CLI 


https://nodejs.org/en/download/

Terminal 
npm install -g expo-cli 
Password: 
Clear
Expo ( https://expo.dev/ ) 
expo init RNCourse 

Managed Workflow 
> blank …// ( “ it will create an new expo reactive native project”) 

https://code.visualstudio.com/

Open a folder 

App.js

import { StatusBar } from ‘expo-status-bar’; 
import { StyleSheet, Text, View } from ‘react-native’;

export default function App () {
return ( 
<View style={styles.container}>
<Text>Hello World!</Text>

<StatusBar style=”auto”/>
</View>
);
}


const style = StyleSheet.create ({
container: {
flex: 1,
backgroundColor: ‘#fff’,
alignItems: ‘center’,
},
});
 
Donwload 
Expo Go ( Cellphone ) 
Terminal 
npm start 
Simulator app device  

Download Android Studio 
https://developer.android.com/studio?hl=pt&gclid=Cj0KCQjwnNyUBhCZARIsAI9AYlFOctZW_HsR1xXx7TMSt-YmI1TQ8RxQvEDRQl5D1IaJWnktnna3KUAaAmhOEALw_wcB&gclsrc=aw.ds

Select a system image 
Open an Emulator 
API 32 Version arm64-v8a

The Basics 
Diving Into the Core Concepts 
Using React Native Components & Building UIs 
Styling React Native Apps 

Adding Interactivity & Managing State 

App.js
Terminal npm install 

https://reactnative.dev/docs/components-and-apis

“Core” Components ( Built Into React Native ) 
“Translation” to native UI widgets is provided by React Native
<View/>
<Text/>
<Button/>
<TextInput/>
<Image/>
<.../>

Your UI & Custom Components 
Combination of “Core” components & other build-in components
const MyTitle = props => {
return ( 
<View> 
<Text> {props.title}</Text> 
</View> 
);
};


Styling React Native Apps 
There is no CSS! 
Inline Styles 
StyleSheet Objects 
Written in JavaScript 


Layouts & Flexbox 

Layouts are (typically) created with Flexbox 
Very similar to browser CSS flexbox! 
Elements are positioned inside of containers 
Positioning is controlled via style settings applied to the element container 

flex: 1 
flex:Direction: ‘column’, / ‘row’ 
justifyContent: ‘flex-start’, / ‘space-between’
alignItems: ‘flex-start’ 

Cross Axis / Main Axis 


ScrollView · React Native

  #

import { useState } from 'react'; 
import { 
StyleSheet, 
View,  
FlatList,
Button
} from ‘react-native’;
import { StatusBar } from 'expo-status-bar'; 

import GoalItem from './componentsGoalItem';
import GoalInput from './components/GoalInput';

export default function App () {
const [modalIsVisible, setMOdalIsVisible] = useState(false);
const [courseGoals, setCourseGoals] = useState([]);

function startAddGoalHandler () {
 setModalIsVisible(true);
}

function endAddGoalHandler () {
setModalIsVisible(false);
}

function addGoalHandler(enteredGoalText) {
setCourseGoals((currentCourseGoals =>[
...currentCourseGoals, 
{text: enteredGoalText, id:Math.radom().toString()},
]);
 endAddGoalHandler();
}


function deleteGoalHandler(id) {
setCourseGoals((currentCourseGoals => { 
return currentCourseGoals.filter((goal) => goal.id !== id);
});
}


  return ( 
<>
<StatusBar style="light" />
    <View style={styles.appContainer}>
      <Button title='Add New Goal' 
              color="#a065ec" />
              onPress={startAddGoalHandler}
 <GoalInput 
     visible={modalIsVisible} 
     onAddGoal={addGoalHandler}
     onCancel={endAddGoalHandler}
/>
          </View style={styles.goalsContainer}>
       <FlatList 
 data={courseGoal} 
renderItem={(itemData)   => {

return <GoalItem 
  text={itemData.item.text} 
  id={itemData.item.id}
  onDeleteItem={deleteGoalHandler}
 />;
);
}} 
keyExtractor={(item, index) => {
return item.id; 

}}
alwaysBounceVertical={false}
/> 
</View>
</View>
</>
    );
}


const style = StyleSheet.create ({
 appContainer: {
    flex:1,
    paddingTop: 50,
    paddingHorizontal: 16
    
 } 
 
    goalsContainer: {
       flex:5 
}


});

}


#


import { useState } from 'react';
import { View, 
TextInput, 
Button, 
StyleSheet, 
Modal, 
Image 
} from 'react-native'; 

function GoalInput(props) { 

const [enteredGoalText, setEnteredGoalText] = useState('');

function goalInputHandler(enteredText) {
 setEnteredGoalText(enteredText); 
}

function addGoalHandler () {

props.onAddGoal(enteredGoalText);
setEnteredGoalText('');
}

return ( 
<Modal visible={props.visible} animationType="slide"> 
<View style={styles.inputContainer}>
<Image style={styles.image} source={require('../assets/images/goal.png')}/>
         <TextInput 
style={styles.textInput} 
placeholder="Your course goal!" 
onChangeText={goalInputHandler} 
value={enteredGoalText}
/>
<View style={styles.buttonContainer}> 
<View style>
< Button title= "Cancel" onPress={props.onCancel} color='#f31282' />
</View>  
<View style={style.button} >
 <Button title="Add Goal" onPress={addGoalHandler} color='#5e0acc' />
</View>
</View>
        
</View>
</Modal>
);
}


export default GoalInput; 

const styles = StyleSheet.create({

inputContainer: {
    flex:1,  
    justifyContent: 'center',
    alignItems: 'center',
    padding: 16,
    backgroundColor: '#311b6b'
 },

image: {
width 100,
height 100,
margin: 20
},

  TextInput: {
    borderWidth: 1,
    borderColor: '#e4d0ff',
    backgroundcolor: '#e4d0ff',
    color: '#120438',
    borderRadius: 6,
    width: '100%',
    padding: 16,
     
  },
buttonContainer: {
marginTop16,
flexDirection:'row'
}
button:{
width: 100,
marginHorizontal: 8 
}
});

#

import {StyleSheet, View, Text, Pressable } from 'react-native';

function GoalItem(props) {


return 

<View key={goal} style={styles.goalItem}>
<Pressable android_ripple={{color:'#210644'}} onPress={props.onDeleteItem.bind(this, props.id)}
style={({pressed) => pressed && styles.pressedItem }
>

<Text style={styles.goalText}>{props.text}</Text>
</View>
</Pressable>

};

export default GoalItem;

const styles = StyleSheet.create({
goalItem:{
margin:8, 
borderRadius: 6,
backgroundColor: '#5e0acc',
color: 'white'
 
},

pressedItem: {
opacity: 0.5
},
goalText: {
color: 'white',
padding 8,
},
});

#









  





