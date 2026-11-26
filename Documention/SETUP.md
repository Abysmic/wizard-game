# Wizard Game — Development Setup

This guide explains how to set up the development environment for Wizard Game on Windows or macOS.

## Tech Stack

- **Game Engine:** Godot 4 (.NET/C# version)
- **Programming Language:** C#
- **Framework:** .NET
- **Dependency Management:** NuGet
- **IDE:** Visual Studio Code
- **Version Control:** Git + GitHub

---

## 1. Install Prerequisites

### 1.1 Git

Git is required for cloning the repository and managing version control.

**Windows:**
https://git-scm.com/downloads/win

**macOS:**
https://git-scm.com/downloads/mac

On macOS, Git may already be installed.

Verify installation:

```bash
git --version
```

### 1.2 .NET SDK

The .NET SDK provides the C# compiler, build tools, and NuGet dependency management.

Download the .NET SDK:

https://dotnet.microsoft.com/download

Select the appropriate installer:

- Windows: x64 or ARM64, depending on your system.
- macOS: Apple Silicon (ARM64) or Intel (x64).

Install an SDK compatible with the project's target framework and Godot version.

Verify installation:

```bash
dotnet --version
dotnet --list-sdks
```

### 1.3 Godot Engine

Download Godot:

**Windows:**
https://godotengine.org/download/windows/

**macOS:**
https://godotengine.org/download/macos/

**IMPORTANT: Download the .NET version of Godot, NOT the standard version.**

Use the same Godot version as the rest of the team to avoid compatibility issues.

On Windows, the downloaded archive may contain two executables:

- `Godot_v4.x_mono_win64.exe` — Main Godot editor.
- `Godot_v4.x_mono_win64_console.exe` — Editor with an additional console for debugging.

Launch the first executable for normal development.

On macOS, launch the Godot application.

### 1.4 Visual Studio Code

Download VS Code:

https://code.visualstudio.com/

Install the following extensions:

1. C# — Microsoft
2. C# Dev Kit — Microsoft
3. Godot Tools — geequlim

These provide C# IntelliSense, debugging capabilities, and Godot integration.

---

## 2. Clone the Repository

Open PowerShell (Windows) or Terminal (macOS).

Clone the repository:

```bash
git clone https://github.com/Abysmic/wizard-game.git
```

Navigate into the repository:

```bash
cd wizard-game
```

Replace the repository URL with the actual GitHub URL.

---

## 3. Open the Godot Project

The Godot project is located inside the `wizard-game-godot` directory.

Repository structure:

```text
wizard-game/
│
├── wizard-game-godot/
│   ├── project.godot
│   ├── WizardGameGodot.csproj
│   ├── WizardGameGodot.sln
│   └── ...
│
├── LICENSE
├── README.md
└── SETUP.md
```

To open the project:

1. Launch Godot .NET.
2. Click **Import** in the Project Manager.
3. Navigate to the cloned repository.
4. Select `wizard-game-godot/project.godot`.
5. Import and open the project.

Godot will automatically generate its local cache files.

Do not create a new Godot project.

---

## 4. Configure VS Code

Open the cloned repository in VS Code.

Make sure the following extensions are installed:

- C# (Microsoft)
- C# Dev Kit (Microsoft)
- Godot Tools (geequlim)

Next, configure Godot to use VS Code.

1. Open Godot.
2. Navigate to **Editor Settings**.
3. Find **Dotnet → Editor → External Editor**.
4. Select **Visual Studio Code**.

On macOS, Editor Settings may be located under the application's menu.

Now, opening C# scripts from Godot should launch VS Code.

---

## 5. Restore Dependencies

Our project uses NuGet for C# dependency management.

NuGet is included with the .NET SDK, so no additional installation is required.

The project's dependencies are defined in:

```text
wizard-game-godot/WizardGameGodot.csproj
```

This file serves a similar purpose to `pyproject.toml` in Python projects.

Navigate to the Godot project directory:

```bash
cd wizard-game-godot
```

Restore dependencies:

```bash
dotnet restore
```

This downloads the required NuGet packages.

No Poetry environment or Python virtual environment is needed.

---

## 6. Build the Project

From inside the `wizard-game-godot` directory, run:

```bash
dotnet build
```

A successful build should display something similar to:

```text
Build succeeded.
    0 Warning(s)
    0 Error(s)
```

This confirms that the C# project and its dependencies are configured correctly.

You can also build the C# project directly from the Godot editor.

---

## 7. Run the Game

1. Open the project in Godot.
2. Allow Godot to finish importing assets.
3. Build the C# project if necessary.
4. Press **F5** or click the Play button.

If a main scene has not been configured yet, Godot will prompt you to select one.

Once a main scene exists, the game should launch normally.

---

## 8. Project Structure

All game-related code and assets belong inside the `wizard-game-godot` directory.

As development progresses, the project will follow a structure similar to:

```text
wizard-game/
│
├── wizard-game-godot/
│   │
│   ├── assets/
│   │   ├── sprites/
│   │   ├── tilesets/
│   │   ├── audio/
│   │   └── fonts/
│   │
│   ├── scenes/
│   │   ├── player/
│   │   ├── world/
│   │   ├── enemies/
│   │   ├── npcs/
│   │   ├── dungeons/
│   │   └── ui/
│   │
│   ├── scripts/
│   │   ├── player/
│   │   ├── combat/
│   │   ├── interaction/
│   │   ├── enemies/
│   │   ├── npc/
│   │   └── core/
│   │
│   ├── resources/
│   │
│   ├── project.godot
│   ├── WizardGameGodot.csproj
│   └── WizardGameGodot.sln
│
├── docs/
├── tools/
├── .gitignore
├── .gitattributes
├── LICENSE
├── README.md
└── SETUP.md
```

**Note:** Directories will be created as needed during development.

There is no need to create every directory immediately.

---

## 9. Git Configuration

Generated files should not be committed to GitHub.

Ensure the repository's `.gitignore` includes:

```gitignore
# Godot generated files
.godot/

# .NET build artifacts
bin/
obj/

# IDE settings
.vs/
.idea/

# Operating system files
.DS_Store
Thumbs.db
```

Files that SHOULD be committed include:

- C# source files (`.cs`)
- Godot scenes (`.tscn`)
- Godot resources (`.tres`)
- Game assets
- `project.godot`
- `.csproj` files
- `.sln` files
- Documentation

---

## 10. Troubleshooting

### .NET command not recognized

If the terminal cannot find `dotnet`:

1. Confirm that the .NET SDK was installed.
2. Restart the terminal.
3. Run:

```bash
dotnet --version
```

### C# is unavailable in Godot

Ensure that the .NET version of Godot was installed.

The standard Godot version does not provide C# support.

### NuGet restore fails

Try:

```bash
dotnet restore
```

Check that:

- An appropriate .NET SDK is installed.
- You have an internet connection.
- The `.csproj` file has not been modified incorrectly.

### Godot project does not open

Ensure you are importing:

```text
wizard-game-godot/project.godot
```

Do not import the repository root.

### VS Code does not recognize C#

Verify that the C# and C# Dev Kit extensions are installed and enabled.

Allow the C# project to finish loading.

---

## 11. Development Workflow

When starting development:

1. Pull the latest changes.
2. Open the Godot project.
3. Write C# code in VS Code.
4. Build and test changes in Godot.
5. Commit and push your work.

Example:

```bash
git pull
```

After completing changes:

```bash
git add .
git commit -m "feat: describe your change"
git push
```

For collaborative development, create a feature branch and open a pull request instead of pushing directly to the main branch.

---

## Setup Complete

Your environment is ready when:

- [ ] Git is installed.
- [ ] .NET SDK is installed.
- [ ] Godot .NET is installed.
- [ ] VS Code and required extensions are installed.
- [ ] Repository is cloned.
- [ ] Existing Godot project opens successfully.
- [ ] `dotnet restore` completes successfully.
- [ ] `dotnet build` completes successfully.
- [ ] Godot is configured to use VS Code.

You are now ready to contribute to Wizard Game!