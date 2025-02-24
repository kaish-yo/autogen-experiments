# ジェネリクスと高度な型

## Chapter 6: ジェネリクスと高度な型

この章では、TypeScriptのジェネリクスと高度な型システムについて学びます。ジェネリクスは、より再利用可能で柔軟な関数やクラスを作成するための強力な機能です。また、高度な型機能を使用することで、型チェックを強化し、より複雑な構造を管理できます。

### 6.1 ジェネリクスの基本

ジェネリクスは、型をパラメータとして受け取ることができる関数やクラスの作成を可能にします。これにより、特定の型に依存しない汎用的なコードを書くことができます。

#### TypeScriptの例

```typescript
function identity<T>(arg: T): T {
    return arg;
}

const result1 = identity<string>("Hello, World!");
const result2 = identity<number>(123);
```

この例では、`identity`関数はジェネリック型`T`を使用しており、引数の型に応じて動作します。これにより、異なる型に対して同じ関数を使うことができます。

### 6.2 ジェネリクスを使用したクラス

ジェネリクスは、クラスでも活用することができます。クラスに型パラメータを付加することで、柔軟性の高いクラス設計が可能になります。

#### TypeScriptの例

```typescript
class Box<T> {
    private value: T;

    constructor(value: T) {
        this.value = value;
    }

    getValue(): T {
        return this.value;
    }
}

const stringBox = new Box<string>("Hello");
const numberBox = new Box<number>(42);

console.log(stringBox.getValue()); // Hello
console.log(numberBox.getValue()); // 42
```

この例では、`Box`クラスがジェネリック型`T`を持ち、異なる型の値を持つボックスを作成できます。

### 6.3 ジェネリクスで制約を設ける

ジェネリクスでは、型に制約をかけて、特定の構造や特性を持つ型でのみ動作するようにすることができます。これにより、より具体的な型チェックが可能になります。

#### TypeScriptの例

```typescript
interface Lengthwise {
    length: number;
}

function logLength<T extends Lengthwise>(arg: T): void {
    console.log(arg.length);
}

logLength({ length: 10 }); // OK
logLength("Hello");        // OK
// logLength(123);        // エラー: 型 'number' はリテラル型に割り当てられません
```

ここでは、`Lengthwise`インターフェースを定義し、`logLength`関数がそのインターフェースを実装する型に対してのみ動作するようにしています。

### 6.4 高度な型機能

TypeScriptには、ユニオン型、交差型、条件付き型などの高度な型機能があり、これらを使用することでより柔軟な型設計が可能になります。

#### 6.4.1 ユニオン型

ユニオン型は、複数の型のいずれかを受け取ることができる型です。

##### TypeScriptの例

```typescript
function printId(id: number | string): void {
    console.log(`Your ID is: ${id}`);
}

printId(101);          // OK
printId("202");        // OK
// printId(true);     // エラー: 型 'boolean' は 'string | number' に割り当てられません
```

#### 6.4.2 交差型

交差型は、複数の型を組み合わせた型であり、全ての型のプロパティを持つことができます。

##### TypeScriptの例

```typescript
interface Person {
    name: string;
}

interface Employee {
    employeeId: number;
}

type EmployeePerson = Person & Employee;

const employee: EmployeePerson = {
    name: "Alice",
    employeeId: 1
};
```

ここでは、`Person`と`Employee`のプロパティを組み合わせた新しい型`EmployeePerson`を作成しています。

#### 6.4.3 条件付き型

条件付き型は、型のランタイム状態に基づいて異なる型を選択する機能です。

##### TypeScriptの例

```typescript
type IsString<T> = T extends string ? "It's a string!" : "It's not a string.";

type Test1 = IsString<string>; // "It's a string!"
type Test2 = IsString<number>; // "It's not a string."
```

この例では、`IsString`型を使用して、与えられた型が文字列かどうかを判定しています。

### 6.5 ユーザー定義型ガード

ユーザー定義型ガードを使用することで、型チェックをカスタマイズし、より安全な型判定が可能になります。

#### TypeScriptの例

```typescript
function isString(value: any): value is string {
    return typeof value === 'string';
}

function example(value: string | number) {
    if (isString(value)) {
        console.log(value.toUpperCase()); // valueはここでstring型
    } else {
        console.log(value.toFixed(2)); // valueはここでnumber型
    }
}
```

ここでは、`isString`関数がユーザー定義型ガードとなり、`example`関数内で`value`の型を判別しています。

### 6.6 Pythonにおけるジェネリクスと高度な型

Pythonでも、型ヒントとともにジェネリクスを使用することが可能です。Pythonの標準ライブラリにおける`TypeVar`を使用して、ジェネリックな関数やクラスを作成できます。

#### Pythonの例

```python
from typing import TypeVar, Generic

T = TypeVar('T')

class Box(Generic[T]):
    def __init__(self, value: T):
        self.value = value

    def get_value(self) -> T:
        return self.value

string_box = Box("Hello")
number_box = Box(123)
```

### 6.7 まとめ

この章では、TypeScriptにおけるジェネリクスと高度な型システムについて学びました。ジェネリクスを使用することで、型に依存しない汎用的なコードが書け、条件付き型や交差型を利用することでより強力なデータ構造を作り出すことができます。TypeScriptの型システムをうまく活用することで、より安全で保守性の高いコードを書くことができるでしょう。次の章では、条件付き型に関する具体的な使用方法について探求していきます。

