---
title: UI Toolkit Tutorial
---

# Goal:
In this tutorial, you will learn to creat your first menu UI for your Unity project using the UI Toolkit from Unity

# Recuirements
- You should know some basic C# to create the connections between UI and Code and the funktions for Buttons.
- Also it is help full if you know how styling with CSS works. Even thou you wont write it by your self, it helps you to understand what stuff like margin padding and so on do and you can easily work with it

# Tutorial

## Creating the UI files

Unity’s UI Toolkit is based on three core components: UXML (structure), USS (styling), and C# (logic).

To begin, the required UI files are created:

1. In the Unity Project window, select
Create → UI Toolkit → UI Document.
This creates a .uxml file that defines the structure of the user interface.

2. then, create a stylesheet via
Create → UI Toolkit → StyleSheet (.uss) to control the visual appearance.

3. To display the UI in a scene, add a UI Document component to a GameObject and assign the created UXML file to the Source Asset field. 

4. The UXML file can be opened with the UI Builder by double-clicking it. The UI Builder is Unity’s visual editor for UI Toolkit layouts.

Now you successfully assigned your UI to your game but its still empty so lets change that.

## Creating the UI Structure

Classes in UI Toolkit are used to group UI elements for styling and identification purposes.

UI elements such as Button, Label, or VisualElement are added by dragging them from the Library into the Hierarchy in the UI Builder.

Each UI element can be assigned:

a Name (used to access the element in C#)

one or more Classes (used for styling and organization)

When an element is createt the UI Toolkit updates your UXML file, by writing all the code for you so you dont have to worry, but if you want to do it manualy you can by opening the UXML file and writing your own UXML that could look like this:
```
<Button name="startButton" class="mainButton" text="Start" />
```

## Styling Classes (USS)
