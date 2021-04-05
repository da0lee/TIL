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

### class

- 설계도
- 속성과 행위로 구성 됨

<br/>

### instance

- 실체
- 해당 클래스의 구조로 컴퓨터 저장공간에서 할당

<br/>

### constructor

- 클래스가 new 표현식에 의해 instance화 되어 객체를 생성할 때 호출되어 멤버 변수를 초기화하고, 필요에 따라 자원을 할당하기도 한다.
- 생성자는 클래스의 멤버가 아니며, 멤버가 아니므로 상속되지 않는다. 따라서, 오버라이딩의 대상이 될 수도 없다. 또한, 일반적인 메소드 호출 방법으로 호출할 수 없다.

<br/>

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

<br/>
<hr/>
<br/>

`오늘 공부한 것`

https://academy.dream-coding.com/courses/take/typescript/lessons
