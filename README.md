# Shiken [試験] #

Shiken is a ruby gem that is a wrapper for selenium.  In my experience many people write "scripts" using selenium, not "tests".  The difference being you can start a set of tests and walk away... then come back and find out what passed or failed.  Scripts are something you have to watch to see what is going on.  Automation is key.

There are other similar frameworks... this is just my own way of digging into automation test and techniques (and ruby code for that matter).

Shiken is the Japanese word for test.

### Project Design Philosopy ###

* the test pyramid
* rely on unit tests
* but have sanity tests
* test on production
* use page oriented tests
* good tests require programming
* test clean up after themselves
* you can run test individually

## Travel Site Examples


### Who do I talk to? ###

* Pat Conley pconley312@gmail.com

### A simple rspec example ###
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
