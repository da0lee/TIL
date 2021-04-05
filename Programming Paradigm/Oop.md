# encapsulation

```ts
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

    makeCoffee(shots: number): CoffeeCup {
      if (this.coffeeBeans < shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT) {
        throw new Error('Not enought coffee beans.');
      }

      this.coffeeBeans -= shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT;
      return {
        shots,
        hasMilk: true,
      };
    }
  }

  const maker = CoffeeMaker.makeMachine(32);
  maker.fillCoffeeBeans(50);

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

<br/>

# Abstraction

```ts
{
  type CoffeeCup = {
    shots: number;
    hasMilk: boolean;
  };

  interface ICoffeeMaker {
    makeCoffee(shots: number): CoffeeCup;
  }

  interface ICommercialCoffeeMaker {
    makeCoffee(shots: number): CoffeeCup;
    fillCoffeeBeans(beans: number): void;
    clean(): void;
  }

  class CoffeeMaker implements ICoffeeMaker, ICommercialCoffeeMaker {
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

    clean() {
      console.log('cleaing the machine');
    }

    private grindBeans(shots: number) {
      if (this.coffeeBeans < shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT) {
        throw new Error('Not enought coffee beans.');
      }

      console.log(`grinding beans for ${shots}`);
      this.coffeeBeans -= shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT;
    }
    private preheat(): void {
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

  class AmateurUser {
    constructor(private machine: ICoffeeMaker) {}
    makeCoffee() {
      const coffee = this.machine.makeCoffee(2);
      console.log(coffee);
    }
  }

  class ProBarista {
    constructor(private machine: ICommercialCoffeeMaker) {}
    makeCoffee() {
      const coffee = this.machine.makeCoffee(2);
      console.log(coffee);
      this.machine.fillCoffeeBeans(45);
      this.machine.clean();
    }
  }

  const maker: CoffeeMaker = CoffeeMaker.makeMachine(32);
  const amateur = new AmateurUser(maker);
  const pro = new ProBarista(maker);
  amateur.makeCoffee();
}

{
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

<br/>

# Inheritance

```ts
{
  type CoffeeCup = {
    shots: number;
    hasMilk: boolean;
  };

  interface ICoffeeMaker {
    makeCoffee(shots: number): CoffeeCup;
  }

  class CoffeeMaker implements ICoffeeMaker {
    private static BEAN_GRAMM_PER_SHOT: number = 7;
    private coffeeBeans: number = 0;

    constructor(coffeeBeans: number) {
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

    clean() {
      console.log('cleaing the machine');
    }

    private grindBeans(shots: number) {
      if (this.coffeeBeans < shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT) {
        throw new Error('Not enought coffee beans.');
      }

      console.log(`grinding beans for ${shots}`);
      this.coffeeBeans -= shots * CoffeeMaker.BEAN_GRAMM_PER_SHOT;
    }
    private preheat(): void {
      console.log('heating up ♨');
    }
    private extract(shots: number): CoffeeCup {
      console.log(`Pulling ${shots} shots ☕`);
      return {
        shots,
        hasMilk: false,
      };
    }
    makeCoffee(shots: number): CoffeeCup {
      this.grindBeans(shots);
      this.preheat();
      return this.extract(shots);
    }
  }

  class CaffeLatteMaker extends CoffeeMaker {
    constructor(beans: number, public readonly serialNumber: string) {
      super(beans);
    }
    private steamMilk(): void {
      console.log('steaming some milk');
    }
    makeCoffee(shots: number): CoffeeCup {
      const coffee = super.makeCoffee(shots);
      this.steamMilk();
      return {
        ...coffee,
        hasMilk: true,
      };
    }
  }

  const machine = new CoffeeMaker(23);
  const latteMachine = new CaffeLatteMaker(23, 'sss');
  const coffee = latteMachine.makeCoffee(1);
  console.log(coffee);
  console.log(latteMachine.serialNumber);
}
```

<br/>
<hr/>
<br/>

`오늘 공부한 것`

https://academy.dream-coding.com/courses/take/typescript/lessons
