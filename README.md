# Galaxy Tab Screen — Samsung Galaxy Tab como segunda tela no Linux


[![Capa do Galaxy Tab Screen para Linux](linkedin-cover-galaxy-tab-screen-linux.jpg)](linkedin-cover-galaxy-tab-screen-linux.jpg)

Estou desenvolvendo o **Galaxy Tab Screen** para usar meu Samsung Galaxy Tab como segunda tela no Linux. Testo com um **Galaxy Tab S10 FE no Kubuntu/KDE Plasma**.

Já uso a tela independente com S Pen, touch e som pelo cabo ou pelo Wi-Fi. Pelo cabo, mantenho a depuração USB desligada.

Comecei pelo VNC e não gostei. Depois consegui espelhar usando o “Segunda tela” da Samsung com GNOME Network Displays. Para ter tela independente, caneta e touch, comecei a adaptar o [UScreen](https://github.com/majmichu1/UScreen).

Já consegui desenhar no Krita com pressão e inclinação da S Pen, apoiar a mão sem interferência nas rodadas e usar dois dedos para mover e ampliar a folha. O computador também oferece uma saída de som para o tablet. Agora a tela chegou à resolução nativa, **2304 × 1440 a 90 Hz**, e posso escolher resolução e atualização pelo PC ou pelo aplicativo.

O nome ficou **Galaxy Tab Screen**, e o repositório é `galaxy-tab-screen-linux`.

Estou registrando o processo para aprender com os testes e entender os problemas que aparecem.

Também conto com [Edmundo Neto](https://github.com/emal0n), trocando ideias sobre desenvolvimento, produto e próximos passos.

## O que já funcionou

| Parte | O que conferi no S10 FE |
| --- | --- |
| Cabo sem depuração | Vídeo, entrada e áudio pela rede criada com a Ancoragem USB, sem ADB |
| Wi-Fi sem cabo | Tela independente, S Pen, touch e som pela rede local, sem ADB |
| Tela independente | Área adicional no KDE, chegando a 2304 × 1440 a 90 Hz pelo Wi-Fi, mantendo as telas físicas |
| Resolução e atualização | Escolha no KDE e no aplicativo; os controles do tablet acompanham as alterações feitas no PC |
| S Pen no Krita | Desenho alinhado à ponta e pressão mudando a espessura pelo cabo e pelo Wi-Fi |
| Inclinação | Traço mais grosso ao inclinar, com um pincel preparado para responder só à inclinação |
| Botão lateral | Move a folha no Krita, como botão do meio nessa configuração |
| Touch | Até cinco dedos na área de teste; dois dedos movem e ampliam/reduzem a folha no Krita |
| Mão apoiada | Desenhei sem interferência nas rodadas curtas, aproximando a caneta antes de apoiar a mão |
| Som | Saída “Galaxy Tab S10 FE (teste)” no PC, com reprodução e troca de saída conferidas por USB e Wi-Fi |
| Retirada do cabo | Aviso de desconexão no tablet, liberação dos contatos e retirada da tela virtual |
| Reconexão USB | A imagem voltou sozinha depois de reconectar na mesma porta e reativar a Ancoragem USB |

Os testes de desenho no Krita foram feitos em 1280 × 800. Depois validei a imagem na resolução nativa e a troca de modos pelo Wi-Fi. As novas opções também foram preparadas para USB, mas ainda falta repetir essas trocas pelo cabo. Os testes com a mão apoiada foram curtos e não cobrem todas as posições de uso.

Deixei resultados, erros e correções no [registro dos testes](docs/testes.md), junto com [o que conferi do UScreen e o que falta](docs/testes.md#conferencia-uscreen). Os números de desempenho e as afirmações de segurança do original não comprovam os resultados da minha adaptação.

## Resolução e Hz agora são uma escolha

A primeira imagem pelo cabo estava em 1280 × 800, com alvo de 30 fps. Mudei para 60 fps, mas continuei achando lenta. Depois aumentei para 90 fps e 60 Mbps. Melhorou muito!

1280 × 800 era a configuração inicial do teste. O aplicativo e o KDE agora oferecem:

| Resolução | Atualização |
| --- | --- |
| 2304 × 1440, nativa | 30, 60 ou 90 Hz |
| 1920 × 1200 | 30, 60 ou 90 Hz |
| 1600 × 1000 | 30, 60 ou 90 Hz |
| 1280 × 800 | 30, 60 ou 90 Hz |

Encontrei um problema ao mudar pelo PC: a imagem mudava, mas o aplicativo continuava mostrando a escolha antiga. No teste 10 isso foi corrigido. A linha “Ativa no PC” e os controles se atualizam mesmo com as configurações do tablet abertas.

Deixei 2304 × 1440 a 90 Hz e mantive os 60 Mbps. Não retomei a investigação de fluidez, e configurar 90 Hz não comprova 90 quadros exibidos por segundo em qualquer situação. Ainda não tenho uma comparação medida com o aplicativo da Samsung no Windows.

## Como está funcionando

No cabo, uso a rede da **Ancoragem USB**. No Wi-Fi, PC e tablet precisam estar na mesma rede local. O host Linux cria a tela com EVDI e captura/codifica H.264 pela GPU. O Android recebe o vídeo e envia os eventos de caneta e touch para o Linux.

Instalei o aplicativo manualmente e confirmei a sessão no tablet. O endereço usado pelo aplicativo fica o mesmo ao reconectar na porta USB testada, mesmo quando a rede recebe outro endereço automático. A sessão Wi-Fi usa o endereço próprio dessa rede. Não precisei ativar a depuração USB em nenhum desses testes.

O som usa um canal separado. Escolho a saída do tablet nas configurações de áudio do computador. Havia um problema que repetia no tablet o áudio já enviado à caixa Bluetooth; corrigi a origem da captura e repeti a troca de saída pelo Wi-Fi e pelo cabo. O som ficou somente na saída escolhida.

Essas mudanças fazem parte da adaptação local. A versão do UScreen usada como base depende de ADB no caminho USB consultado. O resultado pelo Wi-Fi descrito aqui também usa o aplicativo adaptado; o teste com o receptor nativo da Samsung continua separado.

## Como estou organizando

Estou fazendo por etapas. Nesta rodada, preferi testar e reunir os registros depois. Os relatórios completos ficam no meu computador; aqui entram as explicações, sem endereços da rede nem inventário do PC.

Reuni as etapas no [registro dos testes](docs/testes.md), incluindo cabo, Wi-Fi, áudio, Krita e a escolha de resolução e Hz.

O [plano de testes](docs/plano.md) mostra o que pretendo fazer em seguida. A comparação dos projetos, os arquivos que consultei e os créditos estão nas [referências](docs/referencias.md).

Este repositório reúne a documentação. Os APKs ficam apenas nas páginas locais de teste e não serão disponibilizados no GitHub. O código adaptado e os APKs de teste ainda estão no computador; não publiquei uma versão pronta para uso. A adaptação parte do [UScreen](https://github.com/majmichu1/UScreen/tree/66f6bcdab918b8dcc44227dde00197f30a778c44), com os créditos e a licença MIT preservados na cópia local. A base Miracast continua sendo o [GNOME Network Displays](https://gitlab.gnome.org/GNOME/gnome-network-displays), no commit `c305023f1e6d8ab48d18c66a4efbd18e1df7cdee`, sem mudanças no código.
