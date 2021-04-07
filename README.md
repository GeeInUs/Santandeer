
# Cucumber project, featuring Java and JUnit

This is the simplest possible build script setup for Cucumber using Java.
There is nothing fancy like a webapp or browser testing. All this does is to show you how
to install and run Cucumber!

## Prequisite
 1. Java is installed and in path
 2. Maven is intalled
 3. Junit 4.0  and Cucumber is used for assertion and running testss
 
 ### Notes
 Cucumber  is used to define features to test using Cucumber's JUnit runner. T
 he `@RunWith(Cucumber.class)` annotation on the `RunCukesTest`
class tells JUnit to kick off Cucumber.

## MVN Usage
    1. Unizp project in local directory
    2. Go to the location where project unzipped
    2. Open command promt and type mvn test
    
 ## JUNIT Usage (4.0)
 Alternatively JUNIT can be used to run test
   1. Use the exported settings to run tests  Projects/src/test/resources/Santandeer/RunCukesTest.launch



# Test Assumptions
## Sequencing Tests
1. Pricing information is published sequentially. ( No conflation etc)
2. There is no missing pricing information ( no missing CCY1/CCY2)
3. Empty or null data is not validated ( Just Ignored)
4. Sequencing of data is in ASC order ( eg 1, 2,3,4, 5 not 5,4,3, 2,1)
5. Data duplication will fail when validating rules 

## Date time Tests
1. Date and time  per currency pair is considered when checking which pricing information comes first
2. Conflation is permitted
3. Duplication is permitted

## Results
1. Standard .html results generated in Projects\target\cucumber-reports 

## Run Overriding options

The Cucumber runtime parses command line options to know what features to run, where the glue code lives, what plugins to use etc.
When you use the JUnit runner, these options are generated from the `@CucumberOptions` annotation on your test.

Sometimes it can be useful to override these options without changing or recompiling the JUnit class. This can be done with the
`cucumber.options` system property. The general form is:

    mvn -Dcucumber.options="..." test

Let's look at some things you can do with `cucumber.options`. Try this:

    -Dcucumber.options="--help"

That should list all the available options.

*IMPORTANT*

When you override options with `-Dcucumber.options`, you will completely override whatever options are hard-coded in
your `@CucumberOptions` or in the script calling `cucumber.api.cli.Main`. There is one exception to this rule, and that
is the `--plugin` option. This will not _override_, but _add_ a plugin. The reason for this is to make it easier
for 3rd party tools (such as [Cucumber Pro](https://cucumber.pro/)) to automatically configure additional plugins by appending arguments to a `cucumber.properties`
file.

### Run a subset of Features or Scenarios

Specify a particular scenario by *line* (and use the pretty plugin, which prints the scenario back)

    -Dcucumber.options="classpath:skeleton/belly.feature:4 --plugin pretty"

This works because Maven puts `./src/test/resources` on your `classpath`.
You can also specify files to run by filesystem path:

    -Dcucumber.options="src/test/resources/skeleton/belly.feature:4 --plugin pretty"

