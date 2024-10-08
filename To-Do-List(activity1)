import React, { useState } from 'react';
import { StyleSheet, Text, View, TextInput, TouchableOpacity, FlatList } from 'react-native';

export default function App() {
  const [newTask, setNewTask] = useState('');
  const [tasks, setTasks] = useState([]);
  const [editTaskId, setEditTaskId] = useState(null); // Keeps track of the task being edited
  const [editTaskValue, setEditTaskValue] = useState(''); // Holds the new value during editing
  const [searchQuery, setSearchQuery] = useState(''); // Holds the search input
  const [darkMode, setDarkMode] = useState(false); // Dark mode state

  const addTask = () => {
    if (newTask.trim()) {
      setTasks([...tasks, { id: Date.now().toString(), value: newTask }]);
      setNewTask('');
    }
  };

  const toggleTaskCompleted = (taskId) => {
    setTasks(
      tasks.map((task) =>
        task.id === taskId ? { ...task, completed: !task.completed } : task
      )
    );
  };

  const deleteTask = (taskId) => {
    setTasks(tasks.filter((task) => task.id !== taskId));
  };

  const startEditingTask = (taskId, taskValue) => {
    setEditTaskId(taskId); // Set the ID of the task being edited
    setEditTaskValue(taskValue); // Pre-fill the value for editing
  };

  const submitEditedTask = () => {
    if (editTaskValue.trim()) {
      setTasks(
        tasks.map((task) =>
          task.id === editTaskId ? { ...task, value: editTaskValue } : task
        )
      );
    }
    setEditTaskId(null); // Exit edit mode
    setEditTaskValue(''); // Clear edit value
  };

  const handleInputBlur = () => {
    submitEditedTask(); // Submit when the input field loses focus
  };

  const toggleDarkMode = () => {
    setDarkMode(!darkMode); // Toggle dark mode
  };

  // Filter tasks based on the search query
  const filteredTasks = tasks.filter((task) =>
    task.value.toLowerCase().includes(searchQuery.toLowerCase())
  );

  return (
    <View style={[styles.container, darkMode && styles.darkContainer]}>
      <View style={styles.headerContainer}>
        <Text style={[styles.header, darkMode && styles.darkHeader]}>To-do List</Text>
        <TouchableOpacity onPress={toggleDarkMode} style={styles.toggleButton}>
          <Text style={styles.toggleButtonText}>
            {darkMode ? 'Light Mode' : 'Dark Mode'}
          </Text>
        </TouchableOpacity>
      </View>

      <TextInput
        style={[styles.input, darkMode && styles.darkInput, styles.compactSearchBar]}
        placeholder="Search tasks..."
        placeholderTextColor={darkMode ? "#D3D3D3" : "#D3D3D3"}
        value={searchQuery}
        onChangeText={(text) => setSearchQuery(text)}
      />

      <View style={styles.inputContainer}>
        <TextInput
          style={[styles.input, darkMode && styles.darkInput]}
          placeholder="Add a new task"
          placeholderTextColor={darkMode ? "#D3D3D3" : "#D3D3D3"}
          value={newTask}
          onChangeText={(text) => setNewTask(text)}
        />
        <TouchableOpacity style={styles.addButton} onPress={addTask}>
          <Text style={styles.addButtonText}>Add List</Text>
        </TouchableOpacity>
      </View>

      <FlatList
        keyExtractor={(item) => item.id}
        data={filteredTasks}
        renderItem={({ item }) => (
          <View style={styles.taskItem}>
            <TouchableOpacity
              style={[
                styles.radioCircle,
                item.completed && styles.radioChecked,
                darkMode && styles.darkRadioCircle,
              ]}
              onPress={() => toggleTaskCompleted(item.id)}
            />
            {editTaskId === item.id ? (
              <TextInput
                style={[styles.input, darkMode && styles.darkInput, { flex: 1 }]}
                value={editTaskValue}
                onChangeText={(text) => setEditTaskValue(text)}
                onSubmitEditing={submitEditedTask} // Submit when pressing Enter
                onBlur={handleInputBlur} // Submit when losing focus
                autoFocus // Automatically focus the input when editing starts
              />
            ) : (
              <Text
                style={[
                  item.completed ? styles.completedTask : styles.taskText,
                  darkMode && styles.darkTaskText,
                ]}
              >
                {item.value}
              </Text>
            )}

            <TouchableOpacity onPress={() => startEditingTask(item.id, item.value)} style={styles.editButton}>
              <Text style={styles.editButtonText}>✎</Text>
            </TouchableOpacity>

            <TouchableOpacity onPress={() => deleteTask(item.id)} style={styles.deleteButton}>
              <Text style={styles.deleteButtonText}>🗑</Text>
            </TouchableOpacity>
          </View>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 60,
    paddingHorizontal: 20,
    backgroundColor: '#FFFFFF',
  },
  darkContainer: {
    backgroundColor: '#1F1F1F',
  },
  headerContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginBottom: 20,
  },
  header: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#000000',
  },
  darkHeader: {
    color: '#FFFFFF',
  },
  toggleButton: {
    padding: 10,
  },
  toggleButtonText: {
    color: '#007AFF',
    fontWeight: 'bold',
  },
  inputContainer: {
    flexDirection: 'row',
    alignItems: 'center',
    marginBottom: 20,
  },
  input: {
    flex: 1,
    padding: 10,
    borderWidth: 1,
    borderColor: '#D3D3D3',
    borderRadius: 5,
    marginRight: 10,
    color: '#000000',
  },
  darkInput: {
    borderColor: '#555555',
    backgroundColor: '#333333',
    color: '#FFFFFF',
  },
  compactSearchBar: {
    height: 40, // Reduced height for a more compact bar
    marginBottom: 10, // Adjusted margin to reduce spacing
    paddingHorizontal: 10, // Compact padding for a cleaner look
    borderRadius: 5, // Keep the rounded design
    borderWidth: 1,
    borderColor: '#D3D3D3',
    backgroundColor: darkMode ? '#333333' : '#FFFFFF', // Adjust based on dark/light mode
  },
  addButton: {
    backgroundColor: '#000000',
    paddingVertical: 10,
    paddingHorizontal: 20,
    borderRadius: 5,
  },
  addButtonText: {
    color: '#FFFFFF',
    fontWeight: 'bold',
    fontSize: 16,
  },
  taskItem: {
    flexDirection: 'row',
    alignItems: 'center',
    marginBottom: 10,
  },
  radioCircle: {
    height: 24,
    width: 24,
    borderRadius: 12,
    borderWidth: 2,
    borderColor: '#000000',
    marginRight: 10,
  },
  darkRadioCircle: {
    borderColor: '#FFFFFF',
  },
  radioChecked: {
    backgroundColor: '#FFA500',
  },
  taskText: {
    fontSize: 18,
    color: '#000000',
    flex: 1,
  },
  darkTaskText: {
    color: '#FFFFFF',
  },
  completedTask: {
    fontSize: 18,
    color: 'gray',
    textDecorationLine: 'line-through',
    flex: 1,
  },
  editButton: {
    paddingHorizontal: 10,
  },
  editButtonText: {
    color: '#FFA500',
    fontSize: 18,
  },
  deleteButton: {
    paddingHorizontal: 10,
  },
  deleteButtonText: {
    color: 'red',
    fontSize: 18,
  },
});
