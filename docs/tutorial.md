---

When an element is created the UI Toolkit updates your UXML file, by writing all the code for you so you don't have to worry, but if you want to do it manually, you can do that by opening the UXML file and writing your own UXML code that could look like this:
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
No manual code editing is required, but like earlier if you want to write it on your own you may by editing the USS file manually which is just like CSS and could look like this:
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

UI behaviour is implemented using C# scripts. So the first thing you have to do is creating a new class for example MenuController.cs. Now this is where you need some C# knowledge because you need to write the code for this part manually.

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

# Possible problems
- Misspelling the name of elements can lead to problems with referencing them in your C# code
    - Solution: When creating elements you should use the same name structure for each of them so accessing them in C# is easier and less confusing
 

# Result


![ezgif com-video-to-gif-converter (1)](https://github.com/user-attachments/assets/022c971e-81ac-48d7-b92f-8faf75923257)


