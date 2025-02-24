# TypeScriptでの非同期処理

## Chapter 10: TypeScriptでの非同期処理

この章では、TypeScriptにおける非同期処理の仕組みとその実践的な使用方法について探求します。非同期処理は、I/O操作やネットワーク通信などの時間がかかる操作を効率的に扱うための重要なテクニックであり、TypeScriptはJavaScriptの基礎の上に構築されているため、その非同期処理のモデルも引き継いでいます。

### 10.1 非同期処理の基本概念

非同期処理とは、ある処理が完了するのを待たずに次の処理を開始できるようにすることです。これにより、プログラムがブロックされることなく動作し続けることができます。JavaScript（およびTypeScript）では、非同期処理は主に以下の方法で行われます：

- **コールバック**
- **Promise**
- **async/await**

### 10.2 コールバック

コールバックは、非同期処理を行うための基本的な方法ですが、コールバック地獄（callback hell）と呼ばれる、可読性やメンテナンス性を損なう問題が発生することがあります。

#### TypeScriptの例

```typescript
function fetchData(callback: (data: string) => void) {
    setTimeout(() => {
        const data = "Hello, World!";
        callback(data);
    }, 1000);
}

fetchData((result) => {
    console.log(result); // 1秒後に "Hello, World!" と表示
});
```

この例では、`fetchData`関数が1秒後にデータを取得し、その結果をコールバック関数に渡します。

### 10.3 Promise

Promiseは、非同期処理の結果を表すオブジェクトであり、処理が成功した場合には`resolve`が、失敗した場合には`reject`が呼び出されます。これにより、コールバック地獄を回避することができます。

#### TypeScriptの例

```typescript
function fetchData(): Promise<string> {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = "Hello, World!";
            resolve(data);
        }, 1000);
    });
}

fetchData()
    .then((result) => {
        console.log(result); // 1秒後に "Hello, World!" と表示
    })
    .catch((error) => {
        console.error("Error:", error);
    });
```

この例では、`fetchData`関数がPromiseを返し、`then`メソッドを使って結果を処理します。

### 10.4 async/await

`async`/`await`は、Promiseを使用した非同期処理をよりシンプルに記述するための構文糖衣です。`async`関数は常にPromiseを返し、`await`を使用することでPromiseが解決されるまで処理を一時的に待つことができます。

#### TypeScriptの例

```typescript
async function fetchData(): Promise<string> {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve("Hello, World!");
        }, 1000);
    });
}

async function main() {
    const result = await fetchData();
    console.log(result); // 1秒後に "Hello, World!" と表示
}

main();
```

この例では、`fetchData`関数を`await`で呼び出し、Promiseの解決を待ってから結果を処理しています。

### 10.5 エラーハンドリング

非同期処理のエラーハンドリングは非常に重要です。Promiseでは、`catch`メソッドを使用してエラーを捕捉でき、`async/await`では`try/catch`構文を使用することが一般的です。

#### TypeScriptの例（Promiseでのエラーハンドリング）

```typescript
fetchData()
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.error("Error:", error);
    });
```

#### TypeScriptの例（async/awaitでのエラーハンドリング）

```typescript
async function main() {
    try {
        const result = await fetchData();
        console.log(result);
    } catch (error) {
        console.error("Error:", error);
    }
}

main();
```

### 10.6 非同期ループ

非同期処理を用いるループでは、通常の`for`ループではなく、`for...of`ループと`await`を組み合わせることで、順次処理を行うことができます。

#### TypeScriptの例

```typescript
async function fetchMultipleData() {
    const urls = ["url1", "url2", "url3"];
    for (const url of urls) {
        const data = await fetchData(url);
        console.log(data);
    }
}
```

この例では、複数のURLからデータを取得し、1つずつ待機してから結果を表示しています。

### 10.7 Pythonにおける非同期処理

Pythonでも非同期処理が可能で、`asyncio`ライブラリを利用して非同期プログラミングを行うことができます。

#### Pythonの例（asyncio使用）

```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)
    return "Hello, World!"

async def main():
    result = await fetch_data()
    print(result)  # 1秒後に "Hello, World!" と表示

asyncio.run(main())
```

ここでは、Pythonの`async`/`await`構文を使って、非同期にデータを取得し、結果を出力しています。

### 10.8 まとめ

この章では、TypeScriptにおける非同期処理の基本概念、コールバック、Promise、async/awaitの使い方、エラーハンドリング、非同期ループについて学びました。これにより、非同期な操作を行う際のテクニックを理解し、効果的に活用するための手法を習得できるでしょう。次の章では、TypeScriptのモジュールと名前空間について掘り下げていきます。

