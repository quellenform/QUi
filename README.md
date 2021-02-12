# QUi - Quellenform UI (v0.0.3)
Various UXML-/USS-modifications and addons for UIElements in Unity Inspector.

- [QUi - Quellenform UI (v0.0.3)](#qui---quellenform-ui-v003)
  - [Compatibility](#compatibility)
  - [What it does?](#what-it-does)
  - [Example](#example)
  - [Usage](#usage)
  - [UXML Container & Grid](#uxml-container--grid)
  - [USS Classes](#uss-classes)
    - [Colors](#colors)
    - [Input Fields](#input-fields)
    - [Vector Fields](#vector-fields)
    - [Boxed Elements](#boxed-elements)
  - [Added UXML-Elements](#added-uxml-elements)
    - [FoldoutToggle](#foldouttoggle)
    - [Radio](#radio)
    - [SliderField](#sliderfield)
    - [SliderIntField](#sliderintfield)
    - [MinMaxSliderField](#minmaxsliderfield)
    - [EnumToggle](#enumtoggle)
    - [EnumPaging](#enumpaging)
    - [InspectorTitle](#inspectortitle)
  - [Screenshot](#screenshot)
  - [Known Bugs (not solvable?)](#known-bugs-not-solvable)
  - [Known Bugs (fix this!)](#known-bugs-fix-this)
  - [TODO](#todo)
  - [Planned Features](#planned-features)
  - [Changelog](#changelog)

## Compatibility
- Tested with Unity v2019.3+

<div class="page"/>

## What it does?
With UXML and USS it is now possible to style UIElements in Unity 3D with common technics well known to web developers. But most of the default elements in Unity3D are inconsistent/incomplete or not styled in a way which we would consider *impressive*.

So the idea is to get those features into Unity which are common practice in modern webdesign, like the [Twitter Bootstrap](https://getbootstrap.com/).
This Asset is NOT a port of Bootstrap, but it was inspired by the structure and technics which is used there.

QUi is not intended for level-designers or unexperienced users, but if you are developer and want to style your custom inspector, this is for you.

The UIElements are provided for dark- and light-skin.

## Example

If you want to get an example of what you can do with QUi, please take a look into `Examples/Editor/QUiElementsExampleEditor.cs`.
This file contains a bunch of UIElements added to the Inspector. Some values used in this file are defined in the ScriptableObject `Examples/QUiElementsExample.cs`, but they all are just for demonstration porposes and are not useful in any part of a real project.

A good starting point would be to open the ScriptableObject Asset `Examples/QUiElementsExample.asset`

## Usage

Normally you would use elements from `UnityEditor.UIElements` or `UnityEngine.UIElements` in your C# script or directly from UXML, and that's exactly what you still do with QUi.
The difference is, that you are able to use additional elements and get it styled without coding your own USS to achieve a good looking Editor/Inspector.

You have two possibilities to do so:
1. Create your own Editor-script (inheriting from `UnityEditor.Editor`), load the stylesheets you need and add the required classnames to your UIElements
2. Create your own Editor-script (inheriting from `Quellenform.QUi.QUiEditor`, which inherits from `UnityEditor.Editor`) and call the relevant methods and add the required classnames to your UIElements

<div class="page"/>

## UXML Container & Grid

```xml
<ui:VisualElement class="container">
    <ui:VisualElement class="row">
        <ui:VisualElement class="col">
            <!-- UIElements -->
        </ui:VisualElement>
    </ui:VisualElement>
</ui:VisualElement>
```

Multi-column view (2 columns):
```xml
<ui:VisualElement class="container">
    <ui:VisualElement class="row">
        <ui:VisualElement class="col col-6">
            <!-- UIElements -->
        </ui:VisualElement>
        <ui:VisualElement class="col col-6">
            <!-- UIElements -->
        </ui:VisualElement>
    </ui:VisualElement>
</ui:VisualElement>
```

Multi-column view (4 columns):
```xml
<ui:VisualElement class="container">
    <ui:VisualElement class="row">
        <ui:VisualElement class="col col-3">
            <!-- UIElements -->
        </ui:VisualElement>
        <ui:VisualElement class="col col-3">
            <!-- UIElements -->
        </ui:VisualElement>
        <ui:VisualElement class="col col-3">
            <!-- UIElements -->
        </ui:VisualElement>
        <ui:VisualElement class="col col-3">
            <!-- UIElements -->
        </ui:VisualElement>
    </ui:VisualElement>
</ui:VisualElement>
```

<div class="page"/>

## USS Classes

### Colors
The available colors are:
- red
- orange
- yellow
- green
- cyan
- blue
- blue
- violet
- pink


### Input Fields
You can assign those colors to your input fields with the following classes:
- `color-red`
- `color-orange`
- `color-yellow`
- `color-green`
- `color-cyan`
- `color-blue`
- `color-violet`
- `color-pink`

Example:
```xml
<!-- UXML -->
<ui:TextField class="color-green" />
```

```C#
// C#
TextField myTextfield = new TextField("My Textfield");
myTextfield.AddToClassList("color-green");
```

The above color-classes can be applied to the following UIElements:
- `Toggle`
- `BoundsField`
- `BoundsIntField`
- `DoubleField`
- `EnumField`
- `FloatField`
- `IntegerField`
- `LayerField`
- `LayerMaskField`
- `LongField`
- `MaskField`
- `ObjectField`
- `ProgressBar`
- `PropertyField`
- `RectField`
- `RectIntField`
- `TagField`
- `Vector2Field`
- `Vector2IntField`
- `Vector3Field`
- `Vector3IntField`
- `Vector4Field`
- `ObjectField`
- `Slider`
- `SliderInt`
- `SliderField`
- `MinMaxSlider`
- `MinMaxSliderField`
- `Slider`
- `Button`
- `Box`
- `Foldout`
- `FoldoutToggle`
- `EnumToggle`
- `EnumPaging`
- `Radio`

**Attention:** If you assign one of the `color-*`-classes to the UIElements `Box`, `Foldout` or `FoldoutToggle`, all the child input elements are displayed in the chosen color recursively!

### Vector Fields

Vector input fields can be automagically colored according to their axis by adding the class `colored-axis`.
The available UIElements are:
- `Vector2Field`
- `Vector2IntField`
- `Vector3Field`
- `Vector3IntField`

Example:
```xml
<!-- UXML -->
<ui:Vector3Field class="colored-axis" />
```

```C#
// C#
Vector3Field myVector3Field = new Vector3Field();
myVector3Field.AddToClassList("colored-axis");
```

**Attention:** the class `colored-axis` has the highest priority and will override any other color-class added before!

> TODO: Screenshot of colored vector fields

### Boxed Elements

The UIElements `Box`, `Foldout` and `FoldoutToggle` (added by *QUi*) can be displayed as a boxed element and can be additionally styled with a colored background/border.

First you need to add the class `boxed` to it. This will generate a grey box with a small padding.

Additionally you can add one of these colors:
- `boxed-red`
- `boxed-orange`
- `boxed-yellow`
- `boxed-green`
- `boxed-cyan`
- `boxed-blue`
- `boxed-violet`
- `boxed-pink`

The UIElements `Foldout` and `FoldoutToggle` can also have their content indented (default behaviour) or not. If you don't want your box-content to be indented, simple add the class `notindented`.

Example:
```xml
<!-- UXML -->
<ui:Foldout class="boxed">
    <!-- child UIElements -->
</ui:Foldout>
<ui:Foldout class="boxed boxed-green">
    <!-- child UIElements -->
</ui:Foldout>
<ui:Foldout class="boxed boxed-red notindented">
    <!-- child UIElements -->
</ui:Foldout>
```

```C#
// C#
Foldout myFoldout1 = new Foldout() { text = "My Foldout" };
myFoldout1.AddToClassList("boxed");

Foldout myFoldout2 = new Foldout() { text = "My Foldout (green)" };
myFoldout2.AddToClassList("boxed");
myFoldout2.AddToClassList("boxed-green");

Foldout myFoldout3 = new Foldout() { text = "My Foldout (red, notindented)" };
myFoldout3.AddToClassList("boxed");
myFoldout3.AddToClassList("boxed-green");
myFoldout3.AddToClassList("notindented");
```

<div class="page"/>

## Added UXML-Elements
- **SliderField**: A slider with input field
- **MinMaxSliderField**: A min-max-slider with input fields
- **FoldoutToggle**: Foldout-like element with checkbox (bindable)
- **InspectorTitle**: Title element for the inspector with *title*, *subtitle*, *version* and *icon*

If you want to use those UIElements inside your custom UXML-file, you need to add the namespace on top of it:
```xml
<engine:UXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:ui="UnityEngine.UIElements"
    xmlns:ue="UnityEditor.UIElements"
    xmlns:qui="Quellenform.QUi.UIElements" xsi:noNamespaceSchemaLocation="../../../UIElementsSchema/UIElements.xsd">
    <!-- ...your custom UIElements here -->
</engine:UXML>
```

### FoldoutToggle

The `FoldoutToggle` UIElement works exactly like a `Foldout`, but instead using a foldout icon, it is bound to a bool-variable displayed as Toggle.

Additionally the content area can be visible permanently
 and the content is visible (default behaviour).

To change that behaviour, you can additionally add the class `collapsable`, which will fold the content if the Toggle is disabled.

```xml
<!-- UXML -->
<qui:FoldoutToggle class="boxed">
    <!-- child UIElements -->
</qui:FoldoutToggle>
<qui:FoldoutToggle class="boxed boxed-green">
    <!-- child UIElements -->
</qui:FoldoutToggle>
<qui:FoldoutToggle class="boxed boxed-blue" keepOpened="true">
    <!-- child UIElements -->
</qui:FoldoutToggle>
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
FoldoutToggle myFoldoutToggle1 = new FoldoutToggle(mySerializedProperty);

FoldoutToggle myFoldoutToggle2 = new FoldoutToggle("My Toggle Group", mySerializedProperty);
myFoldoutToggle2.AddToClassList("boxed");

FoldoutToggle myFoldoutToggle3 = new FoldoutToggle("My Toggle Group (green, collapsable)", mySerializedProperty);
myFoldoutToggle3.AddToClassList("boxed");
myFoldoutToggle3.AddToClassList("boxed-green");

FoldoutToggle myFoldoutToggle4 = new FoldoutToggle("My Toggle Group (blue, always opened)", mySerializedProperty, true);
myFoldoutToggle4.AddToClassList("boxed");
myFoldoutToggle4.AddToClassList("boxed-blue");
```

### Radio

A Toggle element with rounded borders.

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:Radio binding-path="myProperty"/>
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
Radio myRadio = new Radio("My Slider Float Field");
myRadio.bindingPath = "myProperty";
```

### SliderField

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:SliderField binding-path="myProperty" />
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
SliderField mySliderField = new SliderField("My Slider Float Field") { value = 3.5f };
mySliderField.bindingPath = "myProperty";
```

### SliderIntField

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:SliderIntField binding-path="myProperty" />
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
SliderIntField mySliderIntField = new SliderIntField("My Slider Int Field") { value = 3 };
myRadio.mySliderIntField = "myProperty";
```

### MinMaxSliderField

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:MinMaxSliderField binding-path="myProperty" />
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
MinMaxSliderField myMinMaxSliderField = new MinMaxSliderField();
myMinMaxSliderField.bindingPath = "myProperty";
```

### EnumToggle

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:EnumToggle binding-path="myProperty" />
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
EnumToggle myEnumToggle = new EnumToggle("Label", mySerializedProperty);
```

### EnumPaging

> TODO: Description/Screenshot/Examples

```xml
<!-- UXML -->
<qui:EnumPaging binding-path="myProperty"/>
```

```C#
// C#
SerializedProperty mySerializedProperty = serializedObject.FindProperty("myProperty");
EnumPaging myEnumPaging = new EnumPaging("Label", mySerializedProperty);
```

### InspectorTitle

> TODO: Description/Screenshot


```xml
<!-- UXML -->
<qui:InspectorTitle name="inspector-title">
    <ui:Image name="title-icon" />
    <ui:VisualElement name="title-text">
        <ui:Label name="title-text__title" text="Title" />
        <ui:Label name="title-text__subtitle" text="Subtitle" />
        <ui:Label name="title-text__version" text="0.0.3" />
    </ui:VisualElement>
</qui:InspectorTitle>
```

```C#
// C#
InspectorTitle myInspectorTitle = new InspectorTitle(
    "Title", // Title
    "Subtitle", // Subtitle (optional)
    "0.0.3", // Version (optional)
    "plugin-qui" // <Texture> Icon (optional)
);
```

<div class="page"/>

## Screenshot
![QUi Screenshot](Documentation~/Images/QUi-overview.jpg?raw=true "QUi v0.0.3")

<div class="page"/>

## Known Bugs (not solvable?)
- Unity versions below v2019.4 have problems with the colored border around slider draggers

## Known Bugs (fix this!)
- Initial value in FoldoutToggle is not beeing updated, if element were added by UXML
- Indentation of nested groups leads to incorrect label widths
- Fix USS-classes for Box-elements (change them from `background-*` to `boxed-*` ?)

## TODO
- Revise the colors of the light-skin (right now this is incomplete)
- Test all custom UIElements from UXML directly and check if they work properly (structure, binding!)
- Explain the grid-system with more practical examples
- UXML-definition for EnumToggle/EnumPaging
- Add tutorial which describes the custom implementation of QUiEditor
- Move all the examples to an EditorWindow and remove the ScriptableObjects

## Planned Features
- Alerts/Infoboxes (with icons)
- Modals
- Popovers
- Spinner
- Radio and switches
- Button groups
- Reorderable lists
- Tabs
- UXML-ColorPicker
- ...

<div class="page"/>

## Changelog
> Version 0.0.3 (breaking changes!)
- Bugfixes in USS
- Changed the element name `ToggleGroup` to `FoldoutToggle`, because the name is already in use in Unity UI
- Changed the namespace from `Quellenform.QUi` to `Quellenform.QUiEditor` to get a clear differentiation between Editor and Engine (like `UnityEngine` and `UnityEditor`)
- Changed the behaviour of `Toggle` and moved the USS-class `rounded` to an own element (`Radio`)
- Added elements: `EnumToggle`, `EnumPaging` and `Radio`
- Finalize existing UIElements and optimize code
- Compiled the finalized elements to DLL

> Version 0.0.2
- Bugfixes in USS
- Added elements: `MinMaxSliderField`