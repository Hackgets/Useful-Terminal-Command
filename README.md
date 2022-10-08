# Useful-Terminal-Command
Zorin OSを使っていて、便利なターミナルのコマンド。

## インストールされているパッケージの一覧を、テキストファイルに書き出す
`sudo dpkg -l | awk '/^ii/ { print $2 }' >package-list`
> [Can I routinely log the packages I install of my own choice?](https://forum.zorin.com/t/can-i-routinely-log-the-packages-i-install-of-my-own-choice/21355/3)

## OptiPNGで、カレントディレクトリのPNGファイルを一括処理する
`find . -type f -name '*.png' -exec optipng {} +`
> [OptiPNG で PNG ファイルの最適化を行う方法](https://linux.keicode.com/tools/optipng.php)
