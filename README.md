# MTSA - Tei Lab Edition

鄭研究室による、MTSAのカスタムフォークです。
本家（GitLab）の更新を取り込みつつ、独自の拡張を行っています。

## セットアップ

macOS環境では `Homebrew` を使用して必要なツールをインストールすることを推奨します。

### 1. Homebrewのインストール

まだインストールしていない場合は、[公式サイト](https://brew.sh/)の手順に従って導入してください。

### 2. JDKとMavenのインストール

MTSAのビルドにはJavaとMavenが必要です。
以下のコマンドを実行してください。

```sh
# JDK 11 のインストール
brew install openjdk@11

# JDK 11 のパスを設定
echo 'export PATH="'"$(brew --prefix)"'/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc
echo 'export JAVA_HOME="'"$(brew --prefix)"'/opt/openjdk@11"' >> ~/.zshrc
source ~/.zshrc

# Maven のインストール
brew install maven
```

### 3. インストールの確認

正しくインストールされたか確認します。
それぞれ以下のコマンドを実行し、バージョン情報が表示されれば成功です。

```sh
java -version
mvn -version
```

### 4. リポジトリのクローン

リポジトリをローカルにクローンします。

```sh
git clone https://github.com/tei-lab-univ/MTSA.git
cd MTSA
```

### 5. 依存ライブラリの取得

GitHubの容量制限により、一部の巨大なライブラリファイルはリポジトリに含まれていません。
ビルド前に、以下のコマンドを実行して本家リポジトリから不足しているライブラリを取得してください。

```sh
# maven-root/mtsa/lib の .jar ファイルを取得
curl -L "https://git.exactas.uba.ar/lafhis/mtsa/-/archive/master/mtsa-master.tar.gz?path=maven-root/mtsa/lib" | tar -xz --strip-components=1
```

## ビルドと実行

### 6. プロジェクトのビルド

配置したライブラリを含めてプロジェクトをビルドします。

```sh
cd maven-root/mtsa
mvn clean install -DskipTests
```

### 7. MTSAの実行

ビルド成功後、以下のコマンドで MTSA を起動します。

```sh
mvn exec:java
```
