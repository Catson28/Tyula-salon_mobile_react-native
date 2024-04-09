# Basic Operations TSX

12min

# React Native CRUD tutorial

## Introduction

Storing data on Parse is built around Parse.Object class. Each Parse.Object contains key-value pairs of JSON-compatible data. This data is schemaless, which means that you don’t need to specify ahead of time what keys exist on each Parse.Object. You can simply set whatever key-value pairs you want, and our backend will store it.

You can also specify the datatypes according to your application needs and persist types such as number, boolean, string, DateTime, list, GeoPointers, and Object, encoding them to JSON before saving. Parse also supports store and query relational data by using the types Pointers and Relations.

In this guide, you will learn how to perform basic data operations through a CRUD example app, which will show you how to create, read, update and delete data from your Parse server database in React Native. You will first create your component functions for each CRUD operation, using them later in a complete screen layout, resulting in a to-do list app.

```tsx
```



## Prerequisites

**To complete this tutorial, you will need:**

- A React Native App created and connected to [Back4App](https://www.back4app.com/docs/react-native/parse-sdk/react-native-sdk).
- If you want to test/use the screen layout provided by this guide, you should set up thereact-native-paper﻿[library](https://github.com/callstack/react-native-paper).

## Goal

To build a basic CRUD application in React Native using Parse.

## 1 - Creating data objects

The first step to manage your data in your Parse database is to have some on it. Let’s now make a createTodo function that will create a new instance of Parse.Object with the “Todo” subclass. The Todo will have a title(string) describing the task and a done(boolean) field indicating if the task is completed.



TodoList.tsx

```tsx
1	const createTodo = async function (): Promise<boolean> {
2	  // This value comes from a state variable
3	  const newTodoTitleValue: string = newTodoTitle;
4	  // Creates a new Todo parse object instance
5	  let Todo: Parse.Object = new Parse.Object('Todo');
6	  Todo.set('title', newTodoTitleValue);
7	  Todo.set('done', false);
8	  // After setting the todo values, save it on the server
9	  try {
10	    await Todo.save();
11	    // Success
12	    Alert.alert('Success!', 'Todo created!');
13	    // Refresh todos list to show the new one (you will create this function later)
14	    readTodos();
15	    return true;
16	  } catch (error) {
17	    // Error can be caused by lack of Internet connection
18	    Alert.alert('Error!', error.message);
19	    return false;
20	  };
21	};
```



﻿

Notice that if your database does not have a Todo table (or subclass) in it yet, Parse will create it automatically and also add any columns set inside the Parse.Object instance using the Parse.Object.set() method, which takes two arguments: the field name and the value to be set.

## 2 - Reading data objects

After creating some data in your database, your application can now be able to read it from the server and show it to your user. Go ahead and create a readTodos function, which will perform a Parse.Query, storing the result inside a state variable.

TypeScript

```tsx
1	const readTodos = async function (): Promise<boolean> {
2	  // Reading parse objects is done by using Parse.Query
3	  const parseQuery: Parse.Query = new Parse.Query('Todo');
4	  try {
5	    let todos: Parse.Object[] = await parseQuery.find();
6	    // Be aware that empty or invalid queries return as an empty array
7	    // Set results to state variable
8	    setReadResults(todos);
9	    return true;
10	  } catch (error) {
11	    // Error can be caused by lack of Internet connection
12	    Alert.alert('Error!', error.message);
13	    return false;
14	  };
15	};
```





The Parse.Query class is very powefull, many constraints and orderings can be applied to your queries. For now, we will stick to this simple query, which will retrieve every saved Todo object.

## 3 - Updating data objects

Updating a Parse.Object instance is very similar to creating a new one, except that in this case, you need to assign the previously created objectId to it and then save, after setting your new values.

TypeScript

```tsx
1	const updateTodo = async function (
2	  todoId: string,
3	  done: boolean,
4	): Promise<boolean> {
5	  // Create a new todo parse object instance and set todo id
6	  let Todo: Parse.Object = new Parse.Object('Todo');
7	  Todo.set('objectId', todoId);
8	  // Set new done value and save Parse Object changes
9	  Todo.set('done', done);
10	  try {
11	    await Todo.save();
12	    // Success
13	    Alert.alert('Success!', 'Todo updated!');
14	    // Refresh todos list
15	    readTodos();
16	    return true;
17	  } catch (error) {
18	    // Error can be caused by lack of Internet connection
19	    Alert.alert('Error!', error.message);
20	    return false;
21	  };
22	};
```

﻿

Since this example app represents a to-do list, your update function takes an additional argument, the done value, which will represent if the specific task is completed or not.

## 4 - Deleting data objects

To delete a data object, you need to call the .destroy() method in the Parse.Object instance representing it. Please be careful because this operation is not reversible.



TypeScript

```tsx
1	const deleteTodo = async function (todoId: string): Promise<boolean> {
2	  // Create a new todo parse object instance and set todo id
3	  let Todo: Parse.Object = new Parse.Object('Todo');
4	  Todo.set('objectId', todoId);
5	  // .destroy should be called to delete a parse object
6	  try {
7	    await Todo.destroy();
8	    Alert.alert('Success!', 'Todo deleted!');
9	    // Refresh todos list to remove this one
10	    readTodos();
11	    return true;
12	  } catch (error) {
13	    // Error can be caused by lack of Internet connection
14	    Alert.alert('Error!', error.message);
15	    return false;
16	  };
17	};
```



﻿

Let´s now use these four functions in a complete component, so you can test it and make sure that every CRUD operation is working properly.

## 5 - Using CRUD in a React Native component

Here is the complete component code, including styled user interface elements, state variables, and calls to your CRUD functions. You can create a separate component in a file called TodoList.js/TodoList.tsx containing the following code or add it to your main application file (App.js/App.tsx or index.js):



TodoList.tsx

```tsx
	import React, {FC, ReactElement, useState} from 'react';
	import {
	  Alert,
	  View,
	  SafeAreaView,
	  Image,
	  ScrollView,
	  StatusBar,
	  StyleSheet,
	  TouchableOpacity,
	} from 'react-native';
	import Parse from 'parse/react-native';
	import {
	  List,
	  Title,
	  IconButton,
	  Text as PaperText,
	  Button as PaperButton,
	  TextInput as PaperTextInput,
	} from 'react-native-paper';
	
	export const TodoList: FC<{}> = ({}): ReactElement => {
	  // State variables
	  const [readResults, setReadResults] = useState<[Parse.Object]>();
	  const [newTodoTitle, setNewTodoTitle] = useState('');
	
	  // Functions used by the screen components
	  const createTodo = async function (): Promise<boolean> {
	    // This value comes from a state variable
	    const newTodoTitleValue: string = newTodoTitle;
	    // Creates a new Todo parse object instance
	    let Todo: Parse.Object = new Parse.Object('Todo');
	    Todo.set('title', newTodoTitleValue);
	    Todo.set('done', false);
	    // After setting the todo values, save it on the server
	    try {
	      await Todo.save();
	      // Success
	      Alert.alert('Success!', 'Todo created!');
	      // Refresh todos list to show the new one (you will create this function later)
	      readTodos();
	      return true;
	    } catch (error) {
	      // Error can be caused by lack of Internet connection
	      Alert.alert('Error!', error.message);
	      return false;
	    }
	  };
	
	  const readTodos = async function (): Promise<boolean> {
	    // Reading parse objects is done by using Parse.Query
	    const parseQuery: Parse.Query = new Parse.Query('Todo');
	    try {
	      let todos: Parse.Object[] = await parseQuery.find();
	      // Be aware that empty or invalid queries return as an empty array
	      // Set results to state variable
	      setReadResults(todos);
	      return true;
	    } catch (error) {
	      // Error can be caused by lack of Internet connection
	      Alert.alert('Error!', error.message);
	      return false;
	    }
	  };
	
	  const updateTodo = async function (
	    todoId: string,
	    done: boolean,
	  ): Promise<boolean> {
	    // Create a new todo parse object instance and set todo id
	    let Todo: Parse.Object = new Parse.Object('Todo');
	    Todo.set('objectId', todoId);
	    // Set new done value and save Parse Object changes
	    Todo.set('done', done);
	    try {
	      await Todo.save();
	      // Success
	      Alert.alert('Success!', 'Todo updated!');
	      // Refresh todos list
	      readTodos();
	      return true;
	    } catch (error) {
	      // Error can be caused by lack of Internet connection
	      Alert.alert('Error!', error.message);
	      return false;
	    }
	  };
	
	  const deleteTodo = async function (todoId: string): Promise<boolean> {
	    // Create a new todo parse object instance and set todo id
	    let Todo: Parse.Object = new Parse.Object('Todo');
	    Todo.set('objectId', todoId);
	    // .destroy should be called to delete a parse object
	    try {
	      await Todo.destroy();
	      Alert.alert('Success!', 'Todo deleted!');
	      // Refresh todos list to remove this one
	      readTodos();
	      return true;
	    } catch (error) {
	      // Error can be caused by lack of Internet connection
	      Alert.alert('Error!', error.message);
	      return false;
	    }
	  };
	
	  return (
	    <>
	      <StatusBar backgroundColor="#208AEC" />
	      <SafeAreaView style={Styles.container}>
	        <View style={Styles.header}>
	          <Image
	            style={Styles.header_logo}
	            source={ {
	              uri:
	                'https://blog.back4app.com/wp-content/uploads/2019/05/back4app-white-logo-500px.png',
	            } }
	          />
	          <PaperText style={Styles.header_text_bold}>
	            {'React Native on Back4App'}
	          </PaperText>
	          <PaperText style={Styles.header_text}>{'Product Creation'}</PaperText>
	        </View>
	        <View style={Styles.wrapper}>
	          <View style={Styles.flex_between}>
	            <Title>Todo List</Title>
	            {/* Todo read (refresh) button */}
	            <IconButton
	              icon="refresh"
	              color={'#208AEC'}
	              size={24}
	              onPress={() => readTodos()}
	            />
	          </View>
	          <View style={Styles.create_todo_container}>
	            {/* Todo create text input */}
	            <PaperTextInput
	              value={newTodoTitle}
	              onChangeText={text => setNewTodoTitle(text)}
	              label="New Todo"
	              mode="outlined"
	              style={Styles.create_todo_input}
	            />
	            {/* Todo create button */}
	            <PaperButton
	              onPress={() => createTodo()}
	              mode="contained"
	              icon="plus"
	              color={'#208AEC'}
	              style={Styles.create_todo_button}>
	              {'Add'}
	            </PaperButton>
	          </View>
	          <ScrollView>
	            {/* Todo read results list */}
	            {readResults !== null &&
	              readResults !== undefined &&
	              readResults.map((todo: Parse.Object) => (
	                <List.Item
	                  key={todo.id}
	                  title={todo.get('title')}
	                  titleStyle={
	                    todo.get('done') === true
	                      ? Styles.todo_text_done
	                      : Styles.todo_text
	                  }
	                  style={Styles.todo_item}
	                  right={props => (
	                    <>
	                      {/* Todo update button */}
	                      {todo.get('done') !== true && (
	                        <TouchableOpacity
	                          onPress={() => updateTodo(todo.id, true)}>
	                          <List.Icon
	                            {...props}
	                            icon="check"
	                            color={'#4CAF50'}
	                          />
	                        </TouchableOpacity>
	                      )}
	                      {/* Todo delete button */}
	                      <TouchableOpacity onPress={() => deleteTodo(todo.id)}>
	                        <List.Icon {...props} icon="close" color={'#ef5350'} />
	                      </TouchableOpacity>
	                    </>
	                  )}
	                />
	              ))}
	          </ScrollView>
	        </View>
	      </SafeAreaView>
	    </>
	  );
	};
	
	// These define the screen component styles
const Styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#FFF',
  },
  wrapper: {
    width: '90%',
    alignSelf: 'center',
  },
  header: {
    alignItems: 'center',
    paddingTop: 10,
    paddingBottom: 20,
    backgroundColor: '#208AEC',
  },
  header_logo: {
    width: 170,
    height: 40,
    marginBottom: 10,
    resizeMode: 'contain',
  },
  header_text_bold: {
    color: '#fff',
    fontSize: 14,
    fontWeight: 'bold',
  },
  header_text: {
    marginTop: 3,
    color: '#fff',
    fontSize: 14,
  },
  flex_between: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
  },
  create_todo_container: {
    flexDirection: 'row',
  },
  create_todo_input: {
    flex: 1,
    height: 38,
    marginBottom: 16,
    backgroundColor: '#FFF',
    fontSize: 14,
  },
  create_todo_button: {
    marginTop: 6,
    marginLeft: 15,
    height: 40,
  },
  todo_item: {
    borderBottomWidth: 1,
    borderBottomColor: 'rgba(0, 0, 0, 0.12)',
  },
  todo_text: {
    fontSize: 15,
  },
  todo_text_done: {
    color: 'rgba(0, 0, 0, 0.3)',
    fontSize: 15,
    textDecorationLine: 'line-through',
  },
});

```





```tsx

```





```tsx

```





```tsx

```





```tsx

```



## 

If your component is properly set up, you should see something like this after building and running the app:

![Document image](https://archbee.imgix.net/yD3zCY-NNBBIfd0uqcfR5/51-3FbSNWXp3gY__jZoBZ_image.png)

﻿

Go ahead and add some to-do’s by typing its titles in the input box one at a time and pressing on the Add button. Note that after every successful creation, the createTodo function triggers the readTodos one, refreshing your task list automatically. You should now have a sizeable to-do list like this:

![Document image](https://archbee.imgix.net/yD3zCY-NNBBIfd0uqcfR5/HWcos8Q-b6m_tnv3S574C_image.png)

﻿

You can now mark your tasks as done by clicking in the checkmark beside it, causing their done value to be updated to true and changing its icon status on the left.

![Document image](https://archbee.imgix.net/yD3zCY-NNBBIfd0uqcfR5/bmIa9FjvqA_eGDRbKnfhY_image.png)

﻿

The only remaining data operation is now the delete one, which can be done by pressing on the trash can icon at the far right of your to-do list object. After successfully deleting an object, you should get an alert message like this:

![Document image](https://archbee.imgix.net/yD3zCY-NNBBIfd0uqcfR5/FmDMU0AzdKiS_cN8b3sTu_image.png)

﻿

## Conclusion

At the end of this guide, you learned how to perform basic data operations (CRUD) in Parse on React Native. In the next guide, we will show you which data types are supported in Parse and how to use them.
