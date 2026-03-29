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
6. [Managing Save States and Configurations](#6-managing-save-states-and-configurations)
7. [Advanced Customization Options](#7-advanced-customization-options)
   - [7.1 Hidden Properties](#71-hidden-properties)
   - [7.2 Constant Properties](#72-constant-properties)
   - [7.3 Accessing Property Configurations](#73-accessing-property-configurations)
   - [7.4 Overriding Widgets](#74-overriding-widgets)
   - [7.5 Widget Individualization](#75-widget-individualization)
8. [Dynamic Widget Generation](#8-dynamic-widget-generation)
9. [Use Cases](#9-use-cases)
10. [Similar Games](#10-similar-games)
11. [Technical Information](#11-technical-information)
12. [Frequently Asked Questions (FAQ)](#12-frequently-asked-questions-faq)
13. [Contact Information](#13-contact-information)
14. [Additional Notes](#14-additional-notes)
15. [Patch Notes](#15-patch-notes)
    - [15.1 Version 1.1](#151-version-11)
    - [15.2 Version 1.2](#152-version-12)
    - [15.3 Version 1.3](#153-version-13)

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
- **Widget Individualization:** Customize each property's UI widget, providing developers with full control over their settings menus.
- **Flexible Shortcuts:** Access configuration settings easily through multiple shortcut buttons in the Blueprint editor, widget graph, or main project settings.

---

## 3. Installation

### Prerequisites

Before using EGC, ensure you have the following installed:

- Unreal Engine 5 (or higher)
- Basic knowledge of Unreal Blueprints or C++

### Steps to Install EGC

1. Download the EGC plugin from the Epic Games Marketplace.
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

- Set the save location for your configuration files.
- Configure the Enum Editor Display Name for Blueprints.
- Activate/disable the option for automatically refreshing EGC methods when creating or deleting properties.
- Activate/disable starting the game with the default configuration file (useful in non-multi-world/save scenarios).
- Set the default configuration file name if the above option is activated.
- Toggle the visibility of the Blueprint and Widget Config Settings buttons.

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
- Configure optional attributes like Hidden, Constant, Widget overrides, and Anti-Cheat settings.

### 4.4 Data Types

EGC supports the following data types:

- String
- Integer
- Float
- Boolean
- Vector
- Vector2D
- Rotator
- Color
- Transform

---

## 5. Using Properties in Blueprints

EGC provides Blueprint nodes for getting, setting, and resetting properties. For each supported data type, there are dedicated getter and setter nodes.

Properties can be accessed either by their enum value (recommended for type-safety) or by their string name and category (legacy method).

All nodes return a Success boolean indicating whether the operation was performed successfully.

---

## 6. Managing Save States and Configurations

EGC supports multiple save states and configuration files. You can:

- Save the current configuration to a .ini file.
- Load a configuration from a .ini file.
- Reset properties to their default values.
- Manage multiple configuration profiles for different scenarios (e.g., different save slots).

---

## 7. Advanced Customization Options

### 7.1 Hidden Properties

Hidden properties are not written to .ini files and are only accessible through code. This is useful for internal state values or sensitive data that should not be exposed to players.

### 7.2 Constant Properties

Constant properties can be read globally but cannot be modified by players. They are useful for defining immutable gameplay parameters.

### 7.3 Accessing Property Configurations

You can access the full configuration of any property, including its category, key, default value, and all optional attributes through the EGC API.

### 7.4 Overriding Widgets

Each property can have its default widget overridden with a custom widget class. This allows developers to create specialized UI elements for specific settings.

### 7.5 Widget Individualization

Beyond overriding, widgets can be individually customized per property. This provides full control over the appearance and behavior of each settings element.

---

## 8. Dynamic Widget Generation

One of the most powerful features of EGC is the ability to automatically generate widgets for all properties. By default, EGC creates a widget based on the data type of each property, removing the need for manual UI creation.

Widgets are generated as follows:

- **Booleans:** Checkboxes
- **Strings:** Text input fields
- **Integers/Floats/Vector/Transform/Color/Rotator:** Sliders or numeric input fields

Developers have full control over widget generation and can override the default widget styles or functionality via built-in methods. This allows for a balance between automation and customization, making UI creation fast and flexible.

---

## 9. Use Cases

Here are several practical applications of EGC:

- **Custom Game Settings:** Provide players with the ability to adjust key gameplay parameters such as difficulty, player speed, or graphical options, all through an intuitive settings menu generated by EGC.
- **Server Configurations:** Set up and modify server settings like spawn rates, player limits, and server rules via easily adjustable .ini files, providing flexibility for multiplayer environments.
- **Hidden Properties:** Use hidden properties for values that should not be exposed to the player, such as internal states, game achievements, or sensitive server data.
- **Constant Properties:** Define immutable properties that are read globally but cannot be altered by players, ensuring the integrity of essential gameplay features.
- **Dynamic Widget Rendering:** Automatically generate interactive UI elements for all properties, allowing players to adjust settings on the fly.
- **Widget Individualization:** Customize each widget's style and layout to match the design aesthetic of your game.

---

## 10. Similar Games

Games that could benefit from EGC:

- **ARK: Survival Evolved:** Extensive use of server and game settings that need to be customized and managed through .ini files.
- **Conan Exiles:** Requires intricate server setups and game settings to be handled by both players and server administrators.
- **Rust:** Heavy reliance on custom server configurations and settings, which could be simplified with EGC.
- **Valheim:** Involves server-based configurations where settings are often adjusted for multiplayer experiences.

These games, with their need for server settings and customization options, highlight the potential utility of EGC in a variety of scenarios.

---

## 11. Technical Information

- **Code Modules:** EGC - EasyGameConfiguration [Runtime]
- **Number of Blueprints:** 9 (Widgets)
- **Network Replicated:** No
- **Supported Platforms:** Win64, Android, Linux, LinuxArm64

---

## 12. Frequently Asked Questions (FAQ)

**Q: Does EGC support network replication?**
A: No, EGC is designed for local settings management and does not include network replication. However, it works perfectly in both single-player and multiplayer games.

**Q: Can I add custom widgets for properties?**
A: Yes, you can override default widgets for each property, allowing full customization of the settings menu.

**Q: Does EGC support multiple save files?**
A: Yes, EGC allows the use of multiple save slots, providing flexibility for creating, loading, and managing different configuration profiles.

---

## 13. Contact Information

For any inquiries, suggestions, or troubleshooting, please reach out via email: f.wiegand00@web.de.

---

## 14. Additional Notes

Stay tuned for updates! The current version does not include an example project, but future releases may include additional features and improvements.

---

## 15. Patch Notes

### 15.1 Version 1.1

- Updated Project for Fab
- Updated Project for Unreal Engine 5.5.0

### 15.2 Version 1.2

- Extended support for Unreal Engine 5.2 and 5.1
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

### 15.3 Version 1.3

- Fixed a bug where Vector properties with non-uniform default values (e.g., X=1, Y=2, Z=3) were incorrectly serialized, causing the Y and Z components to always use the X value
- Fixed a crash that could occur when setting a property whose category or key was not yet initialized
- Fixed a bug where modifying Vector2D properties in the editor would incorrectly trigger a refresh of Vector Blueprint nodes instead of Vector2D nodes
- Improved memory management across the plugin
  - Resolved multiple memory leaks in configuration loading, saving, and delegate registration
  - Property lookups in Blueprint functions now properly release allocated memory after use
