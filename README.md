## Table of Contents
- [ExcelToJSON Converter](#exceltojson)
- [Prefab Scanner](#prefab-scanner)
- [Animation Utility](#animation-utility)

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

### **GenerateModelClassFromJSON()**
Generates a C# model class from the JSON string. The model class has properties for each column in the Excel file with corresponding data types. The model class is saved to the "Assets/Scripts/ModelScripts" folder.

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
