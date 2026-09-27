# REZ — ReShade Enhanced Zone

REZ is a custom ReShade shader package and preset collection designed for **S.T.A.L.K.E.R. G.A.M.M.A. / Anomaly on DirectX 11**.

REZ does **not** include ReShade itself. Install ReShade separately from the official ReShade website, then copy the REZ files into the locations described below.

---

## Included Files

Your REZ package may contain:

- `REZ.fx` — the REZ shader
- `REZ_Default.ini` — balanced photorealistic preset
- `REZ_Bodycam.ini` — sharper, flatter digital/bodycam-style preset
- `REZ_Cinematic.ini` — darker cinematic preset
- `REZ_LICENSE.txt` — license terms
- `REZ_CREDITS.txt` — credits and acknowledgements
- `README.md` — this file

The `.fx` file is the shader itself.  
The `.ini` files are ReShade presets.

---

# Installation

## 1. Locate your G.A.M.M.A. Anomaly folder

You need the **actual Anomaly game folder used by G.A.M.M.A.**, not the Mod Organizer 2 folder.

Inside it you should see folders/files similar to:

```text
Anomaly/
├── appdata/
├── bin/
├── gamedata/
└── AnomalyLauncher.exe
```

The important folder for ReShade is:

```text
Anomaly/bin/
```

---

## 2. Check which DirectX 11 executable G.A.M.M.A. uses

Open:

```text
Anomaly/bin/
```

G.A.M.M.A. normally runs one of the DirectX 11 executables in this folder, for example:

```text
AnomalyDX11AVX.exe
```

or:

```text
AnomalyDX11.exe
```

Use the **same executable that your G.A.M.M.A. launcher / Mod Organizer 2 configuration actually launches**.

For a normal modern G.A.M.M.A. installation this is commonly:

```text
Anomaly/bin/AnomalyDX11AVX.exe
```

Do **not** install ReShade to `AnomalyLauncher.exe`.

---

## 3. Install ReShade

Download the current ReShade installer from the official ReShade website:

```text
https://reshade.me/
```

Run the installer.

When asked to select a game/application:

1. Choose **Browse**.
2. Open your G.A.M.M.A. `Anomaly/bin/` folder.
3. Select the DirectX 11 executable you identified above, normally `AnomalyDX11AVX.exe`.
4. When ReShade asks for the rendering API, choose:

```text
DirectX 10/11/12
```

5. Continue through the ReShade installation.

### Shader packages

REZ does not require a large collection of third-party effects, but it uses the normal ReShade include files such as:

```text
ReShade.fxh
ReShadeUI.fxh
```

During ReShade setup, installing the **standard ReShade shader/effect package** is recommended so these files are available.

If ReShade is already installed and working correctly in G.A.M.M.A., you do not need to reinstall it.

---

## 4. Important G.A.M.M.A. launcher setting

Some G.A.M.M.A. launcher versions include an option that removes ReShade files during an install/update.

If your launcher has an option similar to:

```text
Delete ReShade
```

make sure it is **disabled / unticked** before running an update or install operation.

Otherwise the launcher may remove the ReShade installation from the Anomaly folder.

---

# Installing REZ

## 5. Install `REZ.fx`

After ReShade has been installed, your Anomaly `bin` folder should contain a ReShade shader directory similar to:

```text
Anomaly/bin/reshade-shaders/
```

Copy:

```text
REZ.fx
```

into:

```text
Anomaly/bin/reshade-shaders/Shaders/
```

The result should look like:

```text
Anomaly/
└── bin/
    ├── AnomalyDX11AVX.exe
    ├── ReShade.ini
    ├── reshade-shaders/
    │   ├── Shaders/
    │   │   └── REZ.fx
    │   └── Textures/
    └── ...
```

If you use a custom ReShade effect search path, place `REZ.fx` in any folder listed under **Effect Search Paths** instead.

---

## 6. Install the REZ presets

Copy the supplied preset files:

```text
REZ_Default.ini
REZ_Bodycam.ini
REZ_Cinematic.ini
```

into:

```text
Anomaly/bin/
```

Example:

```text
Anomaly/
└── bin/
    ├── AnomalyDX11AVX.exe
    ├── REZ_Default.ini
    ├── REZ_Bodycam.ini
    ├── REZ_Cinematic.ini
    ├── ReShade.ini
    └── reshade-shaders/
        └── Shaders/
            └── REZ.fx
```

The presets do not have to be stored beside the executable, but this is the simplest layout and makes them easy to find in ReShade.

`REZ_LICENSE.txt`, `REZ_CREDITS.txt`, and this README do not need to be copied into the game directory.

---

# First Launch

## 7. Start G.A.M.M.A.

Launch G.A.M.M.A. normally using your usual Mod Organizer 2 / G.A.M.M.A. launcher setup.

When the game starts, you should see the ReShade loading message near the top of the screen.

Once in game, press:

```text
Home
```

to open the ReShade interface.

---

## 8. Select a REZ preset

At the top of the ReShade **Home** tab, open the preset selector and choose one of:

```text
REZ_Default.ini
REZ_Bodycam.ini
REZ_Cinematic.ini
```

Recommended starting point:

### REZ Default
Balanced cold / photorealistic presentation.

### REZ Bodycam
Flatter, sharper and more digital presentation with optional handheld-camera characteristics.

### REZ Cinematic
Darker, more dramatic tonal response.

You can switch between the presets at any time from the ReShade preset selector.

---

# Performance Mode

REZ is designed to work with ReShade **Performance Mode**.

After selecting a preset and confirming that everything is working, Performance Mode may be enabled from the bottom of the ReShade interface.

Some optional REZ effects are controlled by their **technique checkbox** rather than only by a slider. This is intentional and improves reliability in Performance Mode.

Examples include:

- Handheld Camera
- Film Density Response
- Film Softness
- Depth of Field
- Lens Housing / Casing
- Debug tools

---

# Depth of Field

REZ includes an optional depth-based DOF effect.

For DOF to work, ReShade must have access to the correct game depth buffer.

To check this:

1. Enable the `REZ_DEPTH_DEBUG` technique.
2. The screen should display usable scene depth.
3. If the image is completely flat or incorrect, ReShade has not selected a usable depth buffer.

DOF will not work correctly until ReShade depth access is functioning.

Disable `REZ_DEPTH_DEBUG` again after testing.

---

# Troubleshooting

## REZ does not appear in ReShade

Check that:

```text
REZ.fx
```

is located in:

```text
Anomaly/bin/reshade-shaders/Shaders/
```

Then open ReShade and press **Reload**.

Also check **Settings → Effect Search Paths** and make sure the folder containing `REZ.fx` is listed.

---

## ReShade does not appear when the game starts

The most common cause is installing ReShade to the wrong executable.

Reinstall ReShade and select the actual DirectX 11 game executable inside:

```text
Anomaly/bin/
```

For most G.A.M.M.A. installations this is:

```text
AnomalyDX11AVX.exe
```

Do not select `AnomalyLauncher.exe`.

Also confirm that you selected:

```text
DirectX 10/11/12
```

during ReShade setup.

---

## ReShade disappeared after updating G.A.M.M.A.

Check the G.A.M.M.A. launcher for a **Delete ReShade** option.

If present, keep it disabled before performing launcher update/install operations.

You may need to reinstall ReShade afterward if the launcher already removed it.

---

## REZ reports that `ReShade.fxh` or `ReShadeUI.fxh` is missing

Your standard ReShade shader/include files are missing or the shader search path is incorrect.

Run the official ReShade installer again and install the standard ReShade shader package, or verify the ReShade **Effect Search Paths**.

Do not download random replacement DLLs or include files from unofficial sources.

---

## Presets are not listed

You can either:

- place the REZ `.ini` presets directly in `Anomaly/bin/`, or
- use the browse button beside the ReShade preset selector and navigate to wherever you stored them.

---

## An effect slider appears to do nothing

Some REZ features have a corresponding technique in the upper ReShade technique list.

Make sure that technique is enabled.

For example, changing DOF controls will not affect the image if `REZ_DOF` is disabled.

---

# Updating REZ

When installing a newer version of REZ:

1. Close the game.
2. Replace the old:

```text
reshade-shaders/Shaders/REZ.fx
```

with the new `REZ.fx`.
3. Replace the REZ preset `.ini` files if updated presets are included.
4. Start the game.
5. Open ReShade and press **Reload** if necessary.

If you have created your own custom preset, back it up before replacing any `.ini` files.

---

# Uninstalling REZ

To remove REZ without uninstalling ReShade:

Delete:

```text
Anomaly/bin/reshade-shaders/Shaders/REZ.fx
```

and delete any REZ presets you installed:

```text
REZ_Default.ini
REZ_Bodycam.ini
REZ_Cinematic.ini
```

This removes REZ while leaving ReShade itself installed.

---

# Credits

**REZ — ReShade Enhanced Zone**

Developed by **davexmachina**.

REZ is an independent ReShade shader package inspired by the visual approaches and camera/post-processing philosophy of **PRZ** and **RELOOK**.

REZ is an independent implementation and contains no code from those projects.

Built for use with the **ReShade** framework.

REZ is not affiliated with PRZ, RELOOK, ReShade, or GSC Game World.

See `REZ_CREDITS.txt` for the full credits notice.

---

# License

REZ is proprietary software distributed under the **REZ Personal Use License**.

Purchase does not transfer ownership of the software.

Redistribution, re-uploading, resale, bundling, or publication of the REZ files is prohibited except where explicitly permitted by the license.

Screenshots, videos, livestreams, reviews, and other content created while using REZ are permitted, including monetized content.

See:

```text
REZ_LICENSE.txt
```

for the complete license terms.

---

## Notes

REZ is designed specifically around a DirectX 11 S.T.A.L.K.E.R. G.A.M.M.A. / Anomaly setup.

Windows is the primary supported installation path described in this guide. ReShade can also be used in some Wine / Proton / Linux configurations, but installation details vary substantially between setups and are not covered by these instructions.
