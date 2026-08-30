# Build Instructions

This document describes how to build the GmailCreator project locally and in CI/CD environments.

## Prerequisites

### Local Development
- **Windows** (Windows 10 or later recommended)
- **.NET Framework 4.8** (required for running and developing)
- **Visual Studio 2019** or later, or **MSBuild** tools
- **NuGet** (for package management)
- **Google Chrome** installed (required at runtime)

### GitHub Actions (CI/CD)
- Automated via GitHub Actions on push/PR
- No manual setup required

## Building Locally

### Option 1: Visual Studio IDE

1. Open `GmailCreator.sln` in Visual Studio
2. Select **Release** configuration from the dropdown (top toolbar)
3. Right-click the solution and select **Build Solution** (or press `Ctrl+Shift+B`)
4. The output executable will be located at: `bin/Release/GmailCreator.exe`

### Option 2: Command Line (MSBuild)

```powershell
# Navigate to the project directory
cd "C:\path\to\Free-Gmail-Creator-Open-Source-main"

# Restore NuGet packages
nuget restore GmailCreator.sln

# Build the solution in Release mode
msbuild GmailCreator.sln /p:Configuration=Release /p:Platform=AnyCPU
```

### Option 3: Command Line (dotnet)

```powershell
cd "C:\path\to\Free-Gmail-Creator-Open-Source-main"

# Restore packages
dotnet restore

# Build solution
dotnet build --configuration Release
```

## Build Output

After a successful build, the executable will be located at:
```
bin/Release/GmailCreator.exe
```

## Continuous Integration (GitHub Actions)

The project includes an automated build workflow (`.github/workflows/build.yml`) that:

1. **Triggers on:**
   - Push to `main`, `master`, or `develop` branches
   - Pull requests targeting those branches
   - Manual workflow dispatch

2. **Performs:**
   - Checks out the code
   - Sets up MSBuild and NuGet
   - Restores NuGet packages
   - Builds the solution in Release mode
   - Uploads build artifacts (`.exe`, `.dll`, etc.)
   - On failure, uploads build logs for debugging

3. **Access build artifacts:**
   - Go to the GitHub Actions tab in the repository
   - Click the workflow run
   - Download artifacts from the "Artifacts" section

## Troubleshooting

### "dotnet: command not found"
Install the .NET SDK or use MSBuild directly:
```powershell
msbuild GmailCreator.sln /p:Configuration=Release
```

### "Cannot find NuGet packages"
Manually restore packages:
```powershell
nuget restore GmailCreator.sln
```

### Build fails with "Missing assembly references"
Ensure all NuGet packages are restored and the DLL files (`BotModule.dll`, `ChromeController.dll`) are present in the project root directory.

### GitHub Actions workflow fails
Check the workflow logs by:
1. Going to the **Actions** tab in the GitHub repository
2. Clicking the failed workflow run
3. Reviewing the detailed logs for specific error messages

## Project Structure

```
Free-Gmail-Creator-Open-Source-main/
├── .github/
│   └── workflows/
│       └── build.yml              # GitHub Actions workflow
├── bin/                            # Build output directory
├── obj/                            # Intermediate build files
├── Properties/
│   └── AssemblyInfo.cs            # Assembly metadata
├── App.config                      # Application configuration
├── GmailCreator.csproj            # Project file
├── GmailCreator.sln               # Solution file
├── Program.cs                      # Entry point
├── Options.cs                      # CLI argument definitions
├── ChromeController.dll           # External dependency
├── BotModule.dll                  # External dependency
├── ChromeController.xml           # API documentation
├── packages.config                # NuGet packages reference
├── .gitignore                     # Git ignore rules
├── .editorconfig                  # Code style settings
├── README.md                      # Project readme
├── LICENSE                        # MIT License
└── BUILD.md                       # This file
```

## Additional Notes

- **Target Framework:** .NET Framework 4.8
- **Platform:** AnyCPU
- **Build Configuration:** Debug (for development) or Release (for distribution)
- **Dependencies:** Managed via `packages.config` (NuGet)
- **External Libraries:** `BotModule.dll` and `ChromeController.dll` are required for runtime

## Support

For issues or questions, please refer to the README.md or contact the project maintainers.
