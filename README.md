# ctsurn-spec

Specification of the CTS URN notation, version `2.0.rc.1`.  The text of the specification is markdown format in the file `md/specification.md`.

## Using this build file ##

This build file includes a task named `release` that replaces references to the project's `version` property with the value of the current version, and places the resulting file in `build/pkg`.  It places a zip archive of this in `build/distributions`, which can be published to a maven repository with the task `uploadArchives`.  


### Creating a web interface with `bfdocs` ###

Prerequisites:  beautifuldocs, <http://beautifuldocs.com/>.

The following sequence is not yet pacakged as a build task, but can easily be done as follows:

	gradle release
	cp md/manifest.json build/pkg
	cd build/pkg
	bfdocs manifest.json


### Publishing a nexus artifact
To configure the appropriate settings for publishing a zip distribution to a maven server, make a copy of the settings file `publish.gradle`, and set the `pub` property to its name when you run the `uploadArchives` task, e.g.,

	cp publish.gradle publishlocal.gradle
	... [edit values in publishlocal.gradle]
	gradle -Ppub=publishlocal.gradle uploadArchives
