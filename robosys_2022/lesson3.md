# ロボットシステム学

## 第3回: <span style="text-transform:none">Linux環境での<br />PythonプログラミングII</span>

千葉工業大学 上田 隆一

<br />

<p style="font-size:50%">
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
</p>

---

## 今日やること

* Pythonで引数、標準入出力を操作

---

## <span style="text-transform:none">Python</span>での引数の処理

* 要点
    * システムのことを扱う<span style="color:red">sysモジュール</span>を読み込む
        * 他によく使うモジュールとしては<span style="color:red">math</span>など
    * 引数はリストになっている
* 例（`args`）
    ```python
    #!/usr/bin/python3
    import sys             #sysモジュールを読み込み
    
    print(sys.argv)        #sysの「下の」argvに引数が入るのでprintしてみる
    ```
* 実行（「`args`」という名前でコードを保存して実行）
    ```bash
    $ ./args 引数1 引数2 引数3
    ['./args', '引数1', '引数2', '引数3']    #端末に打った通りにリストに入る
    ```

---

## 引数を使ったコマンドの作成1

* 引数の数を足し合わせる`plus`というコマンドを作ってみましょう
    * とりあえず2つの引数を足す計算のコードを作る
    * 例（`plus_a`）
        ```python
        #!/usr/bin/python3
        import sys
        
        print( float(sys.argv[1]) + float(sys.argv[2]) )
        ```
        * <span style="color:red">`float`</span>: 文字列を浮動小数点数に変換 
    * 実行
        ```bash
        $ ./plus_a 1 2
        3.0
        ```

---

## 引数を使ったコマンドの作成2

* 今度は引数をすべて足すコマンドを作成
    * 例（`plus_b`）
        ```python
        #!/usr/bin/python3
        import sys
        
        x = 0.0                    #xを定義して初期化
        for n in sys.argv[1:]:     #スライスを使う
            x += float(n)          #+=で足し込む
        
        print(x)
        ```
        * 一気にコードを書かず、引数がちゃんと読み取れているか`print`で確認しながら書くこと
    * 実行
        ```bash
        $ ./plus_b 1 2 3 4 5 6 7 8 9 10
        55.0
        ```

---

## 引数を使ったコマンドの作成3

* Pythonの「リスト内包表記」を利用
    * 発展的な内容なのでPython初心者の人はやらないでよいです
    * 例（`plus_c`）
        ```python
        #!/usr/bin/python3
        import sys
        
        nums = [ float(e) for e in sys.argv[1:] ]   #引数を浮動小数点数に変換してリスト作成
        print(sum(nums))                            #リストの和を返すsum関数を利用
        ```
