# TypeScriptでのCLIツール開発

## Chapter 12: TypeScriptでのCLIツール開発

この章では、TypeScriptを使用してコマンドラインインターフェース（CLI）ツールを開発する方法について探求します。CLIツールは、スクリプトやアプリケーションをコマンドラインから操作するための重要な手段であり、TypeScriptの型安全性や豊富な機能を活かすことで、高性能で信頼性のあるツールを構築できます。

### 12.1 CLIツールの基本

CLIツールは、コマンドラインからユーザー入力を受け取り、それに応じた処理を実行するプログラムです。CLIツールは、システム管理タスク、データ処理、テストスクリプトなど、さまざまな用途に利用されます。

### 12.2 TypeScriptプロジェクトのセットアップ

TypeScriptでCLIツールを開発するための基本的なプロジェクト構成を作成します。

```bash
mkdir my-cli-tool
cd my-cli-tool
npm init -y
npm install typescript @types/node --save-dev
npx tsc --init
```

この手順で、TypeScriptの環境がセットアップされ、`tsconfig.json`ファイルが生成されます。

### 12.3 コマンドライン引数の処理

CLIツールでは、ユーザーがコマンドラインから入力した引数を受け取ります。Node.jsの`process.argv`を使用することで、引数を取得することができます。

#### TypeScriptの例

```typescript
// cli.ts
const args = process.argv.slice(2); // コマンドライン引数を取得

if (args.length === 0) {
    console.log("Usage: node cli.js <name>");
    process.exit(1);
}

const name = args[0];
console.log(`Hello, ${name}!`);
```

このスクリプトは、コマンドライン引数を受け取り、それを基に挨拶を表示します。

### 12.4 入力のバリデーション

受け取った入力に対してバリデーションを行うことで、エラーを未然に防ぐことができます。例えば、引数が許可される数であることを確認したり、指定された形式のデータであるかをチェックすることができます。

#### TypeScriptの例

```typescript
const name = args[0];

if (!/^[\w\s]+$/.test(name)) {
    console.error("Error: Name can only contain letters and spaces.");
    process.exit(1);
}

console.log(`Hello, ${name}!`);
```

この例では、名前に対して正規表現を用いて妥当性チェックを行い、問題があればエラーメッセージを表示します。

### 12.5 コマンドラインオプションの解析

CLIツールでは、オプションとしてさまざまなフラグや設定を受け取ることが多いです。これを処理するために、`yargs`や`commander`といった便利なライブラリを利用することが一般的です。

#### yargsを利用した例

まず、`yargs`をインストールします。

```bash
npm install yargs
```

次に、次のようにコマンドライン引数を解析します。

```typescript
import yargs from 'yargs';

const argv = yargs
    .scriptName("my-cli-tool")
    .usage("$0 <cmd> [args]")
    .command("greet <name>", "Greet a person", (yargs) => {
        yargs.positional("name", {
            describe: "Name of the person to greet",
            type: "string"
        });
    })
    .help()
    .argv;

if (argv._[0] === "greet") {
    console.log(`Hello, ${argv.name}!`);
}
```

このように、コマンドとオプションを簡単に定義することができます。

### 12.6 コマンドの実行と出力の管理

CLIツールは、ユーザーからの入力を受けて処理を実行し、その結果を出力する役割を果たします。標準出力や標準エラー出力を使って、情報やエラーメッセージを表示します。

#### TypeScriptの例

```typescript
console.log("Processing...");
try {
    // 何らかの処理
} catch (error) {
    console.error("An error occurred:", error);
}
```

### 12.7 モジュールの分割

大規模なCLIツールでは、各機能を分割してモジュール化することで、コードの可読性と保守性を向上させることができます。

#### TypeScriptの例

```typescript
// greet.ts
export const greet = (name: string) => {
    console.log(`Hello, ${name}!`);
};

// cli.ts
import { greet } from './greet';

greet("Alice");
```

### 12.8 Pythonとの比較

PythonでもCLIツールの開発が可能であり、同様の機能を持ったライブラリが存在します。たとえば、`argparse`や`click`は一般的に使用されるパッケージです。

#### Pythonの例（argparseを使用）

```python
import argparse

parser = argparse.ArgumentParser(description='A simple CLI tool')
parser.add_argument('name', type=str, help='Name of the person to greet')

args = parser.parse_args()
print(f'Hello, {args.name}!')
```

この例では、Pythonの`argparse`を用いて、コマンドライン引数を受け取るコードを記述しています。

### 12.9 まとめ

この章では、TypeScriptを使用してCLIツールを開発する方法について幅広く学びました。非同期処理、モジュール化、入力のバリデーション、コマンドラインオプションの解析など、TypeScriptの特性を活かして堅牢なCLIツールを構築する手法を紹介しました。これらの技術を用いることで、実際の貢献が見込める技術知識を得ることができます。次の章では、TypeScriptのモジュールと名前空間についてさらに詳しく探求していきます。

