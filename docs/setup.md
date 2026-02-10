# Installation & Setup

This section explains how to install the plugin, activate it in your project, and perform the initial setup.

---

## Installation

### Marketplace / Plugin Folder

- **Marketplace installation**:  
  If you obtained the plugin from the Unreal Engine Marketplace, download and install it directly into your project using the Marketplace interface.
- **Manual installation**:  
  If you have the plugin as a folder, place it under your project’s `Plugins` directory: `<YourProject>/Plugins/<Here>`

### Activation in Unreal Engine

1. Open your Unreal Engine project.
2. Go to **Edit → Plugins**.
3. Locate the plugin under the **Installed → Gameplay** section.
4. Check the box to **enable** the plugin.
5. Restart the editor if prompted.

### Dependencies

- The plugin is designed to be self-contained.
- Ensure your project meets the minimum requirements for Unreal Engine 5.x.
- No additional third-party plugins are required, but any dependent modules (if used in your project) must also be enabled.

---

## First Setup

### Activate in a New Project

- Create a **new blank project** (recommended for testing first).
- Enable the plugin as described above.
- Confirm that the plugin appears in the **Plugins** panel and is active.

### Global Plugin Settings

- Navigate to **Edit → Project Settings → Domino**.
- Configure global options such as:
- Default behavior component settings
- Logging levels
- Debug options (e.g., enable visual logger integration)

### Verification

- Open the **Output Log** and confirm that the plugin modules load without errors:

```
[Domino] Module loaded successfully
[Domino] Behavior Component initialized
```

- Optionally, drag a **Behavior Component** onto a test actor and press **Play** in PIE to ensure everything works as expected.
