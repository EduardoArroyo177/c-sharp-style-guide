# The C# Style Guide

Our overarching goals are conciseness, readability and simplicity

## Inspiration

This is a guide based on the raywenderlich [C# Style Guide] (https://github.com/raywenderlich/c-sharp-style-guide), but with some modifications to adapt it  to [Unity Technologies UI] (https://bitbucket.org/Unity-Technologies/ui/) coding style and guidelines.

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Script Files](#script-files)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Code Sample] (#code-sample)
- [Code Organization] (#code-organization)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow C# standards.

### Script Files

Script files are all __UpperCamelCase__, multiple words concatenated together,
without
hypens or underscores:

__BAD__:

```c#
image_editor.cs
```

__GOOD__:

```c#
ImageEditor.cs
```

### Namespaces

Namespaces are all __UpperCamelCase__, multiple words concatenated together,
without
hypens or underscores:

__BAD__:

```c#
using unityengine.ui;
```

__GOOD__:

```c#
using UnityEngine.UI;
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example:

```C#
public class ImageEditor : GraphicEditor {}
```

### Methods

Public or private are written in __UpperCamelCase__. For example:

```C#
protected void SpriteGUI(){}
```

### Fields

Written in __lowerCamelCase__.

When having the scope of a variable, it should be written using __Hungarian notation__. For example:

```c#
AnimBool m_ShowType;
```

All other fields are written __lowerCamelCase__. Per Unity convention, this includes __public fields__ as well.

For example:

```C#
public class ImageEditor : GraphicEditor {
  var typeEnum;
  bool showNativeSize;
  var newSprite;
}
```

Private non-static fields should start with a lowercase letter.

__BAD:__

```c#
private int _myPrivateVariable
```

__GOOD:__

```c#
private int myPrivateVariable
```

### Parameters

Parameters are written in __lowerCamelCase__.

__BAD:__

```c#
void SetShowNativeSize(bool Instant)
```
__GOOD:__

```c#
void SetShowNativeSize(bool instant)
```

Single character values to be avoided except for temporary looping variables.

### Delegates

Delegats are written in __UpperCamelCase__.

When declaring delegates, DO add the suffix __EventHandler__ to names of delegates that are used in events. 

__BAD:__

```c#
public delegate void Click()
```
__GOOD:__

```c#
public delegate void ClickEventHandler()
```
DO add the suffix __Callback__ to names of delegates other than those used as event handlers.

__BAD:__

```c#
public delegate void Render()
```
__GOOD:__

```c#
public delegate void RenderCallback()
```
### Events

Prefix event methods with the prefix __On__.

__BAD:__

```c#
public static event CloseCallback Close;
```
__GOOD:__

```c#
public static event CloseCallback OnClose;
```

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```c#
XMLHTTPRequest
String URL
findPostByID
```
__GOOD:__

```c#
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and
member variables.

### Fields & Variables

Prefer single declaration per line.

__BAD:__

```c#
string username, twitterHandle;
```

__GOOD:__

```c#
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where
scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter __I__. 

__BAD:__

```c#
RadialSlider
```

__GOOD:__

```c#
IRadialSlider
```

## Spacing

### Indentation

Indentation is using tabs - never spaces.

#### Blocks

Indentation for blocks uses 1 tab (not spaces):

__GOOD:__

```c#
for (int i = 0; i < 10; i++) {
    Debug.Log("index=" + i);
}
```

__BAD:__

```c#
for (int i = 0; i < 10; i++) {
  Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use default indentation:

__GOOD:__

```c#
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

__BAD:__

```c#
CoolUiWidget widget =
someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.


## Brace Style

Both braces (opening and closing) are awarded their own line.

__BAD:__

```c#
public class ImageEditor : GraphicEditor{
	// ...
	protected void SpriteGUI(){
    	EditorGUI.BeginChangeCheck();
    	EditorGUILayout.PropertyField(m_Sprite, m_SpriteContent);
    	if (EditorGUI.EndChangeCheck()){
    		// ...
    	} else{
        	// ...
        }
    }
}
```

__GOOD:__

```c#
public class ImageEditor : GraphicEditor
{
	// ...
	protected void SpriteGUI()
    {
    	EditorGUI.BeginChangeCheck();
    	EditorGUILayout.PropertyField(m_Sprite, m_SpriteContent);
    	if (EditorGUI.EndChangeCheck())
    	{
    		// ...
    	}
    	else
    	{
        	// ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

__BAD:__

```c#
if (EditorGUI.EndChangeCheck())
	var newSprite = m_Sprite.objectReferenceValue as Sprite;
	
if (newSprite.border.SqrMagnitude() > 0) m_Type.enumValueIndex = (int)Image.Type.Sliced;
```

__GOOD:__

```c#
if (EditorGUI.EndChangeCheck())
{
	var newSprite = m_Sprite.objectReferenceValue as Sprite;
}

if (newSprite.border.SqrMagnitude() > 0) { m_Type.enumValueIndex = (int)Image.Type.Sliced; }
```

## Switch Statements

Switch statements fall-through by default, but this can be unintuitive. Do not use fall-through behavior. 

Always include the `default` case.

## Language

Use US English spelling.

__BAD:__

```c#
string colour = "red";
```

__GOOD:__

```c#
string color = "red";
```

## Code Sample

As an example of how the people of Unity Technologies write the code, next it is shown a class from their UI code:

```c#
using System.Linq;
using UnityEditor.AnimatedValues;
using UnityEngine;
using UnityEngine.UI;

namespace UnityEditor.UI
{
    /// <summary>
    /// Editor class used to edit UI Graphics.
    /// </summary>

    [CustomEditor(typeof(MaskableGraphic), false)]
    [CanEditMultipleObjects]
    public class GraphicEditor : Editor
    {
        protected SerializedProperty m_Script;
        protected SerializedProperty m_Color;
        protected SerializedProperty m_Material;
        protected SerializedProperty m_RaycastTarget;

        private GUIContent m_CorrectButtonContent;
        protected AnimBool m_ShowNativeSize;

        protected virtual void OnDisable()
        {
            Tools.hidden = false;
            m_ShowNativeSize.valueChanged.RemoveListener(Repaint);
        }

        protected virtual void OnEnable()
        {
            m_CorrectButtonContent = new GUIContent("Set Native Size", "Sets the size to match the content.");

            m_Script = serializedObject.FindProperty("m_Script");
            m_Color = serializedObject.FindProperty("m_Color");
            m_Material = serializedObject.FindProperty("m_Material");
            m_RaycastTarget = serializedObject.FindProperty("m_RaycastTarget");

            m_ShowNativeSize = new AnimBool(false);
            m_ShowNativeSize.valueChanged.AddListener(Repaint);
        }

        public override void OnInspectorGUI()
        {
            serializedObject.Update();
            EditorGUILayout.PropertyField(m_Script);
            AppearanceControlsGUI();
            RaycastControlsGUI();
            serializedObject.ApplyModifiedProperties();
        }

        protected void SetShowNativeSize(bool show, bool instant)
        {
            if (instant)
                m_ShowNativeSize.value = show;
            else
                m_ShowNativeSize.target = show;
        }

        protected void NativeSizeButtonGUI()
        {
            if (EditorGUILayout.BeginFadeGroup(m_ShowNativeSize.faded))
            {
                EditorGUILayout.BeginHorizontal();
                {
                    GUILayout.Space(EditorGUIUtility.labelWidth);
                    if (GUILayout.Button(m_CorrectButtonContent, EditorStyles.miniButton))
                    {
                        foreach (Graphic graphic in targets.Select(obj => obj as Graphic))
                        {
                            Undo.RecordObject(graphic.rectTransform, "Set Native Size");
                            graphic.SetNativeSize();
                            EditorUtility.SetDirty(graphic);
                        }
                    }
                }
                EditorGUILayout.EndHorizontal();
            }
            EditorGUILayout.EndFadeGroup();
        }

        protected void AppearanceControlsGUI()
        {
            EditorGUILayout.PropertyField(m_Color);
            EditorGUILayout.PropertyField(m_Material);
        }

        protected void RaycastControlsGUI()
        {
            EditorGUILayout.PropertyField(m_RaycastTarget);
        }
    }
}
```

## Code Organization

As a team, we also want to have a better organized code for making even easier to read a code that was written from other members from the team, so we propose an structure for this:

```c#
using UnityEngine;
using System.Collections;

public class OrganizationScript : MonoBehaviour
{
    //
    // OrganizationScript
    //
    // structs & classes
    //
    // ...
    //
    // Variables
    //
    // ...
    //
    // Properties
    //
    // ...
    //
    // Unity
    //
    // ...
    //
    // User
    //
    // ...
    //
}
```

For the Unity MonoBehaviour functions, we also propose an order for writing them:

```c#
Awake(){}

Start(){}

OnEnable(){}

OnDisable(){}

Update(){}

FixedUpdate(){}
```

## Credits

This style guide is a collaborative effort from the most stylish
raywenderlich.com team members:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley] (https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)

