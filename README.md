# Useful-Terminal-Command
Zorin OSを使っていて、便利なターミナルのコマンド。

## インストールされているパッケージの一覧を、テキストファイルに書き出す
`sudo dpkg -l | awk '/^ii/ { print $2 }' >package-list`
> [Can I routinely log the packages I install of my own choice?](https://forum.zorin.com/t/can-i-routinely-log-the-packages-i-install-of-my-own-choice/21355/3)

## OptiPNGで、カレントディレクトリのPNGファイルを一括処理する
`find . -type f -name '*.png' -exec optipng {} +`
> [OptiPNG で PNG ファイルの最適化を行う方法](https://linux.keicode.com/tools/optipng.php)

## Evolutionのサービスを自動起動させない
```
mkdir -p ~/.config/autostart/
cp /etc/xdg/autostart/org.gnome.Evolution-alarm-notify.desktop ~/.config/autostart/
sed -i "s/NoDisplay=true/NoDisplay=false/" ~/.config/autostart/org.gnome.Evolution-alarm-notify.desktop
```
```
systemctl --user mask evolution-addressbook-factory.service
systemctl --user mask evolution-calendar-factory.service
systemctl --user mask evolution-source-registry.service
systemctl --user mask evolution-user-prompter.service
```
> [How to stop evolution-alarm-notify](https://askubuntu.com/questions/1317784/how-to-stop-evolution-alarm-notify)

## ターミナルからゴミ箱を開く
`nautilus trash://`
> [How to open "Trash" through terminal?](https://askubuntu.com/questions/327943/how-to-open-trash-through-terminal)

これを利用して、`~/.local/shere/applications`に以下のようなdesktopファイルを作れば、メインメニューにアプリケーションとして表示される。お気に入りに登録すれば、タスクバーからゴミ箱を開くことも出来る。
```
[Desktop Entry]
Version=1.0
Type=Application
Name[ja]=ゴミ箱
Name=Trash
Icon=/usr/share/icons/ZorinGrey-Dark/16x16/actions/edit-delete.svg
Exec=nautilus trash://
NoDisplay=false
Categories=Utility;GTK;GNOME;
StartupNotify=false
Terminal=false
```
