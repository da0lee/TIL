# 절차지향

```js
{
  type CoffeeCup = {
    shots: number,
    hasMilk: boolean,
  };

  const BEANS_GRAMM_PER_SHOT: number = 7;
  let coffeeBeans: number = 0;
  function makeCoffee(shots: number): CoffeeCup {
    if (coffeeBeans < shots * BEANS_GRAMM_PER_SHOT) {
      throw new Error('Not enought coffee beans');
    }

    coffeeBeans -= shots * BEANS_GRAMM_PER_SHOT;
    return {
      shots,
      hasMilk: false,
    };
  }

  coffeeBeans += 3 * BEANS_GRAMM_PER_SHOT;
  const coffee = makeCoffee(2);
  console.log(coffee);
}
```

<br/>

# 객체지향

```js
{
  type CoffeeCup = {
    shots: number;
    hasMilk: boolean;
  };

  class CoffeeMaker {
    private static BEAN_GRAMM_PER_SHOT: number = 7;
    private coffeeBeans: number = 0;

    private constructor(coffeeBeans: number) {
      this.coffeeBeans = coffeeBeans;
    }

    static makeMachine(coffeeBeans: number): CoffeeMaker {
      return new CoffeeMaker(coffeeBeans);
    }

    fillCoffeeBeans(beans: number) {
      if (beans < 0) {
        throw new Error('value for beans should be greater than 0');
      }
      this.coffeeBeans += beans;
    }

    private grindBeans(shots: number) {
      if (this.coffeeBeans < shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT) {
        throw new Error('Not enought coffee beans.');
      }

      console.log(`grinding beans for ${shots}`);
      this.coffeeBeans -= shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT;
    }
    private preheat() : void {
      console.log('heating up ♨');
    }
    private extract(shots: number): CoffeeCup {
      console.log(`Pulling ${shots} shots ☕`);
      return {
        shots,
        hasMilk: true,
      };
    }
    makeCoffee(shots: number): CoffeeCup {
      this.grindBeans(shots);
      this.preheat();
      return this.extract(shots);
    }
  }

  const maker = CoffeeMaker.makeMachine(32);
  maker.fillCoffeeBeans(50);
  maker.

  class User {
    get fullName(): string {
      return `${this.firstName} ${this.lastName}`;
    }
    private internalAge = 4;
    get age(): number {
      return this.internalAge;
    }
    set age(num: number) {
      if (num < 0) {
        throw new Error('value for age should be greater than 0');
      }
      this.internalAge = num;
    }
    constructor(private firstName: string, private lastName: string) {}
  }

  const user = new User('steve', 'jobs');
  console.log(user.fullName);
  user.age = 6;
}

```
