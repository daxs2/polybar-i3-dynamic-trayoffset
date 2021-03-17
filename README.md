# polybar-dynamic-trayoffset
*For an english version of this readme, <a href="https://github.com/daltroaugusto/polybar-dynamic-trayoffset/blob/main/README_EN.md">click here</a>.*

Apenas alguns scripts capazes de criar a experiência de uma "traybar dinâmica" para a Polybar no i3wm, fazendo-a com que se comporte *tipo* um módulo.

## Requisitos
1. Versão recente da [Polybar](https://github.com/polybar/polybar/);
2. i3wm (preferencialmente v.4.17+);
3. Instalar os scripts e o módulo corretamente.

## Instalação
1. Baixe a release mais recente ou clone este repositório com ```git clone https://github.com/daltroaugusto/polybar-dynamic-centered-tray.git```, depois navegue para a pasta extraída;
2. Execute ```sudo ./install``` (script de instalação com privilégios de superusuário), ou copie os scripts para uma pasta em seu ```$PATH```;
3. Insira o módulo ```polybar_trayoffset``` na posição em que desejar, no arquivo de configuração da Polybar:

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

4. Certifique-se de, também, configurar corretamente o offset da traybar. A tray deve estar posicionada de modo que sobreponha o módulo.

<div align="center">
<img width="800" src="https://i.imgur.com/qIO6jeI.png" alt="Imagem mostrando a barra de tray sem posicionamento e ação do módulo trayoffset." />

Perceba como a tray está fora de posição. O módulo está posicionado à direita do relógio. Devemos corrigir isso configurando de modo que a tray esteja exatamente onde o módulo fará seu trabalho (nesse caso, mais à direita do relógio), usando as configurações ```tray-offset-x``` e ```tray-position```:

<table>
<tbody>
<tr>
<td><img width="330" src="https://i.imgur.com/ZH14U9x.png" /></td>
<td><img src="https://i.imgur.com/TBzl2Dm.png" /></td>
</tr>
</tbody>
</table>
</div>

5. Agora que o módulo está exatamente na posição em que a tray é invocada pela Polybar, devemos, manualmente, configurar *hooks* para cada programa que vá usar a tray. Suponhamos que o programa ```qbittorrent``` (um cliente torrent em Qt) deseje usar espaço em nossa traybar. Devemos adicionar, então, o seguinte trecho de código em nosso arquivo de configuração do i3wm:

```
for_window [class="qbittorrent"] exec watchps_tray qbittorrent
```

Esse comando fará com que, a cada vez que se detecte uma janela da classe do aplicativo (que também ocupará espaço na tray), se inicie um processo que mantém espaço no lugar do módulo previamente configurado, fazendo com que o resultado seja uma traybar *mais ou menos* dinâmica, conforme a imagem:

<div align="center">
<img src="https://i.imgur.com/GDnAOcw.png" width="800">
</div>

## Configuração adicional

* Por meio das configurações de <a href="https://github.com/polybar/polybar/wiki/Fonts">fontes</a> da Polybar, é possível, em conjunto com ```format-prefix``` e ```format-suffix```, definir uma fonte de largura fixa para o módulo (como Consolas), fazendo com que a largura acrescentada para cada aplicação da tray seja igualmente fixa. É uma opção não recomendada, pessoalmente.
* Com um número inteiro e positivo ao lado do nome da aplicação em ```watchps_tray <aplicação>```, é possível definir manualmente o tamanho de espaçamento criado na tray.
* Para situações excepcionais, o comando ```polybar_trayoffset remove-all``` pode ser executado globalmente, e todo espaçamento acrescentado no módulo será imediatamente removido.

## A fazer
- [ ] Centralizar a gestão de aplicações que usam da tray no próprio script ```polybar_trayoffset```.
- [ ] Encontrar alguma ferramenta ou mecanismo similar ao que o <a href="https://sites.google.com/site/tstyblo/wmctrl/">wmctrl</a> é para janelas, porém para elementos da tray, o que possibilitaria um fluxo/funcionamento mais automático.
