## Table of Contents
- [ExcelToJSON Converter](#exceltojson)
- [Prefab Scanner](#prefab-scanner)
- [Animation Utility](#animation-utility)
- [Event Utility](#event-utility)
- [Event Utility](#addressable-utility)

# KoreUtilitiesAndEditorTools

## **ExcelToJSON Converter** <a name="exceltojson"></a>

This script allows you to convert an Excel file into a JSON file using Unity Editor. The Excel file should follow specific rules for the converter to work correctly. The first row should contain the column headers, the second row should contain the data types for each column (string, int, float, or bool), and the remaining rows should contain the data.

## **How to Use**

1. Place the "ExcelToJSON.cs" script file into the "Editor" folder in your Unity project.
2. Open Unity Editor and go to the "Window" menu. Select "CodeWithK" and then select "Excel To JSON Converter".
3. Click the "Select Excel File" button and choose the Excel file you want to convert. The file path will appear in the text field next to the button.
4. Type in the name of the output JSON file in the "JSON File Name" text field.
5. Click the "Convert" button to convert the Excel file to JSON.
6. The JSON file will be saved in the same folder as the Excel file with the name you specified.

## **Code Explanation**

### **LoadExcelFile()**

The **`LoadExcelFile()`** method opens the Excel file using a **`FileStream`** and reads it using **`IExcelDataReader`**. It returns the first **`DataTable`** in the **`DataSet`**.

### **ConvertDataTableToListOfDictionaries()**

The **`ConvertDataTableToListOfDictionaries()`** method converts the **`DataTable`** into a list of dictionaries, where each dictionary represents a row in the Excel file. It uses the first row of the **`DataTable`** as the headers and the second row as the data types for each column. It then loops through the remaining rows to add the data to the dictionaries.

### **ConvertListOfDictionariesToJson()**

The **`ConvertListOfDictionariesToJson()`** method converts the list of dictionaries into a JSON string using **`JsonConvert.SerializeObject()`**.

### **WriteJsonFile()**

The **`WriteJsonFile()`** method writes the JSON string to a file using **`File.WriteAllText()`**.

### **OnGUI()**

The **`OnGUI()`** method creates the user interface for the script. It includes a label for the script name, buttons to select the Excel file and convert it to JSON, and text fields for the file paths and names.

## **References**

- **[ExcelDataReader](https://github.com/ExcelDataReader/ExcelDataReader)**
- **[Newtonsoft.Json](https://www.newtonsoft.com/json)**

# **Prefab Scanner**

This Unity Editor script generates a C# script that automatically assigns the UI components of a prefab to fields in the script. The generated script can be added to the prefab and used to reference its UI elements.

## **How to Use**

1. Place the "PrefabScanner.cs" script file into the "Editor" folder in your Unity project.
2. Select the prefab asset in the project window that you want to scan for UI components.
3. Open Unity Editor and go to the "Window" menu. Select "CodeWithK" and then select "Prefab Scanner".
4. Enter a name for the generated script in the "Script Name" text field.
5. Click the "Scan Prefab" button to generate the script and add it to the prefab.
6. The generated script will be saved in the "UIScripts" folder in your project and added to the selected prefab.

## **Code Explanation**

### **OnGUI()**

The **`OnGUI()`** method creates the user interface for the script. It includes a text field for the script name and a button to scan the selected prefab.

### **IsValidScriptName()**

The **`IsValidScriptName()`** method checks if the script name contains any invalid characters.

### **FindSerializedFields()**

The **`FindSerializedFields()`** method recursively finds all UI elements in the prefab that start with "m_" and writes their names and types to the output file.

### **AssignUIComponents()**

The **`AssignUIComponents()`** method recursively finds all UI elements in the prefab and writes the code to assign them to their respective fields in the output file.

## **References**

- **[PrefabUtility.GetPrefabAssetType](https://docs.unity3d.com/ScriptReference/PrefabUtility.GetPrefabAssetType.html)**
- **[StreamWriter](https://docs.microsoft.com/en-us/dotnet/api/system.io.streamwriter?view=net-6.0)**
- **[MonoScript](https://docs.unity3d.com/ScriptReference/MonoScript.html)**

## **Animation Utility**

The **`AnimationUtility`** class provides several methods for controlling animations using an Animator component in Unity.

### **Usage**

To use the **`AnimationUtility`** class, you first need to call the **`Initialize`** method and pass in the Animator component you want to control:

```csharp
AnimationUtility.Initialize(animator);

```

After initializing, you can use the other methods provided by the class:

- **`PlayAnimation(string clipName, bool playDirectly = true, Action onStart = null, Action onEnd = null)`**: Plays an animation clip by name. You can choose to play it directly or wait for any other animation that is being played. You can also specify callbacks for when the animation starts and ends.
- **`GetAnimationLength(string clipName)`**: Returns the length of an animation clip by name.
- **`ResetAnimation(string clipName)`**: Sets an animation clip to its starting state.
- **`PauseAnimation(string clipName, Action onPause = null)`**: Pauses an animation clip. You can specify a callback for when the animation is paused.
- **`ResumeAnimation(string clipName, Action onResume = null)`**: Resumes a paused animation clip. You can specify a callback for when the animation is resumed.

### **Example**

Here's an example of how to use the **`AnimationUtility`** class to play an animation clip called "Jump":

```csharp
Animator animator = GetComponent<Animator>();
AnimationUtility.Initialize(animator);
float animationLength = AnimationUtility.GetAnimationLength("Jump");
AnimationUtility.PlayAnimation("Jump", true, () => Debug.Log("Jump started!"), () => Debug.Log("Jump ended!"));

```

### **Notes**

- This class assumes that the Animator component is attached to the same GameObject that this script is attached to.
- This class uses a helper MonoBehaviour to run the DelayedCallback coroutine. This MonoBehaviour is created automatically and does not need to be added to any GameObjects.

# **EventUtility** <a name="event-utility"></a>

The **`EventUtility`** class provides a simple way to manage Unity events with string keys and support for custom data.

## **Overview**

The **`EventUtility`** class provides the following functionality:

- Add and remove listeners from events with string keys.
- Fire events with no parameters, one parameter, two parameters, or custom data of any type.
- Handle events with UnityAction, UnityAction<T>, and UnityAction<T, U> delegates.

## **Public Methods**

### **AddListener**

```csharp
public static void AddListener(string eventName, UnityAction action)

```

Adds a listener to the event with the specified name

### Parameters

- **`eventName`**: The name of the event to add the listener to.
- **`action`**: The action to add as a listener.

### **RemoveListener**

```csharp
public static void RemoveListener(string eventName, UnityAction action)

```

Removes a listener from the event with the specified name.

### Parameters

- **`eventName`**: The name of the event to remove the listener from.
- **`action`**: The action to remove as a listener.

### **FireEvent**

```csharp
public static void FireEvent(string eventName)

```

Fires the event with the specified name.

### Parameters

- **`eventName`**: The name of the event to fire.

### **FireEvent<T>**

```csharp
public static void FireEvent<T>(string eventName, T arg)

```

Fires the event with one parameter.

### Parameters

- **`eventName`**: The name of the event to fire.
- **`arg`**: The parameter to pass to the event.

### **FireEvent<T, U>**

```csharp
public static void FireEvent<T, U>(string eventName, T arg1, U arg2)

```

Fires the event with two parameters.

### Parameters

- **`eventName`**: The name of the event to fire.
- **`arg1`**: The first parameter to pass to the event.
- **`arg2`**: The second parameter to pass to the event.

### **FireEventWithCustomData**

```csharp
public static void FireEventWithCustomData<T>(string eventName, T data)

```

Fires the event with custom data.

### Parameters

- **`eventName`**: The name of the event to fire.
- **`data`**: The custom data to pass to the event.

## **Static Fields**

### **eventDictionary**

```csharp
private static Dictionary<string, UnityEvent> eventDictionary = new Dictionary<string, UnityEvent>()

```

A dictionary of events with string keys and UnityEvent values.

## **Usage**

Here's an example of how to use the **`EventUtility`** class:
```using UnityEngine;
using UnityEngine.Events;

public class MyEventEmitter : MonoBehaviour
{
    // Declare a public UnityEvent field to hold the event
    public UnityEvent myEvent;

    // Start is called before the first frame update
    void Start()
    {
        // Add a listener to the event
        EventUtility.AddListener("myEvent", OnMyEvent);

        // Fire the event with no parameters
        EventUtility.FireEvent("myEvent");

        // Fire the event with one integer parameter
        int intValue = 42;
        EventUtility.FireEvent("myEvent", intValue);

        // Fire the event with two parameters: a float and a string
        float floatValue = 3.14f;
        string stringValue = "Hello, world!";
        EventUtility.FireEvent("myEvent", floatValue, stringValue);
    }

    // This method will be called when the event is fired
    private void OnMyEvent()
    {
        Debug.Log("MyEvent received with no parameters");
    }

    private void OnMyEvent(int intValue)
    {
        Debug.Log("MyEvent received with int parameter: " +intValue);
}

private void OnMyEvent(float floatValue, string stringValue)
{
    Debug.Log("MyEvent received with float parameter: " + floatValue);
    Debug.Log("MyEvent received with string parameter: " + stringValue);
}

private void OnDestroy()
{
    // Remove the listener when the object is destroyed
    EventUtility.RemoveListener("myEvent", OnMyEvent);
}

```
In this example, we declare a public `UnityEvent` field called `myEvent` to hold the event. We then add a listener to the event using the `EventUtility.AddListener` method in the `Start` method, and fire the event using the `EventUtility.FireEvent` method with various parameters.

We also define several private methods to handle the event with different numbers and types of parameters, and remove the listener in the `OnDestroy` method using the `EventUtility.RemoveListener` method.

By using the `EventUtility` class, we can easily manage our events and add and remove listeners without having to manage them ourselves. We can also fire the event with custom data of any type, making our code more flexible and reusable.

    # **AddressableUtility** <a name="addressable-utility"></a>

The AddressableUtility class provides utility functions for loading, preloading, and unloading Unity Addressable assets asynchronously. It also includes a simple object pool for getting assets that have been loaded.

### **Class Members**

`private static Dictionary<string, AsyncOperationHandle> loadedAssets = new Dictionary<string, AsyncOperationHandle>();`A private dictionary that stores the loaded assets' name and handle.

`public static async Task<T> LoadAddressableAsset<T>(string assetName) where T : Object`Loads the Unity Addressable asset with the specified asset name asynchronously and returns the loaded asset. If the asset is already loaded, the function returns the loaded asset immediately.

**assetName:** The name of the asset to load.Returns: The loaded asset.`public static async Task<T> LoadAddressableAssetAsync<T>(string assetName) where T : Object`Loads the Unity Addressable asset with the specified asset name asynchronously and returns the loaded asset. If the asset is already loaded, the function returns the loaded asset immediately.

**assetName:** The name of the asset to load.**Returns:** The loaded asset.`public static async Task PreloadAddressables(IEnumerable<string> assetNames)`Preloads a list of Unity Addressable assets asynchronously.

**assetNames:** A list of asset names to preload.`public static T GetFromPool<T>(string assetName) where T : Object`Returns the loaded Unity Addressable asset with the specified asset name from the object pool.

**assetName:** The name of the asset to get.**Returns:** The loaded asset.`public static Task UnloadAddressable(string assetName)`Unloads the Unity Addressable asset with the specified asset name asynchronously.

**assetName:** The name of the asset to unload.**Returns:** A Task representing the completion of the operation.`public static void UnloadAllAddressables()`Unloads all the loaded Unity Addressable assets asynchronously.
