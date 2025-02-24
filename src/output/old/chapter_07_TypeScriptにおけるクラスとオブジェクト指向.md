# TypeScriptにおけるクラスとオブジェクト指向

## Chapter 7: TypeScriptにおけるクラスとオブジェクト指向

この章では、TypeScriptのクラスとオブジェクト指向プログラミング（OOP）の主要な概念について学びます。TypeScriptのクラスはJavaScriptのクラスを基にしており、強力な型システムを持つため、より安全で保守性の高いコードを書くことができます。

### 7.1 オブジェクト指向プログラミングの基本

オブジェクト指向プログラミング（OOP）は、データとその操作をオブジェクトとしてまとめるプログラミングスタイルです。OOPの主要な概念には以下があります：

- **クラス**: オブジェクトの設計図として、特定のデータとメソッドを定義します。
- **オブジェクト**: クラスから生成された具体例です。プロパティとメソッドを持つ状態を表します。
- **継承**: 既存のクラスを基に新しいクラスを作成する特性です。コードの再利用を促進し、階層的な関係を作ります。
- **ポリモーフィズム**: 同じ操作で異なる型のオブジェクトを扱う能力です。メソッドのオーバーライドやオーバーロードを通じて実現されます。

### 7.2 TypeScriptのクラス

TypeScriptのクラスは、JavaScriptのクラス文法を使用して定義され、型注釈を追加することで、型安全なコードを実現します。

#### TypeScriptの例

```typescript
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet(): string {
        return `Hello, my name is ${this.name}.`;
    }
}

const alice = new Person("Alice", 30);
console.log(alice.greet()); // Hello, my name is Alice.
```

この例では、`Person`クラスを定義し、`name`と`age`のプロパティ、および`greet`メソッドを持つオブジェクトを生成しています。

### 7.3 継承とオーバーライド

継承を用いることで、既存のクラスから新しいクラスを作成し、機能を継承したり拡張したりできます。

#### TypeScriptの例

```typescript
class Employee extends Person {
    employeeId: number;

    constructor(name: string, age: number, employeeId: number) {
        super(name, age); // 親クラスのコンストラクタを呼び出す
        this.employeeId = employeeId;
    }

    greet(): string {
        return `${super.greet()} My employee ID is ${this.employeeId}.`;
    }
}

const bob = new Employee("Bob", 40, 102);
console.log(bob.greet()); // Hello, my name is Bob. My employee ID is 102.
```

ここでは、`Employee`クラスが`Person`クラスを継承し、`greet`メソッドをオーバーライドしています。`super`キーワードを使うことで、親クラスのメソッドにアクセスすることができます。

### 7.4 アクセス修飾子

TypeScriptでは、クラスのプロパティやメソッドにアクセス修飾子を設定することができます。これにより、カプセル化を実現し、外部からのアクセスを制御します。

- **public**: デフォルトの修飾子。外部からアクセス可能。
- **private**: クラス内のみアクセス可能。
- **protected**: クラス内及びサブクラスからアクセス可能。

#### TypeScriptの例

```typescript
class BankAccount {
    private balance: number = 0;

    deposit(amount: number): void {
        this.balance += amount;
    }

    getBalance(): number {
        return this.balance;
    }
}

const account = new BankAccount();
account.deposit(100);
console.log(account.getBalance()); // 100
// console.log(account.balance);    // エラー: プロパティ 'balance' はプライベートです
```

### 7.5 抽象クラスとインターフェース

抽象クラスは、他のクラスによって拡張されることを目的としたクラスで、直接インスタンス化はできません。一方、インターフェースはオブジェクトの形状を定義し、複数のクラスで同じ構造を持たせるために使用されます。

#### TypeScriptの例

```typescript
abstract class Animal {
    abstract makeSound(): string;

    move(): void {
        console.log("Moving...");
    }
}

class Dog extends Animal {
    makeSound(): string {
        return "Woof!";
    }
}

const dog = new Dog();
console.log(dog.makeSound()); // Woof!
dog.move(); // Moving...
```

ここで、`Animal`は抽象クラスで`makeSound`メソッドを定義しています。`Dog`クラスはそれを継承し、`makeSound`メソッドを実装します。

#### インターフェースの例

```typescript
interface Vehicle {
    start(): void;
}

class Car implements Vehicle {
    start(): void {
        console.log("Car started.");
    }
}

const myCar = new Car();
myCar.start(); // Car started.
```

この例では、`Vehicle`インターフェースを定義し、`Car`クラスがそれを実装しています。

### 7.6 JavaScriptとの関係

TypeScriptはJavaScriptのスーパーセットであるため、JavaScriptのオブジェクト指向の機能はそのまま利用できます。TypeScriptでは型付けが強化されているため、より堅牢なアプリケーションを構築する際に役立ちます。

### 7.7 まとめ

この章では、TypeScriptにおけるクラスとオブジェクト指向の基本概念、継承、アクセス修飾子、抽象クラスおよびインターフェースについて学びました。これらのテクニックを通じて、より構造化された、安全なコードを構築することができます。次の章では、TypeScriptのモジュールと名前空間について掘り下げていきます。

