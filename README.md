# Shiken Examples #

Shiken is a ruby gem that is a wrapper for selenium that you vcan find at 
[Shinken]: https://github.com/pconley/Shiken "the source code for the gem"

## The examples ##

* Travel
* (More to come)

### Testing Philosopy ###

* the test pyramid
* rely on unit tests
* but have sanity tests
* test on production
* use page oriented tests
* good tests require programming
* test clean up after themselves
* you can run test individually

### Who do I talk to? ###

* Pat Conley pconley312@gmail.com

### A Quick Look ###
So, what would a test look like using shiken?  This is an example from the travel project that uses the session and page objects to extract the test(s) from the (resuable) login/out steps and specific page elements.  This example has 4 independent tests... each wrapped in the start and stop of a session.

```
require 'spec_helper.rb'

describe "Agile Travel - Select Flight Page" do
	
	before :each do
		TravelSession.start()
		$TravelFlightPage.goto
		expect($TravelFlightPage).to be_present
	end
  
  	after :each do
		TravelSession.stop
  	end
	
	it "has correct title" do
		expect($TravelFlightPage.title).to eq("Agile Travel")
	end
  
	it "has expected labels" do
		expect($TravelFlightPage).to have_content("Select Flight")
		expect($TravelFlightPage).to have_content("Trip type:")
		expect($TravelFlightPage).to have_content("Departing: ")
	end

	it "can fill two-way and get to passenger" do
		$TravelFlightPage.fill_flight_return_details
		expect($TravelPassengerPage).to be_present
  	end
  
  	it "can fill one-way and get to passenger" do
		$TravelFlightPage.fill_flight_oneway_details
		expect($TravelPassengerPage).to be_present
  	end
end

```
### API Entry Points ###

```
SK::init
SK::quit
SK::Trace
SK::Browser
SK::RadioSet
SK::Dropdown
```
*** rspec spec helper ***

Sometimes you want to use one browser session for an entire test suite execution, so you will put the init and quit into the spec_helper so it runs once before all the tests
```
RSpec.configure do |config|
     
  config.before :suite do
     SK::init()
  end

  config.after :suite do
    SK::quit()
  end
        
end
```
### SK::Trace ###
You can turn on/off the shiken internal tracing by by setting the trace level using either a symbol or a number.  Normally, it is a good idea to leave the default which set to :warn.  You can use numbers or symbols.
```
#!ruby

SK::Trace.level = :debug # = 3    # all tracing
SK::Trace.level = :warn  # = 2    # warnings and errors (default)
SK::Trace.level = :error # = 1    # just errors
SK::Trace.level = :quiet # = 0    # no putput
```
