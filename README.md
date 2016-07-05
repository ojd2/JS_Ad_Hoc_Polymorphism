# Ad-hoc Polymorphism

Ad-hoc polymorphism is formally known as a method and language construct 
that allows a method to work with arguments of varying types.
Encapsulation also resembles ad-hoc polymorphism in functional implementations. 
Other implementations include both Single and Double dispatch, most commonly 
implemented using imperative languages. 

###Overview

Many languages like JavaScript implement polymorphism to various degrees,
some more suitable and stable than others. Reasons for conveying polymorphism
in programming languages are purely type orientated. Many types have the same 
structural type, but multiple semantic types can also hold a set of different
behaviors. If we understand the set different behaviors, we can call methods to
perform multiple behaviors and at the same time reserve the objects state. 
Languages with no ad-hoc polymorphism constructs will ultimately have to force 
objects to share and extend a lot of unnecessary information.

### Single Dispatch

Over time, Single Dispatch has evolved into Double Dispatch for its flexible
mapping and invocation properties. 

To begin with, Single Dispatching can be implemented by invoking a polymorphic
method that also invokes another object’s polymorphic methods. 
The example below demonstrates that each object invoked by the `BankPrototype`
object, knows what to do when:

`MoneyAddedTo -> Savings() || MoneyAddedTo -> Mortgage()`

```
var BankPrototype = {
	MoneyAddedTo: function (otherObject) {
		this.Savings();
		otherObject.Savings();
		this.Mortgage();
		otherObject.Mortgage();
	},
	Savings: function () {
		return moneyForSavings
	},
	Mortgage: function () {
		return moneyForMortgage
	}
}
```

### Double Dispatch

However, the example above has some limitations that could be addressed. 
What if there needs to be a unique calculation called upon mortgage fees
for the coming month of July? What if the interest rate for a more universal
payment needs to be added or subtracted? Furthermore, the banks savings 
accountants were doubling the interest rates or changing the interest paid 
from yearly to monthly? For any one of these scenarios, special cases were
integrated into programming languages to handle these exceptions. We can 
implement Double dispatching using methods as our arguments. In JavaScript, 
we can extend our `BankPrototype` into more smaller components that are 
modular and can be connected by chaining together prototypes: 

```
var SavingsPrototype = {
	moneyToBeSaved: function (objectOfMoneyToBeSaved) {
		return objectOfMoneyToBeSaved.interestRateIncrease(this)
	},
	interestRateCalculation: function (money) {
		 Handle when money needs interest rate to be increased calculation.
	},
	addInterestRate: function (money) {
		 Handle when the interest rate needs to be added to fees in July.
	}
}
```
var MortgagePrototype = {
	moneyForMortgage: function (objectOfMoneyForMortgagePayment) {
		return objectOfMoneyForMortgagePayment.JulyCalculation(this)
	},
	addMortgageInterestRate: function (payment) {
		 handle meteor-fighter collisions
	},
	subtractMortgageInterestRate: function (payment) {
		 handle meteor-meteor collisions
	}
}
```

Some money object can invoke the savings method that performs a 
method on the mortgage returned value. Essentially, we have a 
set of polymorphic methods working in routine. Methods can be 
easily coupled, tupled and doubled together.

```
var someMoney = Object.create(SavingsPrototype),
someMortgage  = Object.create(MortgagePrototype);
```

Method calling is done here.

`someMoney.moneyToBeSaved(someMortgage);`