## Grunt.MsBuild

These two Nuget packages add another step to the build of whatever project they're installed into.

In this additional build step, which triggers only if a gruntfile.js is found, **npm install** is executed (installing all the packages listed in package.json ) and if successful the command **grunt build$Configuration** is run where $Configuration is the currently set build configuration.

For example in a **release** build the command **grunt buildRelease** would be executed allowing you to customize the grunt build process based on the project configuration.

#### Differences between global and local

As you may have noted there are two packages version: Global and local. 

 - The global version assumes grunt-cli has been installed globally and will use it ( This is the most common situation on you development machine )
 - The local version assumes grunt-cli will be installed locally with the node packagesd specified in your package.json and will use to invoke grunt ( this is a more common setup on a build agent in TFS for esample where node is installed global but you can't easily add other global dependencies)

#### Common pitfalls

These are coomon problems found :

- If npm install says your pacakge.json cannot be parsed it is probably due to VS that saved your file in UTF8 format whit BOM. Save it as ASCII and the problem will disappear

- Usage of these package in a build osted on Visual Studio online is currently not possible due to the fact that the build agent has an old (0.6) version of node.js installed preventing the execution of the npm install command. This could be solved by checking in all the packages needed but I don't think it's a good solution.  