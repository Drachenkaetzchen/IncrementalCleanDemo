This is a minimal example of the IncrementalClean issue with Fody 3.2.12+ and PropertyChanged.Fody.

How to reproduce (in Visual Studio 2017 Community Edition):

- Check out this repository
- Use Build > Build solution
- Verify that NAudio.dll is there in ClassLibraryIndirect\bin\Debug
- Use Build > Build solution again, note that the project is rebuilt every time
- After the build, NAudio.dll is gone from ClassLibraryIndirect\bin\Debug

Additional notes:

- This only seem to happen if the NuGet packages use packages.config (which I believe is the default in VS2017)
- I'm using PropertyChanged.Fody for this repro, it could be that PropertyChanged.Fody is the culprit

To verify that this bug was introduced in Fody 3.2.12, manage the NuGet packages for the project and
downgrade to 3.2.11. Upon rebuild, the project is marked as up-to-date and I couldn't get MSBuild to ever
jump into IncrementalClean.