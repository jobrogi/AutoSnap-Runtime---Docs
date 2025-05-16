# AutoSnap – Runtime

AutoSnap – Runtime brings powerful, grid-based snapping and transform controls to runtime actors in your Unreal Engine project. Designed for user-generated content workflows, in-game editors, or simulation-style building systems, this plugin gives developers precise, hotkey-controlled actor manipulation and snapping without needing the editor.

> ✅ Built for Unreal Engine 5.3+  
> 🧩 Runtime-Only | Blueprint Compatible | No External Dependencies

---

## 📦 Features

- Grid-snapped actor movement in world space  
- Runtime gizmo with axis & plane-based dragging (X/Y/Z, XY/XZ/YZ)  
- Dynamic grid that follows actors  
- Adjustable snap size  
- Tag-based actor selection system  
- Clean Blueprint integration (no C++ required)  
- Designed for runtime UGC or in-game building

---

## 🚀 Getting Started

### 1. Enable the Plugin

In the UE editor, go to **Edit > Plugins**, search for `AutoSnap - Runtime`, and enable it. Restart the editor if required.

### 2. Add the Component

In your player character or controller Blueprint, add the `AutoSnapControllerComponent`.

The component will automatically:
- Spawn the runtime gizmo and grid visualizer
- Handle input mapping and selection
- Snap tagged actors during drag

### 3. Assign Required Fields

In the component's Details panel:  
*(Note: Most fields are auto-filled during runtime using plugin defaults)*

- **Grid Visualizer Class**: Assign `BP_GridVisualizer`  
- **Runtime Gizmo Class**: Assign `BP_Gizmo`  
- **Input Mapping**: Assign `IMC_AutoSnap`  
- **Select Action**: Assign `IA_LeftClick`  
- (Optional) Enable **Require Actor Tag for Selection** and set the tag to `"SnapSelectable"`

---

### 🔄 Default vs. Custom Asset Behavior

If you want to use your own **Input Mapping Context**, **Input Action**, **Grid Visualizer**, or **Gizmo Class**, simply assign them in the Details panel.

If you **leave any of these empty**, the plugin will automatically use its built-in defaults during `BeginPlay`.

---

## 🎯 Optional: Add Custom Trace Channel (For Hover Effects Only)

AutoSnap uses a custom trace channel (`ECC_Gizmo`) to detect when the mouse is hovering over gizmo arrows or planes. This enables **visual feedback** like changing the arrow’s color when hovered — it does **not affect** snapping, actor selection, or movement.

If you don't set this up, the plugin will still work perfectly — just without visual hover cues.

---

### 🔧 Why Use It?

This line from the code enables on-hover visual effects:

```cpp
bool bHit = GetWorld()->LineTraceSingleByChannel(Hit, Start, End, ECC_Gizmo, Params);
```

If you haven't defined `ECC_Gizmo` in your project, this line will fall back to default behavior and the hover colors won't change.

---

### 📝 How to Set It Up in Unreal Engine

#### Go to Project Settings:

- Open your project
- Navigate to **Edit > Project Settings**

#### Search for Engine → Collision:

- In the left panel, search for **"Collision"**
- Click on **Engine > Collision > Trace Channels**

#### Add a New Trace Channel:

- Click **New Trace Channel**
- Name it: `Gizmo`
- Set the default response to: `Block`

#### Apply the Trace Channel to Gizmo Meshes (Optional):

If you're editing the gizmo Blueprint or mesh component:

- Set **Collision Presets** to `Custom`
- Under **Trace Responses**, set `Gizmo` to `Block`
- All other responses can stay as `Ignore`

---

### ✅ Result

When the player hovers their mouse over a gizmo arrow or plane, the mesh will highlight to indicate it's interactive. This improves visual feedback for dragging, but has no effect on logic or snapping functionality.

> This step is **100% optional** and purely enhances the user experience with visual feedback.
