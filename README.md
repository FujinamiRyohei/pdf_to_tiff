# PDF to TIFF

PDF画像を(白黒=grayscaleの)TIFFへ変換するサンプルです。

Dependency

* [pdf2image](https://github.com/Belval/pdf2image)

## How to run

変換後の形式は以下になります。
- 解像度：400 dpi
- ファイル形式：マルチページTIFF
- カラー：モノクロ2階調
- 圧縮形式：CCITT Group 4

### Lambda Style

![lambda_style.PNG](./docs/lambda_style.PNG)
※現在は上記の仕様を満たしていません。

1. Dockerを利用できる環境を用意する。

2. 以下のコマンドを順番に実行してAWS Lambdaにデプロイするパッケージを作成する。
    ```
    docker build -t pdf-to-tiff .
    docker run -d --name package-build pdf-to-tiff
    docker cp package-build:deploy.zip .
    docker rm package-build
    ```

3. AWS Lambdaに作成した`deploy.zip`をアップロードする。

    ランタイム：Python3.8  
    ハンドラ：main.handler

4. 以下のコマンドで動作確認が可能
    ```
    aws lambda invoke --function-name Lambda関数名 test.tif
    ```
    ※Lambda関数内のpdfがtiffに変換されて`test.tif`として返却される。

### Fargate Style
[こちら](./development/README.md)を参照
