# QA Engineer Assessment Solution

## Introduction

Use this file to document your solution and findings.

Name: Joel Sitanala

## Remarks 

# GETTING STARTED

Preparation for Protractor (prep part 1)
After unpacking the ZIP file with the assessment I started installing Protractor on my local machine.
I first had to run an update for NPM because all my work is usually done on a remote machine.
While installing Protractor I read the README.md file and the other files that could help me understand this assesment.
After the installation I could run the first test succesfully. 
At first it did't start but selenium server wasn't running, it took me about 2 seconds to realise that.

Assesment (Prep part 2)
In the ASSESMENT.md file it stated that I could use Visual Studio Code as an IDE.
I'm used to work with Visual Studio Enterprise. But for this assignment I choose VSC because I do not have a VSE licence.
I installed a cucumber extention for intellisensing and protractor testrunner for VSC.
Apparently the VSC interface is not like the VSE version, but that should not be a problem. I tried to run the test, just to see what happens.

The test did not run. I installed protractor-cucumber-framework
Still no succes. I googled running  protractor with VSC as IDE.
It pointed me to configure the launch.json file. Before going into that I just wanted the application to run.

I returned to the commandline to try and run the application first.
So I installed the angular CLI and ran the command 'npm start'. It gave me the next error.

"An unhandled exception occurred: Cannot find module '@angular/compiler-cli/src/tooling'
Require stack: ..."

I ran the updates and fixes:
$ npm i -g npm-check-updates
$ ncu -u
$ npm audit fix --force

After running the the "start" command again I got an TypeScript error.
"The Angular Compiler requires TypeScript >=4.0.0 and <4.2.0"
So I installed the correct TypeScript version and the last thing was to comment  "import 'core-js/es7/reflect';" in the file polyfills.ts.
As I got this error "Error: ./src/polyfills.ts".

Then I finally got to see the GUI after the command: "npm start".

I still got the warning that "Warning: C:/qa-test-assessment-master/src/environments/environment.prod.ts is part of the TypeScript compilation but it's unused.
Add only entry points to the 'files' or 'include' properties in your tsconfig."

After adding files properties in ts.config.app.json I got the application running without
errors of warnings. 


# Running the test
When running the test it could not find the feature files. I fixed the path to the feature file in protractor.conf.js. Then I got the message "error: unknown option '--strict'" so I changed the value from "true" to "false". Just to see what happens. My priority was running the test, so it was trail and error and getting to know the framework better. 
The test still did not run because it gave me another error. By now I wasn't sure I was going the right direction, because of the following errors.

"DevTools listening on ws://127.0.0.1:56349/devtools/browser/09432f71-bccf-439c-90b5-fc1d4c631dbd
[18080:18260:0308/204950.335:ERROR:device_event_log_impl.cc(214)] [20:49:50.335] USB: usb_device_handle_win.cc:1056 Failed to read descriptor from node connection: Een apparaat dat op het systeem is aangesloten, werkt niet. (0x1F)"

The short answer to my question was that it should work. After some googling the error has something to do with a chromium bug (windows only?), but it was fine ignoring it.
That made me wonder if this was a chromium bug than it shouldn't appear in Firefox. So I started the test in Firefox and the 'USB' error message didn't show up.

I implemented a work around by using import-cwd so the support code always requires cucumber-js from the current working directory.
After that the result folder was missing. So I added the folder.
I switched back to Chrome and ran the test...

Then I finally got the TEST running after the command: "protractor protractor.conf.js"


# WRITING THE TESTS
I started to monkey test the application and write the feature files using the acceptance criteria in README.md. Now I could focus on the implementation. 
When running the test I could see the test start the browser and performing the test, but the debug messages showed me that it could not read the cucumber scenario's.
I went back to the config file and fixed the cucumberOpts in reading the step files.

In the search-person file I added one test and to not repeat the Given steps I added the Background keyword. To make shorter.

To be honest, at this point I still can't run the test from VSC. But if it had run It would make debugging so much easier.

To make the first test more robust I added clicking on the radiobutton person, even when the test starts with the radiobutten 'people' active. As the application is searching for people and planets I decided to make 2 seperate feature files for both.
I started to work on the search-person.feature. The already were some locators in the pageObject file. So the first 2 tests were just to see if the feature files, steps (gluecode) and pageObject files worked as aspected. Once I got a succesfull test I tried to use the reference/definition in Visual Studio Code. It was fairly easy to add an settings.json
with the right configuration.

For the next challenge I wanted to work with datatables. For the first acceptence criteria I could do just that. So I started to write the scenario's for searching planets and some alternative scenario's. To make a long story short. I was still learing the posibilities of this framework and the libraries.

Back to the test. 

After trying to work with Examples with multiple columns I went back to just one column.
I could retrieve the values in the datatable and display the values in the console.log.
The part to transfer those values and assert those with the actual values in the application, was a bit of a challenge. Once I got it working I decided to write some extra test to gain confidence. I had a lot of questions how to work with iterations, hooks, html reporting etc. While writing the test scenario's I tried to make the locators in the pageObject file as generic as possible. The last thing I did was working with tags.

I added the tag '@fail' for the test with another expected result. If you put a space in the input field then and click the search button, you get a list of results. These are not all the results. For planets searching with "IV" got me 2 results. But one of the results is not shown in the list if searching with a space. 

It has been 3 years that I'd worked with Protractor (Cucumber). Despite the time and effort I put in this assesment, It had good fun working with Protractor again.













