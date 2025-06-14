# 学習記録

# June 15, 2025 StudyLog

**Paiza Dランクスキルチェックテスト×5問**
**Paiza PHP体験編完了**

**XAMPPの設定**
php.ini
- output_buffering = 4096 //バッファリング処理の有効化
- error_reporting = E_ALL //エラーの出力レベル
- default_charset = "UTF-8" //規定の文字コード
- date.timezone = Asia/Tokyo //規定のタイムゾーン
- display_errors = On //エラーの表示

**SQL**
- SELECT
- FROM
- WHERE

**backlog**
- サインアップ
- 学習プロジェクト作成
- ガントチャート作成

# June 14, 2025 StudyLog
//**break, continue, while, foreach**

**foreach文**
```php
    //配列の要素に-の値が含まれているかを知りたいときの例
    <?php
    $arr = [12, 34, 22, 65, 64, 67, 9, 12, 677];

    //配列の要素数を取得
    $num = count($arr);

    $message = '含まれていない';

    //for文
    for ($i = 0; $i < $num; $i++) {
        $value = $arr[$i];
        if ($value < 0) {
            $message = '含まれている';
            break; //この時点で処理を打ち切る
        }
    }
    echo $message;
    echo '<br>';
    echo '<br>';

    //配列の要素数を取得
    $num = count($arr);

    $sum = 0;

    for ($i = 0; $i < $num; $i++) {
        $value = $arr[$i];
        if ($value % 2 === 1) {
            continue; //この時点で処理をスキップする。何もせずに、次の処理へ進む。
            //配列の数が膨大な場合、プログラムのはじめの方にcontinueを書いていると、読み手がスキップする部分について考えなくてよくなったりするので、複雑なプログラムにおいてcontinueによる恩恵が生まれることがある
        }
        $sum += $value;
    }
    echo $sum;
    echo '<br>';
    echo '<br>';

    //while文 上記のfor文と同じ処理
    $i = 0;
    while ($i < $num) {
        $value = $arr[$i];
        if ($value < 0) {
            $message = '含まれている';
            break;
        }
        $i++;
    }
    echo $message;
    echo '<br>';
    echo '<br>';
    //使い分けとしては、より（見た目が）シンプルに書けるほうの構文を用いれば良い。更新のパターンが複雑なときはfor文よりもwhile文のほうが適している。

    //foreach文
    $arr = [1, 2, 3, 4, 5];

    foreach($arr as $value) {
        echo $value;
        echo '<br>';
    }
    echo '<br>';

    //上記のfor文で配列の要素に-の値が含まれているかどうか知りたいときの例をforeachで書き換えると以下のようになる
    $arr = [12, -34, 22, 65, 64, 67, 9, 12, 677];

    $message = '含まれていない';

    //foreach文
    foreach($arr as $value) {
        if ($value < 0) {
            $message = '含まれている';
            break;
        }
    }
    echo $message;
    echo '<br>';
    echo '<br>';
    //このようにすっきりとするので、配列から値を取り出すときは、for文よりもforeach文を用いる方が良い。

    //ValueだけでなくKeyも取り出したいときの例
    $fruits = [
        'りんご' => 3,
        'みかん' => 2,
        'ぶどう' => 6,
    ];

    foreach($fruits as $key => $value) {
        echo "{$key}は{$value}個あります。";
        echo '<br>';
    }
    echo '<br>';

    ?>


**for文**
```php
    <?php
    error_reporting(E_ALL);
    ini_set('display_errors', '1'); //下記でオレンジという配列に含まれないKeyで呼び出そうとした場合、エラー文を表示させるためのスクリプト


    for ($i = 0; $i < 10; $i++) {
        echo 'こんにちは' . "<br>";
    } //処理（初期化;条件;更新）
    //++は加算子もしくはインクリメント演算子
    //$i++;
    //$i=$i+1;
    //$i+=1; 複合代入演算子
    //これらは、厳密には異なる意味合いを持つが、基本的に1つずつプラスするという点で同じ意味になり、より簡潔で読みやすい構文表現を提供する機能のことをシンタックスシュガーという
    echo $i;
    echo '<br>';

    for ($i = 0; $i < 10; $i++) {
        $count = (string) $i;
        echo $count . '回目の繰り返しです';
        echo '<br>';
    }
    echo '<br>';

    for ($i = 0; $i < 10; $i++) {
        $count = (string) $i;
        echo "{$count}回目の繰り返しです"; //""の時に限り{}で変数をStringに埋め込める
        echo '<br>';
    }
    echo '<br>';

    for ($i = 0; $i < 10; $i++) {
        echo "{$i}回目の繰り返しです"; //この記述でも表示はできるが、暗黙の型変換が行われているため、理解せずに使用することは避けるべき
        echo '<br>';
    }
    echo '<br>';
    $g = [1, 2, 3];
    echo "{$g}です"; //このように記述するとarray型がString型に暗黙の型変換となり、エラー文も表示される
    echo '<br>';
    echo '<br>';

    ?>

    <table border="1">
        <?php
        for ($i = 1; $i < 10; $i++) {
            echo '<tr>';
            for ($j = 1; $j < 10; $j++) {
                $x = $i * $j;
                echo "<td>{$x}</td>";
            }
            echo '</tr>';
        }    //このように記述すると$iが縦の数字、$jが横の数字になり、九九の表になる
        echo '<br>';
        echo '<br>';
        ?>
    </table>

**配列**
```php
    <?php
    error_reporting(E_ALL);
    ini_set('display_errors', '1');
    //下記でオレンジという配列に含まれないKeyで呼び出そうとした場合、エラー文を表示させるためのスクリプト

    $a = [
        NULL => 1,
        TRUE => 2,
        2.7 => 3
    ];
    var_dump($a); //array(3) { [""]=> int(1) [1]=> int(2) [2]=> int(3) }
    //Keyに使用できる型は、基本的にIntとStringのみとする。それ以外を用いると、暗黙の型変換が起きる
    echo '<br>';
    echo '<br>';

    // $b = [
    //     ['key' => 'value'] => 1
    // ];
    // var_dump($b);
    //このように連想配列を連想配列のKeyにすると、型変換できずにエラーとなる

    $c = ['田中', '佐藤', '鈴木'];
    var_dump($c); //array(3) { [0]=> string(6) "田中" [1]=> string(6) "佐藤" [2]=> string(6) "鈴木" }
    //このようにKeyと=>を省略して記述することで、配列とすることもできる
    echo '<br>';
    echo '<br>';

    $d = ['田中', '佐藤', '鈴木', 'たかはし' => '高橋'];
    var_dump($d); //array(4) { [0]=> string(6) "田中" [1]=> string(6) "佐藤" [2]=> string(6) "鈴木" ["たかはし"]=> string(6) "高橋" }
    //このように一つだけKeyと=>を入れることも可能だが、このようにするとKeyにIntとStringが混ざることになるので、原則このような書き方はしない
    echo '<br>';
    echo '<br>';

    array_push($d, '吉田'); //関数：$dの最後に'吉田'を追加
    var_dump($d);
    echo '<br>';
    echo '<br>';

    array_push($d, '田口', '森田', '武田'); //複数要素追加
    var_dump($d);
    echo '<br>';
    echo '<br>';

    $d[] = '村田'; //要素を一つだけ追加する場合は、この表記でOK。処理もこちらのほうが早い
    var_dump($d);
    echo '<br>';
    echo '<br>';

    $e = ['関口', '加藤', '井口'];
    $merged = array_merge($d, $e); //2つの配列を結合した新しい配列$mergedを作成する※元の配列には影響しない
    //このような元の関数に影響を及ぼさない関数を非破壊的な関数という。対象的に破壊的な関数もある。関数を使用するときは、PHPの公式ドキュメントを参照し、どちらかを確認する。
    var_dump($merged);
    echo '<br>';
    echo '<br>';

    array_unshift($e, '佐々木'); //先頭に要素を追加する
    var_dump($e);
    echo '<br>';
    echo '<br>';

    array_unshift($e, '八木', '澤口'); //複数要素を追加する
    var_dump($e);
    echo '<br>';
    echo '<br>';

    $first = array_shift($e); //先頭の要素を削除し、取り出した値を返す
    var_dump($first);
    echo '<br>';
    echo '<br>';

    $last = array_pop($e); //末尾の要素を削除する
    var_dump($last);
    echo '<br>';
    echo '<br>';
    var_dump($e);
    echo '<br>';
    echo '<br>';


    $f = [
        0 => 'ゼロ',
        100 => 'ヒャク'
    ];
    //このように歯抜けでも表示はするが、原則しない。どうしても必要だとい場合はStringにして書く。
    // $f = [
    //  '0' => 'ゼロ',
    //  '100' => 'ヒャク'
    // ];
    var_dump($f);
    echo '<br>';
    echo '<br>';

    ?>

**配列**
```php
    <?php
    error_reporting(E_ALL);
    ini_set('display_errors', '1'); //下記でオレンジという配列に含まれないKeyで呼び出そうとした場合、エラー文を表示させるためのスクリプト

    $week = [
        "青色" => "月曜日",
        "赤色" => "火曜日",
        "水色" => "水曜日",
        "黄土色" => "木曜日",
        "黄色" => "金曜日",
        "灰色" => "土曜日",
        "白色" => "日曜日"
    ];
    var_dump($week); //array(7) { ["青色"]=> string(9) "月曜日" ["赤色"]=> string(9) "火曜日" ["水色"]=> string(9) "水曜日" ["黄土色"]=> string(9) "木曜日" ["黄色"]=> string(9) "金曜日" ["灰色"]=> string(9) "土曜日" ["白色"]=> string(9) "日曜日" } と、配列内の全ての要素を参照できる
    echo "<br>";
    echo "<br>";

    echo $week["水色"]; //水曜日、となりKeyでValueを取り出せる
    echo "<br>";
    echo "<br>";

    $week["水色"] = "Wednesday"; //書き換えることができる
    echo $week["水色"]; //Wednesday"]
    echo "<br>";
    echo "<br>";

    echo $week["オレンジ"]; //エラー文が表示される
    echo "<br>";
    echo "<br>";
    
    $week["オレンジ"] = "架空の曜日"; //新しくKeyを代入することができる
    echo $week["オレンジ"]; //架空の曜日
    echo "<br>";
    echo "<br>";
    
    ?>

# June 13, 2025 StudyLog

**PHP基礎**
データ型：文字列(String), 整数(Int), 少数(Float), 論理値(Bool)
演算：ある値から別の値を作り出すこと
- 単項演算
- 二項演算
```php
<?php
echo 3 + 5;
?>
```
- 結合演算
    ```php
    <?php
    	echo ‘今日は ’ . ‘金曜日’;
    ?>
    ```
- 三項演算
    ```php
    <?php
    	echo ‘今日は ’ . ‘金曜日’ . ‘です’;
    ?>
    ```
- 少数型の演算
    ```php
    <?php
    	echo 100-99.6; //結果：0.40000000000001 プログラムで少数型の演算を行うと誤差が生じる
    ?>
    ```
- Bool型(論理値型)
    - TRUE　FALSE
    - 論理和
        ```php
        $x = TRUE || FALSE; //TRUE
        //もしくは
        $x = TRUE or FALSE; //TRUE
        ```
    - 論理積
        ```php
        $y = TRUE && FALSE; //FALSE
        //もしくは
        $y = TRUE and FALSE; //FALSE
        ```
    - 否定演算
        ```php
        $z = ! FALSE
        ```
- NULL型（特殊型で、無を表す）

```php
$apple_is_red = TRUE;
$apple_is_blue = FALSE;
$i_dont_know_apple = NULL;
```

- キャスト演算（単項演算、型変換）

```php
var_dump();　//echoがHTMLに書き込むのに対し、var_dump()は型の情報を含むより詳細な情報を知ることができる。デバッグの際に用いる

    <?php
        var_dump(1); //int(1)
        echo '<br>';

        var_dump('1'); //string(1) "1"
        echo '<br>';

        $x = TRUE;
        var_dump($x); //bool(true)
        echo '<br>';

        $x = (string) 10; //キャスト演算。Int型の10をString型に変換
        var_dump($x); //string(2) "10"
        echo '<br>';

        $x = (int)'10'; //キャスト演算。String型の10をInt型に変換
        var_dump($x); //int(10)
        echo '<br>';

        $x = (int)'a'; //キャスト演算。String型のaをInt型に変換
        var_dump($x); //int(0)
        echo '<br>';

        $x = (bool)'a'; //キャスト演算。String型のaをbool型に変換
        var_dump($x); //bool(true)
        echo '<br>';

        $x = '10' + '10';
        echo $x; //String型の結合演算にかかわらず20と出力される。（暗黙の型変換）
    ?>
```

**暗黙の型変換**を行う言語→**弱い**型付けの言語

**暗黙の型変換**を行わない言語→**強い**型付けの言語

**→暗黙の型変換は**エラーの温床になるので、**基本的には避ける**ようにし、**キャストを行う際は手動**で行う。

→暗黙の型変換を行う言語においては、Bool型とString型の足し算や、Bool型とString型の論理積などが可能になる。結果は複雑に多様なものがあるので、覚えることは不要で都度調べれば良い。

→重要なことは**正しい型でプログラムを書く**こと。　

**比較演算**：2つの値からBool型の値を作り出す（Int型の値2つからBool型の値を作ったり、String型の値2つからBool型の値を作ったりする。※論理和、論理積は、Bool型の値2つからBool型の値を作る）

→比較が正しいとき：TRUE

→比較が誤っているとき：FALSE

**比較演算**：2つの値からBool型の値を作り出す（Int型の値2つからBool型の値を作ったり、String型の値2つからBool型の値を作ったりする。※論理和、論理積は、Bool型の値2つからBool型の値を作る）

→比較が正しいとき：TRUE

→比較が誤っているとき：FALSE

```php
    <?php
    if (TRUE || FALSE) {
        echo 'TRUEのときしか出ない';
        echo '<br>';
    }
    echo 'if文の外';
    echo '<br>';
    echo '<br>';

    var_dump(1 < 2); // true
    echo '<br>';
    var_dump(1 > 2); // false
    echo '<br>';
    var_dump(1 <= 1); // true
    echo '<br>';
    var_dump(1 == 1); // true
    echo '<br>';
    var_dump(1 == 2); // false
    echo '<br>';
    var_dump(1 != 2); // true
    echo '<br>';
    var_dump(1 != 1); // false
    echo '<br>';
    echo '<br>';

    $x = 1;
    $y = 2;
    var_dump($x < $y); // true
    echo '<br>';
    var_dump($x > $y); // false
    echo '<br>';
    var_dump($x <= $y); // true
    echo '<br>';
    var_dump($x >= $y); // false
    echo '<br>';
    echo '<br>';

    var_dump(1 < 'a'); // true 暗黙の型変換
    echo '<br>';
    var_dump(1 > 'a'); // false 暗黙の型変換
    echo '<br>';
    //PHPではこういったことも可能だが、基本的に暗黙の変換は行わないのがセオリー
    echo '<br>';

    var_dump(1==='1'); // false
    echo '<br>';
    var_dump(1==='2'); // false
    echo '<br>';
    //暗黙の型変換を行わない比較
    //型も値も合っていないとtrueにならない
    ?>
```

# June 12, 2025 StudyLog

- 変数は$で始まり、直後には数字はNG。アンダーバーかアルファベット
- 変数に文字列を代入できる
- 変数に変数も代入できる
- 変数に値を代入する＝値にあだ名をつける
- ブラウザで改行するには
  ```php
  echo '<br/>';
- echo：PHPでの出力＝HTMLへ書き込むこと
- HTML内でPHPタグで囲まれた範囲がPHPのプログラムとして認識される
- 文字列ではない部分＝プログラム＝コンピュータへの命令
- ブラウザをsafariからchromeに変更
- “”内にh1タグなどを入れることができる
- データ型：どんな種類の数値なのか
- 基本データ型10種のうちスカラ型4種：文字列、整数、少数、論理値
- 数値型は計算可能
- 四則演算：+  - * / %(剰余)
- 論理和 || (or)：または
- 論理積&&(and)：かつ
- 単項演算（否定演算）!：ではない
- NULL：無
- PHPの役割：HTMLの作成とデータの管理

# HelloWorldの実行
- Apache, MySQL Databaseが起動できたので、xamppfiles>htdocs>にhello.phpを作成
- localhost/hello.phpにHelloWorldの表示確認完了
  
# XAMPPのMySQLが起動しない問題とその解決
## 状況
- XAMPP 8.2.4をインストールしたところ、 Apacheは起動したがMySQL Databaseが起動しない。
- コントロールパネルでは「MySQL Database: stopped」となっていた。
- ターミナルで`lsof -i :3306`を実行すると、mysqldプロセスが何度も起動し、killしても直後に再起動されてしまう。
- XAMPPのバージョンを8.0.28に下げ、再インストールしたところ、MySQL Databaseが「running」となった。

## 原因と考察
- **以前、MySQLやMySQL Workbenchをインストールしていたため、システムに他のMySQLサーバーが自動起動設定されていた可能性が高い。**
- **XAMPPのMySQLがポート3306で起動しようとしても、他のmysqldがすでにポートを占有していたため、競合が発生していた。**
- **バージョンを下げて再インストールしたことで、設定や自動起動がリセットされ、競合が解消されたと考えられる。**
- **XAMPPのバージョンによってはMySQLではなくMariaDBが同梱されている場合があり、MySQL Workbenchとの互換性やポート設定が異なる場合もある。**

## 学び
- **複数のMySQLサーバーを同時に使う場合、ポート競合や自動起動設定に注意する必要がある。**
- **競合が発生した場合は、他のMySQLサーバーを停止・アンインストールするか、XAMPPのMySQLのポートを変更するなどして回避する。**
- **XAMPPのバージョンや同梱DBの種類（MySQL/MariaDB）にも注意する。**

## 備考
- 今回の経験は、Mac環境でのXAMPP運用やMySQLの競合トラブル解決の良い事例となった。

## June 10, 2025

- **PHP基礎**
    - 半角スペースと改行は同じ
    - スペースはいくつあっても1個とカウント
    - 全角スペースはエラーとなる
    - echoでString型の文字列を表示することは、htmlで文字列を表示させることと同じ

- **Linux基礎**
    - サーバーにLinuxが使われる理由
      - OSSかつ無料
      - 安定して稼働できる（GUIを取り外し少ないファイルサイズにできる）
      - セキュリティの観点からLinuxのパーミッションの機能でアクセス制限が可能
      - サーバー構築の方法
        1. 物理マシンにLinuxインストール
        2. 仮想マシンを利用（VMWareやVirtualBoxを用いて作成）
        3. レンタルサーバー(Xserver/さくらVPS/etc.)やクラウド(AWS(Amazon EC2)/Azure(Virtual Machines)/GCP(Compute Engin3))を利用
        4. コンテナ（Docker）を利用
     - コンテナ利用の関連項目
       - IPアドレス
       - ゲートウェイ
       - ポート番号
       - DNS
       - NAT
       - コマンド
       - ストレージ
       - データベース
       - ライブラリ
       - Webアプリフレームワーク
       - API

- **Docker基礎**
    - コンテナ：アプリとファイルシステムを隔離する特殊なプロセス
    - プロセス：OS上で動作している一つ一つの処理
    - コンテナを使用することで1つの物理マシン内で隔離された複数の仮想サーバーを構築できる

## June 9, 2025

- **DockerインストールとApache起動**
**Dockerの基本を理解し、PHP環境を構築する準備**

1. **Dockerインストール**
2. **Dockerの基本操作**
    - **docker run hello-worldを実行**
    - **「Hello from Docker!」との表示確認**
3. **Apacheコンテナの起動**
    - **docker run --name my-apache -p 8080:80 -d httpdを実行**
    - **ブラウザでhttp://localhost:8080に「It works!」との表示確認**
- **VMWare Fusion（Mac）でAlmaLinux仮想マシンを構築（参考図書：Linux標準教科書Ver4.0.0）**
    - 選定理由：PCがMacbook Apple M1 ProでありApple silicon搭載モデルであるためVirtualBoxの使用が不可で、無料で使用可能なソフトウェアとしてVMWare、UTMのうちVMWareを選択しインストールした
    - Arm用AlmaLinuxイメージをダウンロードし、仮想マシン作成・インストール完了
    - インストール後の初期設定（端末起動、キーボード・日本語入力の確認）
- **SSH接続の実践**
    - “sshコマンドでゲストOSに接続”
    - ローカルからリモートサーバ（AlmaLinux）へのSSH接続を実施
    - ローカルとリモートの見分けやすくするため、リモートの表示をlocalhost以外のものにしたく、プロンプトにホスト名を表示させる方法を確認し、操作環境の見易さを向上
- **シェルとLinuxカーネル（参考図書：新しいLinuxの教科書）**
    - 構造、役割を図で理解
    - 分かれている理由
        - 別のOSでの同様にシェルの操作を行える汎用性のため
        - シェルがエラーや高負荷状態となりクラッシュしてもOS本体のLinuxカーネルへの影響が最小限とすることができるため

## June 8, 2025

## **paiza の演習課題を進める中での気づき**

## **1. どんなことでつまづいたか**

paiza の演習問題で「最初の入力が回数、2 行目以降がデータ」というルールが、**なぜそうなるのか、プログラムのどの部分で決まっているのかが腑に落ちなかった**。論点は「1 行目はもう使わない」という部分で、**どの行が 1 行目で、どの部分が 2 行目以降なのか**、**プログラムのどこでどう処理されているのか**が引っかかり、下記のように解像度を上げたことで理解に至ったためそれを記す。

---

## **2. 具体的な例と解説**

## **例：入力データ**

3<br>
10<br>
15<br>
8

---

## **プログラムのどこで何をしているか**

*// ①最初の行を「回数」として読み取る*<br>
$count = (int)trim(fgets(STDIN));
*// ここで「3」が$countに入る<br>
//②$count回だけ繰り返す*<br>
for ($i = 0; $i < $count; $i++) {<br>
    *// ③for文の中で「データ」を読み取る*<br>
    $num = (int)trim(fgets(STDIN));<br><br>
    *// 1回目：2行目の「10」が$numに入る<br>
    // 2回目：3行目の「15」が$numに入る<br>
    // 3回目：4行目の「8」が$numに入る<br><br>
    // ④$numを使って何か処理する*<br>
    echo $num . "\n";<br>
}

---

## **3. なぜ「1 行目はもう使わない」のか**

- **最初の`fgets(STDIN)`で 1 行目（この例では「3」）を読み取り、`$count`に代入している**
- **その後、for 文の中で`fgets(STDIN)`を実行しているので、2 行目（「10」）、3 行目（「15」）、4 行目（「8」）が順に`$num`に入る**
- **1 行目は最初に`$count`に入れたきり、その後は特に使わない**
- **for 文の中で`fgets(STDIN)`を実行しているため、2 行目以降しか読み取らない**

---

## **4. 学び**

- **プログラムは「書かれた順番」に動く**
  - 最初に**`fgets(STDIN)`**で 1 行目を読み取り、「回数」として使う
  - for 文の中で**`fgets(STDIN)`**を実行するので、2 行目以降を「データ」として読み取る
- **「最初の行が回数、2 行目以降がデータ」というのは、この「書かれた順番」と「for 文の設計」で決まる**
- **どの行が何を意味するかは、プログラムのどの部分で`fgets(STDIN)`を実行しているかで決まる**
- **もし「1 行目もデータとして使いたい」なら、for 文の前に`$num = (int)trim(fgets(STDIN));`を追加する必要がある**

---

## **5. まとめ**

> プログラムは「上から順」に動くので、最初に fgets(STDIN)で 1 行目を読み取ると「回数」になり、for 文の中で fgets(STDIN)を実行すると「データ」になる。この「書かれた順番」と「for 文の設計」が、「最初の行が回数、2 行目以降がデータ」というルールを実現している。どの行が何を意味するかは、プログラムのどの部分で fgets(STDIN)を実行しているかで決まる。

## その他

## **1.  文末のセミコロン（;）**

- **コードのエラーで「文末のセミコロン（;）抜け」をしがち**
- **PHP では文末に必ずセミコロンが必要（例外は PHP ブロック終了直前に限る）**
- **セミコロンが抜けると構文エラーとなり、プログラムが動かなくなる**

## **2.  インデントとスペースの活用**

- **フォーマッターがなくても、自分でインデントやスペースを揃える**
- **スペースやタブ、改行は「可読性を高めるため」に使うもので、PHP の実行には影響しない**
- **for 文や if 文、変数代入など、カッコや演算子の前後にスペースがなくてもエラーにはならない**
- **ただし、スペースをまったく入れないと可読性が低くなる**
- **コーディング規約やチームのルールで「スペースや改行を入れる」ことが推奨されることが多い**

## **3.  エラーの種類と違い**

- **コンパイルエラー**
  - **プログラムの書き方（構文）のミスで、実行前に検出される**
- **ランタイムエラー**
  - **実行時の状況やデータの問題で発生するエラー**
  - **PHP や Python などインタプリタ型言語では、ほとんどすべてのエラーがランタイムエラーとして発生する**

## June 7, 2025

- 各書籍の内容を俯瞰し、必要な情報をピックアップした。
  『Web を支える技術』『かやのき先生の基本情報技術者教室』『CAREER SKILLS』『Web 系エンジニアになろう』『GitHub 実践入門』について、目次や各章のまとめを確認し、全体像を把握した。
- paiza PHP コース#10（if 文）までを進め、基礎文法の理解を深めた。
- 書籍購入
  - 安全な Web アプリケーションの作り方：セキュリティのリテラシーを広げるため
  - Docker&仮想サーバー完全入門：Docker を用いて開発環境を構築するため
