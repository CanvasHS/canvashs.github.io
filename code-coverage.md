---
layout: default
---
#Inspecting code coverage
##First time configuration
First the required libraries for code coverage have to configured, before being able to execute code coverage on the javascript and haskell code. First make sure that you will be able to run all tests by following the [test instructions](test.html).

#Haskell module
Code coverage reports will be generated in ```dist\hpc\html\module-test```. To generate code coverage for the tests run:


    cabal install --enable-library-coverage --enable-tests

If this does not work, then clear the ```dist``` folder and try again.

#Javascript
Javascript code coverage is accessable from:
**canvashs-client/tests/test.html**

If code coverage does not work instructions will be visible on the test.html page.

##Browser support
Due to some limitations of running blanketjs locally some security settings have to be modified in chrome and firefox.

- Run chrome using the ```--disable-web-security``` flag
- Firefox go to ```about:config``` and set ```security.fileuri.strict_origin_policy``` to false. (Understand the security risks of turning this off, make sure you reset this value later!)

