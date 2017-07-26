CLOSURES

Require the return of a function.

The closure's whole environment at the time of the return is remembered and attached
to the function that is returned.
  - The closure reaches the outer function's variables, but not

Two main things about closures:
  1. Scope tree
  2. Snapshot

Normally it is bad to let others access/change the outer function's private variables. If
you really want to allow it, use a get/set function pair (a function allowing to (re)set
the variable, and another allowing to get the changed variable).


Examples:

Quidditch team registration closures

  function registerTeam(teamName) {
  	var players = [];
  	return function(newPlayer) {
  		// var players = []; // if placed here, array resets each time
  		players.push(newPlayer);

  		console.log(teamName, players)
  	}
  }

  var hufflepuffAddPlayerFn = registerTeam('Hufflepuff');

  hufflepuffAddPlayerFn('Nobody');
  hufflepuffAddPlayerFn('No one else');
  hufflepuffAddPlayerFn('No one at all');

  var slythendorAddPlayerFn = registerTeam('Slythendor');
  slythendorAddPlayerFn('Lane');
  slythendorAddPlayerFn('Jackson');
  slythendorAddPlayerFn('Miguel');

Calculator closures

  function makeCalculator(startNum) {
  	var total = startNum;

  	function adder(numToAdd) {
  		total = total + numToAdd;
  		console.log(total);
  	}
  	function subtractor(numToSub) {
  		total = total - numToSub;
  		console.log(total);
  	}
  	function multiplier(numToMult) {
  		total = total * numToMult;
  		console.log(total);
  	}

  	return {
  		add: adder,
  		sub: subtractor,
  		mult: multiplier,
  		div: function divider(numToDiv) {
  			total = total / numToDiv;
  			console.log(total);
  		},
  		log: function() {
  			console.log(total);
  		}
  	}
  }

  var calcTen = makeCalculator(10);
  calcTen.add(100);
  // calcTen.mult(10);
  // calcTen.div(20);
  // calcTen.div(5);
  // calcTen.sub(10);

  var calcHundred = makeCalculator(100);
  calcHundred.add(300);
  calcHundred.div(25);



  function Animal(name, type, legs, sound) {
  	this.name = name;
  	this.type = type;
  	this.legs = legs;
  	this.sound = sound;
  }


Prototypes

  Animal.prototype.makeSound = function() {
  		console.log("The " + this.name + " is a " + this.type + " that says \"" + this.sound + ".\"");
  };

  var giraffe = new Animal('giraffe', 'necky thing', 4, 'Bleeeeeeeeck');
  var snake = new Animal('snake', 'slimy thing', 0, 'Sssssssssss');

  console.log(giraffe.makeSound());
  console.log(snake.makeSound());



  Array.prototype.copyArray = function() {
  	var arr = this;
  	newArr = [];
  	for (var i = 0; i < arr.length; i++) {
  		newArr.push(arr[i]);
  	}
  	console.log(newArr);
  }
  var myArr = [1, 2, 3]; // Same as writing: var myArr = new Array();
  myArr.copyArray();
