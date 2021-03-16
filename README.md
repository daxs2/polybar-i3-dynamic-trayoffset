# polybar-dynamic-centered-tray
Apenas alguns scripts capazes de criar a experiência de uma "traybar dinâmica" para a Polybar, fazendo-a com que se comporte *tipo* um módulo.

## Requisitos
1. Versão recente da [Polybar](https://github.com/polybar/polybar/);
2. i3wm (preferencialmente v.4.17+);
3. Instalar os scripts e o módulo corretamente.

## Instalação
1. Baixe a release mais recente ou clone este repositório com ```git clone https://github.com/daltroaugusto/polybar-dynamic-centered-tray.git```, depois navegue para a pasta extraída;
2. Execute ```sudo ./install``` (script de instalação com privilégios de superusuário), ou copie os scripts para uma pasta em seu ```$PATH```;
3. Insira o módulo ```polybar_trayoffset``` na posição em que desejar, no arquivo de configuração da Polybar:

<table>
    <tbody>
        <tr>
            <td><img src="https://i.imgur.com/Jp2SVAv.png" /></td>
            <td>
                ```
[module/trayoffset]
type = custom/script
interval = 1.0
exec = polybar_trayoffset echo
format = <label>
                ```
            </td>
        </tr>
    </tbody>
</table>