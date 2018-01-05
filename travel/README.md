# Shiken - Travel #

This is an example that uses a fake website that exists for this kind of testing... it is located at 
[Agile Trave]: travel.agileway.net "fake wesite for testing"
The tests themselves are written in ruby/rspec.  

## Install 

CLONE 

gem install selenium-webdriver
gem install colorize
gem install shiken 

rspec spec

### Author ###

* Pat Conley (pconley312@gmail.com)

### API Entry Points ###
Full documentation is at 
[Shiken Documentation] : http://www.rubydoc.info/gems/shiken/0.0.4 "detail api documentation"
but here is a few things to grab your attention
```
#!ruby

SK::init
SK::quit
SK::Trace
SK::Browser
SK::RadioSet
SK::Dropdown
```
*** rspec spec helper ***

Usually you want to use one browser session for an entire test suite execution, so you will put the init and quit into the spec_helper

```
#!ruby

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

You can turn on/off the WT internal tracing by by setting the trace level using either a symbol or a number.  Normally, it is a good idea to leave the default set to :warn


```
#!ruby

SK::Trace.level = :debug # 3
SK::Trace.level = :warn  # 2 is the default
SK::Trace.level = :error # 1 
SK::Trace.level = :quiet # 0
SK::Trace.level = 3 # all tracing
SK::Trace.level = 2 # warnings and errors
SK::Trace.level = 1 # just errors
SK::Trace.level = 0 # no output
```