# Decorators
> Testing recipes for decorators

## Table of contents

- [Boilerplate](#boilerplate)


## Boilerplate

Before start we need to initialize the related decorator and mock it's dependencies.

```js
describe('Decorator: $rootScope', function() {
  var $rootScope;

  beforeEach(module('myApp'));

  beforeEach(inject(function(_$rootScope_) {
    $rootScope = _$rootScope_;
  }));

  it('should log how many times the $apply method was called', function() {

    spyOn(console, 'log');

    $rootScope.$apply();
    $rootScope.$apply();
    $rootScope.$apply();

    expect(console.log).toHaveBeenCalledWith(1);
    expect(console.log).toHaveBeenCalledWith(2);
    expect(console.log).toHaveBeenCalledWith(3);
  });
});

```
