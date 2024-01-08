[[010 CS1331 MOC]]
1. Install the Checkstyle plugin for IntelliJ:
	1. Navigate to File -> Settings -> **Plugins**
	2. Make sure you're on the **Marketplace** tab, and search for "Checkstyle-IDEA." Install the plugin with the author **Jamie Shiell** as shown below: ![[CheckstyleImage1.png]]
	3. Download the `checkstyle.xml` provided on Canvas and move this to somewhere you can easily find, e.g. your project directory. 
	4. Open up the project directory with your homework code and configure checkstyle:
		1. Navigate to File -> Settings -> Tools -> **Checkstyle**
		2. **IMPORTANT** The current checkstyle version only works on *8.26*. Using the most recent version of checkstyle (by default) **will not work**. You can choose the version with the **Checkstyle version** dropdown in the **Checkstyle** category.
		3. Under the **Configuration File** heading, click the small white plus icon to add a new configuration file:  ![[CheckstyleToolsImage.png]]
		4. After clicking on the white plus, a new window should popup to add a new configuration. Under **Use a local Checkstyle file**, enter the exact path to your `checkstyle.xml` by either directly entering it or using the **Browse** button.
		5. Click the blue **Next** button. IntelliJ should tell you the "rules file has been validated and is ready to add." Click **Finish**, and your new configuration should now be in the **Configuration file** section.
		6. Enable the configuration by clicking on the **Active** selection box, and hit **Apply** to save your changes.

IntelliJ should now fully support your Checkstyle configuration, including suggestions (e.g. auto wrap an if statement in brackets).