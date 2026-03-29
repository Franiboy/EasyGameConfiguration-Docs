# EGC - EasyGameConfiguration

**Version 1.3**

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Features Overview](#2-features-overview)
3. [Installation](#3-installation)
4. [Configuration Setup](#4-configuration-setup)
   - [4.1 Initial Configuration Setup](#41-initial-configuration-setup)
   - [4.2 Creating Custom Categories](#42-creating-custom-categories)
   - [4.3 Creating Custom Properties](#43-creating-custom-properties)
   - [4.4 Data Types](#44-data-types)
5. [Using Properties in Blueprints](#5-using-properties-in-blueprints)
   - [5.1 Enum-Based Access (Recommended)](#51-enum-based-access-recommended)
   - [5.2 Legacy String-Based Access](#52-legacy-string-based-access)
   - [5.3 Available Nodes Per Type](#53-available-nodes-per-type)
   - [5.4 Resetting Properties](#54-resetting-properties)
6. [Listening for Property Changes](#6-listening-for-property-changes)
7. [Managing Save States and Configurations](#7-managing-save-states-and-configurations)
8. [Advanced Customization Options](#8-advanced-customization-options)
   - [8.1 Hidden Properties](#81-hidden-properties)
   - [8.2 Constant Properties](#82-constant-properties)
   - [8.3 Anti-Cheat Detection](#83-anti-cheat-detection)
   - [8.4 Accessing Property Configurations](#84-accessing-property-configurations)
   - [8.5 Overriding Widgets](#85-overriding-widgets)
   - [8.6 Widget Individualization](#86-widget-individualization)
9. [Dynamic Widget Generation](#9-dynamic-widget-generation)
10. [Use Cases](#10-use-cases)
11. [Similar Games](#11-similar-games)
12. [Technical Information](#12-technical-information)
13. [Frequently Asked Questions (FAQ)](#13-frequently-asked-questions-faq)
14. [Contact Information](#14-contact-information)
15. [Patch Notes](#15-patch-notes)
    - [15.1 Version 1.3](#151-version-13)
    - [15.2 Version 1.2](#152-version-12)
    - [15.3 Version 1.1](#153-version-11)

---

## 1. Introduction

EGC - EasyGameConfiguration is a powerful, easy-to-integrate library built for both Blueprint and C++ in Unreal Engine, enabling developers to create and manage custom configuration files (.ini files) without needing deep technical expertise. This plugin provides context-free access to game settings and properties, making it incredibly versatile and adaptable across various game development scenarios.

EGC aims to streamline the process of working with configuration files by offering an intuitive interface for both novice and advanced developers. Whether you are building a single-player game, a complex multiplayer experience, or a dynamic game mode, EGC gives you the tools to manage settings seamlessly through customizable .ini files.

---

## 2. Features Overview

EGC comes packed with a variety of features designed to make working with configuration files as simple as possible. Key highlights include:

- **Context-Free Access:** Interact with properties from anywhere in Blueprints or C++ without remembering key names or categories.
- **Dynamic Widget Generation:** Automatically generate UI widgets for all properties with the option to override styles and functionality.
- **Save and Load Functionality:** Save, load, reset, and manage multiple configuration files through Blueprints.
- **Custom Save Locations:** Define where .ini files are stored.
- **Hidden and Constant Properties:** Define properties that are hidden from .ini files or create constants that are globally readable but unmodifiable.
- **Anti-Cheat Detection:** Detect unauthorized modifications to save game files and automatically replace tampered values.
- **Change Callbacks:** Listen for property changes via delegates and react in real time.
- **Widget Individualization:** Customize each property's UI widget, providing developers with full control over their settings menus.
- **Flexible Shortcuts:** Access configuration settings easily through multiple shortcut buttons in the Blueprint editor, widget graph, or main project settings.

---

## 3. Installation

### Prerequisites

Before using EGC, ensure you have the following:

- Unreal Engine 5.5 or higher
- Basic knowledge of Unreal Blueprints or C++

### Steps to Install EGC

1. Download the EGC plugin from [Fab](https://www.fab.com/).
2. Open your Unreal Engine project and navigate to Plugins.
3. Enable EGC - EasyGameConfiguration and restart your project.
4. You should now see a new EasyGameConfiguration tab in the Project Settings.

Access the plugin through multiple shortcuts:

- **Main Menu:** Navigate to Edit > Easy Game Configuration Settings.
- **Blueprint Editor:** A new Config Settings button appears at the top right (can be disabled).
- **Widget Graph Editor:** A Config Settings button is available in the top-left (can be disabled).

---

## 4. Configuration Setup

### 4.1 Initial Configuration Setup

Navigate to Project Settings and locate the General tab under EasyGameConfiguration.

- **Config Folder:** Set the directory where configuration files are saved (default: `Saved/`).
- **Enum Editor Display Name:** Configure how properties are displayed in the Blueprint editor (e.g., `BaseSpeed[BaseSettings]` or `BaseSettings.BaseSpeed`).
- **Refresh BP Nodes:** Activate/disable automatically refreshing EGC methods when creating or deleting properties.
- **Start Game With Config:** Activate/disable loading a default configuration file on game start (useful in non-multi-world/save scenarios).
- **Default Config:** Set the default configuration file name if the above option is activated.
- **Blueprint Button / Widget Button:** Toggle the visibility of the Config Settings shortcut buttons in the Blueprint editor and Widget graph.

### 4.2 Creating Custom Categories

Categories are used to group related properties together. They function as sections in the .ini file.

- Navigate to the Category tab in EasyGameConfiguration settings.
- Add a new category by specifying a name.
- Categories are essential as each property must be assigned to a category.

### 4.3 Creating Custom Properties

Once you have at least one category, you can create properties:

- Navigate to the Properties tab in EasyGameConfiguration settings.
- Select the category you want to add the property to.
- Choose a data type and a name for the property.
- Set a default value for the property.
- Configure optional attributes:
  - **Display Name:** A localized name shown in widgets.
  - **Description:** A localized description for the property.
  - **Is User Editable:** Whether the property appears in the .ini file (see [8.1 Hidden Properties](#81-hidden-properties)).
  - **Is Constant:** Whether the property can be modified at runtime (see [8.2 Constant Properties](#82-constant-properties)).
  - **Should Render Widget:** Whether the dynamic widget method includes this property.
  - **Widget Override:** Replace the default widget with a custom widget class.
  - **Cheat Value:** An alternative value used when tampering is detected (see [8.3 Anti-Cheat Detection](#83-anti-cheat-detection)).

### 4.4 Data Types

EGC supports 9 data types:

| EGC Type | Unreal Engine Type | Example |
|----------|-------------------|---------|
| String | `FString` | `"Hello World"` |
| Integer | `int` | `42` |
| Float | `float` | `3.14` |
| Boolean | `bool` | `true` / `false` |
| Vector | `FVector` | `(X=1.0, Y=2.0, Z=3.0)` |
| Vector2D | `FVector2D` | `(X=1.0, Y=2.0)` |
| Rotator | `FRotator` | `(Pitch=0, Yaw=90, Roll=0)` |
| Color | `FLinearColor` | `(R=1.0, G=0.5, B=0.0, A=1.0)` |
| Transform | `FTransform` | Location + Rotation + Scale |

Each type supports up to **250 properties** (Property0 through Property249).

---

## 5. Using Properties in Blueprints

All EGC Blueprint nodes can be found by searching for **"EGC"** in the Blueprint editor. Every node returns a **Success** boolean indicating whether the operation was performed successfully.

### 5.1 Enum-Based Access (Recommended)

The recommended way to access properties is via their type-safe enum. When you create a property in the Project Settings, EGC assigns it to an enum value (e.g., `E_StringProperties::Property0`). The enum display name is configured in the settings.

**Setting a value:**
- Use the **Set {Type} Setting** node (e.g., `Set String Setting`, `Set Integer Setting`)
- Input: the property enum + the new value
- Output: Success boolean

**Getting a value:**
- Use the **Get {Type} Setting** node (e.g., `Get String Setting`, `Get Float Setting`)
- Input: the property enum
- Output: Success boolean + the current value

### 5.2 Legacy String-Based Access

For dynamic or data-driven scenarios, you can also access properties by their string name and category. These nodes have a **Legacy** suffix:

- **Set {Type} Setting Legacy** -- takes a Property name (FString) + Category (FString) instead of an enum
- **Get {Type} Setting Legacy** -- same approach for reading

> **Note:** The enum-based approach is recommended because it provides compile-time safety and auto-complete in the Blueprint editor. The legacy approach is useful when property names are determined at runtime.

### 5.3 Available Nodes Per Type

For each of the 9 data types, the following Blueprint nodes are available:

| Node | Description |
|------|-------------|
| **Set {Type} Setting** | Set a property value by enum |
| **Set {Type} Setting Legacy** | Set a property value by name + category |
| **Get {Type} Setting** | Read a property value by enum |
| **Get {Type} Setting Legacy** | Read a property value by name + category |
| **Reset {Type} Setting** | Reset a property to its default value |
| **On {Type} Setting Changed** | Get a delegate to listen for changes (see [Section 6](#6-listening-for-property-changes)) |
| **On {Type} Setting Changed Legacy** | Same, by name + category |
| **Get {Type} Property Configuration** | Read the full property config (default value, category, attributes) |
| **Get {Type} Widget For Property** | Get the widget instance for a specific property |
| **Get All {Type} Widgets** | Get all widget instances for this type |

Replace `{Type}` with: String, Integer, Float, Boolean, Vector, Vector2D, Rotator, Color, or Transform.

### 5.4 Resetting Properties

Use the **Reset {Type} Setting** node to reset an individual property back to its default value as configured in the Project Settings.

To reset **all** properties at once, use the **Reset Setting** node (found under EasyGameConfiguration > General).

---

## 6. Listening for Property Changes

EGC provides a delegate system that lets you react whenever a property value changes. This is useful for updating UI, triggering gameplay logic, or synchronizing state.

**How to use:**

1. Call the **On {Type} Setting Changed** node for the property you want to observe.
2. The node returns a delegate object and a Success boolean.
3. Bind a custom event to the delegate's **On {Type} Setting Changed** event.
4. Your event receives the **Old Value** and **New Value** as parameters.

**Example:** To listen for changes to a Float property:
1. Call `On Float Setting Changed` with the property enum.
2. Bind to the returned delegate's `On Float Setting Changed Signature` event.
3. Your bound event fires with `(float OldValue, float NewValue)` whenever that property is updated.

Legacy variants (`On {Type} Setting Changed Legacy`) work the same way using string name + category.

---

## 7. Managing Save States and Configurations

EGC provides three core nodes for managing configuration files, found under **EasyGameConfiguration > General**:

| Node | Description |
|------|-------------|
| **Create Or Load Setting** | Creates a new .ini configuration file or loads an existing one. Takes a `ConfigName` (the filename without extension) and an optional `OverrideWithCurrentProperties` flag. |
| **Unload Setting** | Unloads the current configuration. The optional `KeepProperties` flag determines whether current values are retained in memory. |
| **Reset Setting** | Resets all properties to their default values as defined in the Project Settings. |

**Typical workflow:**

1. On game start, call `Create Or Load Setting` with the desired config name (e.g., `"PlayerSettings"`).
2. Read and write properties using the Get/Set nodes during gameplay.
3. Changes are automatically persisted to the .ini file and save game.
4. Call `Unload Setting` when switching profiles or ending a session.

**Multiple profiles:** You can manage multiple configuration profiles by calling `Create Or Load Setting` with different config names (e.g., `"Slot1"`, `"Slot2"`, `"ServerConfig"`).

---

## 8. Advanced Customization Options

### 8.1 Hidden Properties

Set **Is User Editable** to `false` on a property to hide it from the .ini file. Hidden properties:

- Are not written to or read from the .ini configuration file.
- Can only be accessed through Blueprint nodes or C++ code.
- Are useful for internal state values, achievements, or sensitive data that should not be exposed to players.

### 8.2 Constant Properties

Set **Is Constant** to `true` (only available when Is User Editable is `false`) to make a property read-only at runtime:

- The **Get** nodes work normally and return the value.
- The **Set** nodes will fail (Success = false) and the value remains unchanged.
- Useful for defining immutable gameplay parameters that should be globally readable but never modified by game logic.

### 8.3 Anti-Cheat Detection

EGC includes a hash-based anti-cheat system for save game files. When enabled, EGC generates a hash of the save game data and detects unauthorized modifications.

**Setup:**

1. In Project Settings > EasyGameConfiguration > Security, enable **Detect Cheats** (enabled by default).
2. For each property, optionally enable **Use Cheat Value** and set a **Cheat Value**.
3. If a tampered save game is detected, properties with a configured cheat value will be set to that value instead of the manipulated one.

This protects against players manually editing save game files to gain unfair advantages.

### 8.4 Accessing Property Configurations

Use the **Get {Type} Property Configuration** node to read the full configuration of any property at runtime. This returns:

- **Config** (`FEGCSectionProperty`): Category, display name, description, type, and all flags (Is User Editable, Is Constant, Should Render Widget, Widget Index).
- **Type Config** (e.g., `FEGCStringType`): Default value, cheat value, and widget override class.

This is useful for building dynamic settings menus or debugging property configurations.

### 8.5 Overriding Widgets

Each property can have its default widget overridden with a custom widget class:

1. Create a new Widget Blueprint that inherits from the appropriate EGC widget class (e.g., `EasyGameConfigurationStringWidget`).
2. In the property configuration, set the **Widget Override** to your custom widget class.
3. The custom widget will be used instead of the default one when calling `Get {Type} Widget For Property` or `Get All {Type} Widgets`.

### 8.6 Widget Individualization

Beyond overriding widget classes, each property's widget can be individually customized:

- Set a **Display Name** and **Description** per property (supports localization via FText).
- Control the **Widget Index** to define the sort order in dynamically generated settings menus.
- Use **Should Render Widget** to exclude specific properties from widget generation while keeping them accessible via code.

---

## 9. Dynamic Widget Generation

One of the most powerful features of EGC is the ability to automatically generate widgets for all properties.

**Nodes:**

| Node | Description |
|------|-------------|
| **Get All Widgets** | Returns all widget instances for all property types, sorted by Widget Index. Takes a Player Controller as input. |
| **Get All {Type} Widgets** | Returns all widget instances for a specific type (e.g., `Get All String Widgets`). |
| **Get {Type} Widget For Property** | Returns the widget for a single specific property. |

By default, EGC creates a widget based on the data type of each property:

| Type | Default Widget |
|------|---------------|
| Boolean | Checkbox |
| String | Text input field |
| Integer / Float | Slider or numeric input field |
| Vector / Vector2D / Rotator / Transform | Numeric input fields per component |
| Color | Color picker / numeric input fields |

Each default widget provides a **Blueprint Implementable Event** that fires when the property value changes, allowing you to add custom logic in the widget's Event Graph.

Developers have full control over widget generation and can override the default widget styles or functionality via the widget override system (see [8.5 Overriding Widgets](#85-overriding-widgets)).

---

## 10. Use Cases

Here are several practical applications of EGC:

- **Custom Game Settings:** Provide players with the ability to adjust key gameplay parameters such as difficulty, player speed, or graphical options, all through an intuitive settings menu generated by EGC.
- **Server Configurations:** Set up and modify server settings like spawn rates, player limits, and server rules via easily adjustable .ini files, providing flexibility for multiplayer environments.
- **Hidden Properties:** Use hidden properties for values that should not be exposed to the player, such as internal states, game achievements, or sensitive server data.
- **Constant Properties:** Define immutable properties that are read globally but cannot be altered by players, ensuring the integrity of essential gameplay features.
- **Dynamic Widget Rendering:** Automatically generate interactive UI elements for all properties, allowing players to adjust settings on the fly.
- **Widget Individualization:** Customize each widget's style and layout to match the design aesthetic of your game.

---

## 11. Similar Games

Games that could benefit from EGC:

- **ARK: Survival Evolved:** Extensive use of server and game settings that need to be customized and managed through .ini files.
- **Conan Exiles:** Requires intricate server setups and game settings to be handled by both players and server administrators.
- **Rust:** Heavy reliance on custom server configurations and settings, which could be simplified with EGC.
- **Valheim:** Involves server-based configurations where settings are often adjusted for multiplayer experiences.

These games, with their need for server settings and customization options, highlight the potential utility of EGC in a variety of scenarios.

---

## 12. Technical Information

- **Plugin Version:** 1.3
- **Engine Version:** Unreal Engine 5.5
- **Code Modules:** EGC - EasyGameConfiguration [Runtime]
- **Number of Blueprints:** 9 (default widget Blueprints)
- **Number of Blueprint Nodes:** 94
- **Network Replicated:** No
- **Supported Platforms:** Win64, Android, Linux, LinuxArm64

---

## 13. Frequently Asked Questions (FAQ)

**Q: Does EGC support network replication?**
A: No, EGC is designed for local settings management and does not include network replication. However, it works perfectly in both single-player and multiplayer games. Configuration files are stored locally on each machine.

**Q: Can I add custom widgets for properties?**
A: Yes, you can override default widgets for each property by creating a Widget Blueprint that inherits from the appropriate EGC widget class and setting it as the Widget Override in the property configuration.

**Q: Does EGC support multiple save files?**
A: Yes, EGC allows the use of multiple save slots. Call `Create Or Load Setting` with different config names to create and switch between configuration profiles.

**Q: What is the maximum number of properties per type?**
A: Each data type supports up to 250 properties (Property0 through Property249). With 9 data types, this gives you a total of 2,250 possible properties.

**Q: What is the difference between enum-based and legacy access?**
A: Enum-based access (e.g., `Set String Setting`) uses type-safe enums for compile-time safety and auto-complete. Legacy access (e.g., `Set String Setting Legacy`) uses string-based property name + category, which is useful when property names are determined at runtime. The enum-based approach is recommended for most use cases.

**Q: How does the anti-cheat system work?**
A: EGC generates a hash of the save game data. When loading, if the hash does not match (indicating manual file editing), properties with a configured cheat value are set to that value instead. Enable this under Project Settings > EasyGameConfiguration > Security.

**Q: Can I listen for property changes at runtime?**
A: Yes, use the `On {Type} Setting Changed` nodes to get a delegate, then bind a custom event. Your event fires with the old and new values whenever the property is updated.

---

## 14. Contact Information

For any inquiries, suggestions, or troubleshooting, please reach out via email: f.wiegand00@web.de.

---

## 15. Patch Notes

### 15.1 Version 1.3

- Fixed a bug where Vector properties with non-uniform default values (e.g., X=1, Y=2, Z=3) were incorrectly serialized, causing the Y and Z components to always use the X value
- Fixed a crash that could occur when setting a property whose category or key was not yet initialized
- Fixed a bug where modifying Vector2D properties in the editor would incorrectly trigger a refresh of Vector Blueprint nodes instead of Vector2D nodes
- Improved memory management across the plugin
  - Added `NativeDestruct()` override to all 9 widget classes to properly clean up delegates and prevent memory leaks when widgets are destroyed
  - Resolved multiple memory leaks in configuration loading, saving, and delegate registration
  - Property lookups in Blueprint functions now properly release allocated memory after use
- Added null-checks to all `Get {Type} Widget` functions to gracefully handle missing player controllers instead of crashing
- Initialized all temporary widget pointers in `Get All {Type} Widgets` functions to prevent undefined behavior from uninitialized pointers
- Fixed uninitialized `SaveGameObject` pointers in configuration loading and saving functions that could cause crashes if `Cast` returned null
- Added null-check before `GenerateHashOfSaveGame` call to prevent crash when save game loading fails but anti-cheat detection is enabled
- Fixed unnecessary `FString` dereference in `GetSettingIntern` and legacy setter functions that could cause incorrect string handling
- Fixed `FLinearColor` default value to use alpha=1 (fully opaque) instead of alpha=0 (fully transparent), preventing invisible default colors
- Refactored delegate lookup pattern in `CallOnChangeDelegate` to use safe intermediate variables instead of fragile chained `Find()->Find()` calls, eliminating redundant map lookups and improving robustness

### 15.2 Version 1.2

- Improved savegame security
- Added anti-cheat detection for saved games
- Added toggle to enable/disable anti-cheating
- Cheat value can be configured for each property
  - if enabled and a cheat is detected, this value will be set
- Added keywords for all major plugin methods
  - "EGC" is now a known keyword
- Improved Project Settings UI
  - Convert all toggles with data to inline toggles
- Fixed bug where inline toggles were not saved immediately
- New Blueprint Nodes Reset {Type} Setting added for all types
  - reset individual properties to the default value

### 15.3 Version 1.1

- Updated Project for Fab
- Updated Project for Unreal Engine 5.5.0
