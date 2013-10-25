---
layout: default
---
#Running tests
##First time configuration
Tests are configured in the canvashs.cabal file. To run the javascript tests from the cabal file [phantomjs](http://phantomjs.org/) is required and put in the PATH [(how to put it in your PATH)](http://stackoverflow.com/a/6448469/359582). Also make sure that the cabal bin files are in your PATH as well (should be somewhere like %userprofile%\AppData\Roaming\cabal\bin, ~/.cabal/bin). Before tests can be run they have to be configured. Run 

    cabal update
    cabal install --enable-tests

##Testing
Tests can be run using:

    cabal test

#Configuring tests

##Module
For the module component configuring tests is similar. Tests are configured using [Hspec](http://hspec.github.io/). Tests should be placed in the **canvashs-module/tests** folder. For each module a seperate Spec file should be created, each spec file should end with Spec.hs. For example: tests for CanvasHs/Module/SubModule.hs should have a spec file at tests/CanvasHs/Module/SubModuleSpec.hs. Spec files will automatically be discovered.

How to write tests with Hspec can be found in the [Getting started with Hspec tutorial](http://hspec.github.io/getting-started.html).  


##Client side
For the client side implementation tests are configured using [Jasmine](http://pivotal.github.io/jasmine/). Tests should be placed in the **canvashs-client/tests/spec** folder. Related tests should be placed in separate Spec files. Spec files should be placed in the **canvashs-client/tests/index.html**, in this way:

	<!-- include spec files here... -->
	<script type="text/javascript" src="spec/specfile.js"></script>

On the github pages of Jasmine there is a basic guide on how to write tests: [Jasmine website](http://pivotal.github.io/jasmine/). Basic example:

    describe("Test suite name", function() {
      it("contains spec with an expectation", function() {
        expect(true).toBe(true);
      });
    });

The **JS-ImageDiff** script is also included by default, example usage can be found [here](http://humblesoftware.github.io/js-imagediff/test.html).