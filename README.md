# Useful-Terminal-Command
Zorin OSを使っていて、便利なターミナルのコマンド。

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
Icon=/usr/share/icons/Zorin/16x16/places/user-trash.svg
Exec=nautilus trash://
NoDisplay=false
Categories=Utility
StartupNotify=false
Terminal=false
```

## PCの電源を切る
`gnome-session-quit --power-off`

これを利用して、`~/.local/shere/applications`に以下のようなdesktopファイルを作れば…
```
[Desktop Entry]
Version=1.0
Type=Application
Name[ja]=電源を切る
Name=Power off
Icon=/usr/share/icons/ZorinGrey-Dark/16x16/panel/system-devices-panel-alert.svg
Exec=gnome-session-quit --power-off
NoDisplay=false
Categories=Utility
StartupNotify=false
Terminal=false
```

## Conkyの自動起動
`conky --daemonize --pause=5`

こうしないと、表示がおかしくなるようだ。

### おまけ
```
conky.config = {
    alignment = 'top_right',
    default_color = 'white',
    double_buffer = true,
    font = 'M+ 1mn:size=12',
    gap_x = 10,
    gap_y = 10,
    draw_shades = false,
    own_window = true,
    own_window_type = 'desktop',
    own_window_argb_visual = true,
    own_window_colour = '#000000',
    own_window_argb_value = 127,
    use_xft = true,
    default_bar_height = 6,
    default_bar_width = 80,
    short_units = true,
}

conky.text = [[
$alignc${font M+ 1mn:size=36}${time %R}$font
$alignc${time %F} ${time %A}
CPU: ${alignr}${freq} M $cpubar
RAM: ${alignr}${mem} $membar
Swap: ${alignr}${swap} $swapbar
File: ${alignr}${fs_used} $fs_bar
Temp: ${alignr}${acpitemp} °C
]]
```
