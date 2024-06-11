# 自分用メモ

## ?オペレータ

Rustの`?`オペレータはエラーハンドリングに使用されます。このオペレータは、`Result`型の値を返す関数やメソッドで使用できます。`?`オペレータは、`Result`型の値が`Ok`の場合はその中の値を取り出し、`Err`の場合は直ちにそのエラーを返します。

以下に具体的な例を示します。

```rust
fn read_file() -> Result<String, std::io::Error> {
    let mut file = File::open("file.txt")?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}
```

使わない場合には

```rust
fn read_file() -> Result<String, std::io::Error> {
    let mut file = match File::open("file.txt") {
        Ok(file) => file,
        Err(e) => return Err(e),
    };
    let mut contents = String::new();
    match file.read_to_string(&mut contents) {
        Ok(_) => Ok(contents),
        Err(e) => Err(e),
    }
}
```

この例では、File::openとread_to_stringの両方がResult型を返します。これらの関数が成功すれば、その結果が次の行に渡されます。一方、いずれかの関数がエラーを返すと、そのエラーが直ちにread_file関数から返されます。これにより、エラーハンドリングが簡潔になり、コードの可読性が向上します。

## ロギング

環境変数RUST_LOGを設定する必要がある→別にマストじゃなくない？？

ハードコードしても良さそうだしサンプルコードはなかったらinfoが設定されるだけに見える。

外部で制御する枠組みがなさそうでそこは不便っぽい。