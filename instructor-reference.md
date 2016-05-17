## [I do: Javascripting your tests (10/65)](https://github.com/ga-wdi-lessons/js-jasmine/tree/wdi9-updates#i-do-javascripting-your-tests-1065)

For the snowman builder, the result would be this:

```js
describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){

  });

  //In order for it to really be a snowman, it needs to have a carrot nose.
  it("should have a carrot nose", function () {

  });

  //It also needs stick arms.
  it("should have stick arms", function () {

  });

  //If the snowman is named Olaf, he should like warm hugs.
  describe( "a snowman named Olaf", function(){

    it( "should like warm hugs", function(){

    });

  });

});
```

## [Let's add the first expectation:](https://github.com/ga-wdi-lessons/js-jasmine/tree/wdi9-updates#lets-add-the-first-expectation)

```js
describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  })

  // ... more stuff
});
```

add require:

```js
var Snowman = require("../snowman");

describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  });

  // ... more stuff
});
```

## [The final Snowman specs:](https://github.com/ga-wdi-lessons/js-jasmine/tree/wdi9-updates#the-final-snowman-specs)

```js
var Snowman = require("../snowman");

describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  });

  //In order for it to really be a snowman, it needs to have a carrot nose.
  it("should have a carrot nose", function () {
    var olaf = new Snowman("Olaf");
    expect ( olaf.features ).toContain("carrot nose");
  });

  //It also needs stick arms.
  it("should have stick arms", function () {
    var olaf = new Snowman("Olaf");
    expect ( olaf.features ).toContain("stick arms");
  });

  //If the snowman is named Olaf, he should like warm hugs.
  describe("A snowman named Olaf", function(){
    it( "should like warm hugs", function(){
      var frosty = new Snowman("Frosty");
      var olaf = new Snowman("Olaf");
      expect( olaf.hug() ).toBe( "I like warm hugs!" );
      expect( frosty.hug() ).not.toBe( "I like warm hugs!" );
    });
  });

});
```

## [Refactor (10/150)](https://github.com/ga-wdi-lessons/js-jasmine/tree/wdi9-updates#refactor-10150)

``` js
describe( "A snowman", function(){
  var olaf;

  beforeEach(function(){
    olaf = new Snowman("Olaf");
  });

  it( "should have a name", function(){
    expect( olaf.name ).toBeDefined();
  });

  it("should have a carrot nose and stick arms", function () {
    expect ( olaf.features ).toContain("carrot nose", "stick arms");
  });

  describe("A snowman named Olaf", function(){
    var frosty;
    it( "should like warm hugs", function(){
      frosty = new Snowman("Frosty");
      expect( olaf.hug() ).toBe( "I like warm hugs!" );
      expect( frosty.hug() ).not.toBe( "I like warm hugs!" );
    });
  });

});
```
