# jasmine-fake-window

jasmine-fake-window is an extension for [Jasmine](http://pivotal.github.com/jasmine/) JavaScript Testing Framework:

- minimally obtrusive utility for handling window mocking in jasmine
- currently only handles window.location

## Installation

download _jasmine-fake-window.js_ from [here](https://raw.github.com/ryanv/jasmine-fake-window/master/dist/jasmine-fake-window.js) and include it in your Jasmine's test runner file (or add it to _jasmine.yml_ file if you're using Ruby with [jasmine-gem](http://github.com/pivotal/jasmine-gem));

## Usage

```javascript
// source file
MyObjectNamespace = {
  window: window,
  goToUrl: function(url) {
    MyObjectNamespace.window.location.href = url
  }
}
// MyObjectNamespace spec
describe("MyObjectNamespace.window.location.href", function() {
  beforeEach(function() {
    MyObjectNamespace.window = jasmine.fakeWindow
  });

  it('does not change the page location', function() {
    MyObject.window.location.href = 'http://www.fake.com';
    // this spec would never run otherwise, because it would navigate
    // to another page.
    expect(MyObject.window.location.href).toEqual('http://www.fake.com');
    MyObject.goToUrl('http://www.google.com');
    // this spec wouldn't ever run either
    expect(MyObject.window.location.href).toEqual('http://www.google.com');
  });
});
```
## Running Specs

run `grunt` from the command line to lint and run specs

## Building distrubution

run `grunt preprocess`

## TODO
- add navigator functionality
- DRY up code
- add init function to automatically set before and after blocks to reset the location or tie fake window in jasmine.Env
