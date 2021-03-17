# polybar-dynamic-trayoffset
A bunch of scripts able to create a "dynamic traybar" experience for Polybar in i3wm, making it behave *kinda like* a module.

## Requirements
1. A recent version of [Polybar](https://github.com/polybar/polybar/);
2. i3wm (rather v.4.17+);
3. Install scripts, hooks and module.

## Installation
1. Download the latest release and extract to a folder or clone this repository with ```git clone https://github.com/daltroaugusto/polybar-dynamic-trayoffset.git```, then browse to the working folder;
2. Run ```sudo ./install``` (installation script with root privileges), or just copy the scripts to a folder in your ```$PATH```;
3. Insert the ```polybar_trayoffset``` module at the position you prefer, in Polybar config file:

<table align="center">
    <tbody>
        <tr>
            <td><img src="https://i.imgur.com/Jp2SVAv.png" /></td>
            <td>
                
    [module/trayoffset]
    type = custom/script
    interval = 1.0
    exec = polybar_trayoffset echo
    format = <label>
                
</td>
</tr>
</tbody>
</table>

4. Make sure to also set up properly the traybar's offset. The tray must be positioned in a way that overlays the module.

<div align="center">
<img width="800" src="https://i.imgur.com/qIO6jeI.png" alt="Image showing the tray bar without positioning and action from trayoffset module." />

Notice how the tray is out of position. The module is positioned to the right of the clock. We need to correct this setting up in a way that tray stay exactly where the module will do their work (in this case, more to the right of the clock), by using the parameters ```tray-offset-x``` and ```tray-position```:

<table>
<tbody>
<tr>
<td><img width="330" src="https://i.imgur.com/ZH14U9x.png" /></td>
<td><img src="https://i.imgur.com/TBzl2Dm.png" /></td>
</tr>
</tbody>
</table>
</div>

5. Now that the module is exactly in the position where tray is invoked by Polybar, we must, manually, set up *hooks* for every program that would use the tray. Let's say that ```qbittorrent``` (a Qt-based torrent client) wants to use some space in our traybar. Then we'd need to add the following statement in our i3wm's config file:

```
for_window [class="qbittorrent"] exec watchps_tray qbittorrent
```
This command will make that, for each time a window of such that application's class is detected (that will also occupies space in tray), will also be started an instance of ```watchps_tray``` that keeps needed space in the module previously setted up, what will give you a *kinda* dynamic traybar experience, just as follows:

<div align="center">
<img src="https://i.imgur.com/GDnAOcw.png" width="800">
</div>

## Extra settings

* By setting up the <a href="https://github.com/polybar/polybar/wiki/Fonts">fonts</a> in Polybar, it is possible to define, with ```format-prefix``` and ```format-suffix```, a monospaced font for the module (like Consolas), which would make the added largure for each application as fixed as any character of that font (regardless any other font in the bar). This is a not recommended option, personally.
* By inserting an integer and positive number aside the application's name in ```watchps_tray <application>```, it is possible to manually set up the spacing size created in tray.
* Just for exceptional situations, the command ```polybar_trayoffset remove-all``` can be globally executed, and any spacement added within the module will be immediately removed.

## To do
- [ ] Centralize the management of apps that use the tray within the ```polybar_trayoffset``` script.
- [ ] Find some tool or mechanism similar to what <a href="https://sites.google.com/site/tstyblo/wmctrl/">wmctrl</a> is for windows, but for tray elements, what would make possible a more automatic flow/behavior.
