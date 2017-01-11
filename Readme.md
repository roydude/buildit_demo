## Running the project

### Pre-requisites
Before you begin you need to have docker installed. I'm assuming this is running on Linux (tested on Ubuntu 16.04) - 
Docker containers provide a way of using 3rd party software without installing it on every tester's machine.
It is my preference to use it if possible, but in the case that it's not available you would need to install
Maven, Chrome webdriver and phantomjs locally (and adapt the scripts in ./bin accordingly).

### Running tests
<pre>./bin/run-tests </pre>
(Hint: pass the '-h' parameter to see all options that this script provides.)

## Reporting
The report will be created as ./reports/index.html<br><br>
I have included the reports generated by my test run in case there are any issues running it (at least you can see what the report looks like).

## Logs
The log4j logs are also in the ./reports folder.

## If I had more time ...
* I would put everything in the *utilities* folder into a separate Maven repo so it could be accessed
 by other projects (with the possible exception of the DailyWeather class).
 
* I would also cut down the 'noise' at the start of the tests from the webdriver (ProtocolHandShake etc...).

* I would add other webdrivers (i.e. Chrome via a container + VNC viewer container so you can watch
teh tests run on the screen - this can be helpful when debugging automation, or for demos).

## Project structure and details

The basic structure is as follows (with the interesting parts in __bold__):

<pre>
.
├── <b><i>pom.xml</i></b>
├── <b>features</b>
├── bin
│   ├── <b>run-tests</b>
│   └── ... (various supporting scripts) ...
└── src
    └── test
        ├── java
        │   └── uk
        │       └── co
        │           └── buildit
        │               └── app
        │                   ├── <b><i>RunCukesTest.java</i></b>
        │                   ├── <b>steps</b>
        │                   └── support
        │                       ├── <b>elements</b>
        │                       ├── <b>hooks</b>
        │                       ├── <b>pages</b>
        │                       └── <b>utilities</b>
        └── resources
            └── <b><i>extent-config.xml</i></b>
</pre>
<br>

### Project setup files...

* #### _pom.xml_
Contains automation project build details such as dependencies etc... 

* #### _RunCukesTest.java_
This controls the running of the tests via cucumber / maven.

* #### _extent-config.xml_
Contains configuration for the report (uses the report mechanism from here http://extentreports.relevantcodes.com/). You should put the name of your project in the title and report headings in here.
<br><br>

### Test code files...

* #### features
Contains feature files.<br/><br/>

* #### steps
Contains the definition of steps used in the feature files.

* #### pages
Contains the logic code used by the steps (based on application pages, or screens). If there is logic that isn't specific
to a screen then it should be in the Application.java class here (i.e. functionality that could be used in multiple places
in the application).

* #### elements
Contains definitions for each element that you need access to. I always make sure selector methods are named informatively (i.e. the name ends with Element or Elements, depending on whether it returns one element or a list of elements).
Again, If there are elements that aren't specific to a screen, then they should be in the Application.java class here.

* #### hooks
Contains the code to be executed via cucumber 'hooks' (Before / After etc...). Generally you should leave these as they
are here, or at least only add to them (don't remove the code that's in them).

* #### utilities
Contains functionality that could possibly be used for other projects (usually I'd have these in a separate repo and call
them from there).