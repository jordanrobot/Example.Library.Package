Example Library Package
===

A simple example showing how to pack any library file into a nuget package.  Let's say there is a certain third party software package that you want to make use of in your code.  Instead of resolving the packages to your GAC or hardcoding paths to dll files in your project file, you can instead pack those library files into a private nuget package feed.  This simplifies dependencies for these third party libraries, especially when working with different development machines, in CI/CD, or with other contributors.

At the simplest, we're just putting the library files and any xml documentation files in the lib folder, and editing the nuspec file to reference those files.

The `build.ps1` file is a simple routine that will delete all existing nuget packages in the directory and create a new package based on your nuspec file.

The `deploy.ps1` is a simple script to push your nuget to your private package feed.  Before you run, please replace the `"private nuget feed"` text with your feed's address.

### Thoughts on Versioning

I'll pause here to remind you to give thought towards versioning.  When supporting multiple releases of the third-party library(s), consider how the nuget package versioning may be utilized to improve downstream consumption of the package.  Consider anchoring the nuget package's version number to the version of the library, or by release date.  Choose a method that is the most straightforward for your use case.  For example, if a third party component is released yearly, and the year is the most signifigant versioning indicator, consider using the year as the major version number. I.e. `2014.0.0`.  This allows you to access the specific version of the component via your nuget package feed.