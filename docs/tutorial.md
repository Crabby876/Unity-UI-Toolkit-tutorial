---
title: UI Toolkit Tutorial
---

# Goal:
In this tutorial, you will learn to creat your first menu UI for your Unity project using the UI Toolkit from Unity

# Recuirements
- You should be confident using Unity.
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

<img width="443" height="978" alt="image" src="https://github.com/user-attachments/assets/d6b5bfab-7c0c-421e-a3da-db796a4e349f" />


Each UI element can be assigned:

- a Name (used to access the element in C#)

- one or more Classes (used for styling and organization)

When an element is createt the UI Toolkit updates your UXML file, by writing all the code for you so you dont have to worry, but if you want to do it manualy, you can do that by opening the UXML file and writing your own UXML code that could look like this:
```
<Button name="startButton" class="mainButton" text="Start" />
```

## Styling Classes (USS)

UI Toolkit allows visual styling of UI elements directly inside the UI Builder, without manually editing USS files.

### Selecting a UI Element

In the UI Builder, a UI element (for example a Button or Label) is selected from the Hierarchy panel. Once selected, its properties become visible in the Inspector.

<img width="471" height="602" alt="image" src="https://github.com/user-attachments/assets/9eb0b102-0466-4125-9fe4-09d36c287e68" />

### Assigning Style Classes

In the Inspector, a class name can be added in the Class List field.
This class will be used to apply shared styling to multiple elements.

### Editing Styles Visually

The Inspector provides multiple styling sections such as:

- Layout (width, height, flex direction, alignment)

- Style (background color, text color, font size)

-  Spacing (margin and padding)

- Border and Background

  <img width="683" height="1199" alt="image" src="https://github.com/user-attachments/assets/4207c74d-74b7-4abf-9775-2a7d0539b30a" />


Changes made here immediately update the preview in the Viewport.

### Creating and Modifying Stylesheets Automatically

When styles are edited through the UI Builder, Unity automatically updates the associated USS stylesheet in the background.
No manual code editing is required, but like earlyier if you want to write it on your own you may by editing the USS file manualy wich is just like CSS and could look like this:
```
.mainButton {
    width: 200px;
    height: 60px;
    background-color: #2a9df4;
    color: white;
    unity-font-style: bold;
}

```

### Reusing Styles Across Elements
Once a class has defined visual properties, the same class can be applied to other UI elements through the Inspector.
This ensures a consistent appearance across the interface.

### Live Preview and Iteration

All styling changes are displayed in real time within the UI Builder, allowing quick iteration and visual refinement of the UI.

## Linking Buttons and Adding Functionality

UI behavior is implemented using C# scripts. So the first thing you have to do ist creating a new class for example MenuController.cs. Now this is where you need some C# knowladge becouse you need to write the code for this part manualy.

### Accessing the UI Root

First create a variable that stores the root element of the UI Toolkit hierarchy. All UI elements defined in the UXML file exist under this root.

```
public VisualElement ui;

private void Awake()
{
    ui = GetComponent<UIDocument>().rootVisualElement;
}

```
In Awake, the script retrieves the UIDocument component attached to the same GameObject and stores its rootVisualElement.
This ensures that the UI hierarchy is available before any interaction logic is applied.

### Referencing Elements from UXML

```
public Button playButton;
public Button levelsButton;
public Button quitButton;


private void OnEnable()
{
    playButton = ui.Q<Button>("play-button");

    levelsButton = ui.Q<Button>("levels-button");

    quitButton = ui.Q<Button>("quit-button");
}

```

These variables represent the elements defined in the UXML file. Each button is identified by its name attribute in UXML (for example: play-button). You access the element by going int to the root elements and searching the element type and name (ui.Q<Button>("play-button")). 

### Registering Button Events

Now using our variabel for the buttons, we can assigne funktions to them as you can see below:

```
private void OnEnable()
{
    playButton = ui.Q<Button>("play-button");
    playButton.clicked += OnPlayButtonClicked;

    levelsButton = ui.Q<Button>("levels-button");
    levelsButton.clicked += OnLevelsButtonClicked;

    quitButton = ui.Q<Button>("quit-button");
    quitButton.clicked += OnQuitButtonClicked;
}

```

The last piece to finish our fully working UI is now the funktion wich depends on your buttons and what they should do. In my case I created a quit button which is made to stop the game so the funktion could look something like this:

```
private void OnQuitButtonClicked()
{
    Application.Quit();
#if UNITY_EDITOR
    EditorApplication.isPlaying = false;
#endif
}

```

# Posible problems
- Missspelling the name of elements can lead to problems with referencing them in your C# code
    - Solution: When creating elements you should use the same name structure for each of them so accessing them in C# is easier and less confusing
 

# Result
![ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/b6f30dce-380d-44c5-893e-1075cd481b2c)




