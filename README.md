

### 🇧🇷 [Исходник] Tutorial ImGui Lua BR (Moonloader)

**Autor:** Haru Urara
**Data de Início:** 7 Set 2025

-----

## ***Tutorial feito para quem é Brasileiro***

***Uns tempos atrás, a moderação chutou minha bunda quando fiz um tutorial que particularmente era péssimo. Agora que me aprofundei em Moon Imgui, posso fazer o tutorial sem ter uma crise existencial novamente...***

-----

### ***Dependências :***

  * [Lua para windows](https://github.com/rjpcomputing/luaforwindows/releases/tag/v5.1.5-52)
  * [SA-MP 0.3.7](https://www.sa-mp.mp/downloads/)
  * [Asi Loader](https://www.mixmods.com.br/2025/07/sa-silent-asi-loader/)
  * [Moonloader](https://www.mixmods.com.br/2020/10/moonloader/)
  * [ImGui Lua](https://www.mixmods.com.br/2019/08/imgui-interface-grafica-para-moonloader/)

-----

### ***Aviso :***

#### ***A IDE é seu critério, gosto de [Notepad ++](https://notepad-plus-plus.org/downloads/) e [Sublime Text](https://www.sublimetext.com/) com [Auto Complete](https://www.blast.hk/threads/13315/#post-118518) de ImGui ou Moonloader para menu grande***

***Não precisa ter um computador incrível para progamar Lua, apenas tenha força de vontade, eu mesmo uso um notebook de 1.0 GHz e estou vivo 💀***

***Não tenha pressa para aprender. Programação é treino, persistência e corrigir erros.***

-----

### Inicio :

***O que saber no inicio?***

  * obviamente saber o básico de [Lua](https://www.lua.org/), você pode ver cursos no youtube (recomendo [CFB Cursos](https://www.youtube.com/c/cfbcursos)), ou ler (nerd).
  * não achar que vai fazer um menu complexo em 2 segundos
  * saber lidar com erros

***Nâo vou ensinar Lua aqui, crie vergonha na cara e vá estudar\!***

-----

### ***Básico :***

O código abaixo cria a estrutura básica da janela.

```lua
local imgui = require "imgui"  --precisa do arquivo imgui em sua lib

function imgui.OnDrawFrame() -- OnDrawFrame é um nome obrigatório pois contém o conteúdo do menu
  imgui.Begin('Janela ImGui') --Nome da Janela
  imgui.Text('Texto da janela') --Texto dentro da janela
  imgui.End() --Finaliza o codigo do menu
end

function main() -- Obrigatório,sem function main,seu menu nao vai abrir
  imgui.Process = true -- O Menu será processado enquanto imgui.Process for verdadeiro
end -- Finaliza o main
```

**Isso Vira um menu redimensionável e não fechável**  <br> <img width="109" height="57" alt="1757207674804" src="https://github.com/user-attachments/assets/6966f1f8-f408-4766-86ac-f77add85396e" />



-----

### **Ainda Básico :**

#### ***Checkbox***

```lua
local checkbox = imgui.ImBool(false) -- Variável da checkbox,false para começar desmarcado

imgui.Checkbox("Checkbox",checkbox)  -- Você pode acessar o valor da checkbox (ativado ou não) com '.v'
```

<img width="92" height="26" alt="1757377135283" src="https://github.com/user-attachments/assets/9c14fa38-8e8a-42b5-95d4-984bf83b19f0" />


#### ***Slider Int e Slider Float***

**Slider Int (Valores inteiros):**

```lua
local sliderint = imgui.ImInt(0) -- Valor inteiro,começa em zero

imgui.SliderInt("Slider Inteiro",sliderint,0,10) -- Vai de 0 a 10

--Você pode pegar os valores do slider com '.v' Exemplo : sliderint.v
```

<img width="315" height="23" alt="1757376765189" src="https://github.com/user-attachments/assets/f48dc497-7189-4df7-a3da-1b22a1df6333" />


**Slider Float (Valores decimais):**

```lua
local sliderfloat = imgui.ImFloat(0.0) -- Valor Decimal,começa em 0.0

imgui.SliderFloat("Slider Decimal ",sliderfloat,0.0,100.0) -- Vai de 0.0 a 100.0

--Você pode pegar os valores do slider com '.v' Exemplo : sliderfloat.v
```
<img width="325" height="23" alt="1757376849841" src="https://github.com/user-attachments/assets/bb70f98e-41f0-4a0c-a2f0-15ab4bf590ff" />


#### **Input Text (Caixinhas de texto)**

```lua
local text = imgui.ImBuffer(256) -- Variável do Input Text. 256 é o máximo de letras

imgui.InputText("Adicione um texto",text)

--Você pode pegar os valores dos Input's com '.v' Exemplo : text.v
```

<img width="344" height="27" alt="1757376884387" src="https://github.com/user-attachments/assets/92ec8210-3647-4222-8aaa-efb5eecd060f" />


-----

### ***Juntando Tudo : Menu Completo***

Este código junta todos os widgets e usa a tecla **F2** para abrir e fechar o menu.

```lua
local imgui = require "imgui" --precisa do arquivo imgui

local key = require "vkeys" -- precisa do arquivo vkeys

local menu = imgui.ImBool(false) --Valor booleano false,janela começa fechada

local sliderinteiro = imgui.ImInt(0) --Slider começa em zero

local sliderdecimal = imgui.ImFloat(0.0) --Começa em 0.0

local texto = imgui.ImBuffer(256) -- Vai até 256 letras (Máximo)

local checkbox = imgui.ImBool(false) --Começa desmarcado o checkbox

function imgui.OnDrawFrame() -- OnDrawFrame é nome obrigatório pois contém o conteúdo do menu
if menu.v then --sem isso,o botao de fechar nao funciona
imgui.SetNextWindowSize(imgui.ImVec2(350, 200), imgui.Cond.FirstUseEver) --Seta a posição inicial, Cond.FirstUseEver permite fechar com X
  imgui.Begin('Janela ImGui',menu) --usado para controlar o abre e fecha
 
  imgui.Text('Texto da janela') --Texto dentro da janela
 
  imgui.Button("Clique me") --Botao basico
 
  imgui.SliderInt("Slider Inteiro",sliderinteiro,0 ,10) -- vai de zero a 10
 
  imgui.SliderFloat("Slider Decimal",sliderdecimal,0.0,10.0) --Vai de 0.0 até 10.0
 
  imgui.Checkbox("Checkbox",checkbox) --Checkbox
 
  imgui.InputText("Adicione um texto",texto) --Caixa de texto compatível com letras latinas
 
  imgui.End() --Finaliza o codigo do menu
  end
end


function main()
  while true do --enquanto verdadeiro
    wait(0) -- espera 0 segundos
    if wasKeyPressed(key.VK_F2) then --Se F2 for apertado, Menu abre ou fecha
        menu.v = not menu.v -- .v pega o valor booleano da variavel menu
    end
    imgui.Process = menu.v -- O Menu será processado enquanto menu for verdadeiro
  end
end
```

***Como ficou :***

<img width="354" height="207" alt="1757210338004" src="https://github.com/user-attachments/assets/e9446df1-f812-4962-9308-edb545653389" />


-----

### ***InputInt e InputFloat :***

Opção de caixa de texto que só aceita números e tem botões de + e -.

```lua
           local input1 = imgui.ImInt(0) -- Valor inteiro,começa em zero
            local input2 = imgui.ImFloat(0.0) -- Valor decimal,começa em zero

            imgui.InputInt("Input1", input1) -- Caixa de texto so que de numeros inteiros e com botão + e -
            imgui.InputFloat("Input2", input2) -- Caixa de texto de valor decimal
```

***Como fica :***

<img width="397" height="47" alt="Untitled4" src="https://github.com/user-attachments/assets/18dce89b-59f7-47c8-b45b-4d22a073ea46" />



### Como definir o tamanho de um botão e sua cor?

***Usando `ImVec2` e `ImVec4` isso é possivel.***

#### Como definir o tamanho (`ImVec2`):

```lua
imgui.Button("Meu Botão", imgui.ImVec2(200, 40))
                             -- Explicação
-- imgui.Button(texto, imgui.ImVec2(largura, altura))
```

***Aqui vão exemplos de botões :***

```lua
-- Botão quadrado
imgui.Button("Quadrado", imgui.ImVec2(50, 50))

-- Botão largo
imgui.Button("Largo", imgui.ImVec2(300, 30))

-- Botão fino
imgui.Button("Fino", imgui.ImVec2(100, 20))
```

***Como fica :***

<img width="330" height="115" alt="1758383144245" src="https://github.com/user-attachments/assets/fb7ab6b6-4a7e-4212-ac35-c8e572423e73" />


> **Claro que não fica tão legal, recomendo usar as 'flags windows' para deixar sem as bordas.**

Você também pode usar `imgui.PushItemWidth()` para definir a largura de outros itens.

### ***Exemplo PushItemWidth :***

```lua
imgui.PushItemWidth(20)
imgui.Button("Botão")

imgui.PushItemWidth(50)
imgui.SliderInt("Slider", sliderint, 0, 10)

imgui.PushItemWidth(50)
imgui.Checkbox("Checkbox",checkbox)
```
<img width="109" height="77" alt="1758384674125" src="https://github.com/user-attachments/assets/c0ea8869-f864-4405-9f10-47cce7f7dd2a" />


#### ***Como escolher cor do botão com ImVec4? :***

```lua
imgui.PushStyleColor(imgui.Col.Button, imgui.ImVec4(r,g,b,a))

-- Seu botão

imgui.PopStyleColor() -- termina a aplicação das cores (Obrigatório)
```

**📌 Exemplo básico:**

```lua


imgui.PushStyleColor(imgui.Col.Button, imgui.ImVec4(0.2, 0.6, 1.0, 1.0)) -- Azul claro

if imgui.Button("Clique Aqui", imgui.ImVec2(200, 40)) then
    sampAddChatMessage("Você clicou no botão!", 0xFFAA00)
end

imgui.PopStyleColor()


```
Notas:
• Os valores do ImVec4 vão de 0.0 a 1.0 (não use 255!).
• Ordem: vermelho, verde, azul, alpha (transparência) .
• Sempre use PopStyleColor() depois para resetar o estilo. 
-----

# Exemplos de cores:

```lua
imgui.ImVec4(1.0, 0.0, 0.0, 1.0) -- vermelho
imgui.ImVec4(0.0, 1.0, 0.0, 1.0) -- verde
imgui.ImVec4(0.2, 0.6, 1.0, 1.0) -- azul claro
imgui.ImVec4(0.7, 0.7, 0.7, 1.0) -- cinza claro
```
# Exemplo Real : 

```lua


local vermelho = imgui.ImVec4(1.0, 0.0, 0.0, 1.0) -- vermelho
local verde = imgui.ImVec4(0.0, 1.0, 0.0, 1.0) -- verde
local azul = imgui.ImVec4(0.2, 0.6, 1.0, 1.0) -- azul claro
local cinza = imgui.ImVec4(0.7, 0.7, 0.7, 1.0) -- cinza claro

                    --Vermelho
        imgui.PushStyleColor(imgui.Col.Button,vermelho)
        imgui.Button("Vermelho")
        imgui.PopStyleColor()
 
                      --Verde
        imgui.PushStyleColor(imgui.Col.Button,verde)
        imgui.Button("Verde")
        imgui.PopStyleColor()
 
                       --Azul
        imgui.PushStyleColor(imgui.Col.Button,azul)
        imgui.Button("Azul ")
        imgui.PopStyleColor()
 
                      --Cinza
        imgui.PushStyleColor(imgui.Col.Button,cinza)
        imgui.Button("Cinza")
        imgui.PopStyleColor()


```
E ele fica assim :

<img width="104" height="98" alt="1758382325395" src="https://github.com/user-attachments/assets/6a39001b-2e91-48f2-a356-6f795f90af86" />

### *** Imgui Addons : ​***

Radio Button : 

```lua


 local checked_radio = imgui.ImInt(1) --Radio button começa na opção 1
 
        imgui.RadioButton("Radio 1",checked_radio,1) --Radio button opção 1

        imgui.SameLine() --Próximo elemento na mesma linha

        imgui.RadioButton("Radio 2",checked_radio,2) --Radio button opção 2

        imgui.SameLine() --Próximo elemento na mesma linha

        imgui.RadioButton("Radio 3",checked_radio,3) --Radio button opção 3

-- Você pode criar condições como
if imgui.RadioButton("Radio 1 ", checked_radio, 1) then
        -- Seu código
    end

```
<img width="231" height="23" alt="1757379674988" src="https://github.com/user-attachments/assets/d024e2ea-dcf4-4256-9fd2-b2a16132a9b4" />

Combo :

```lua


local combo = {"test","test2","test3"} -- Array de strings para o combo

 imgui.Combo("Combo 1",combo_select,combo) -- Lista com opções do combo
-- Você pode pegar valores assim

local select_combo = 1 --- Armazena o índice do item que foi selecionado

local combo_itens = {"teste","test2","test3"} -- Array dos itens

if imgui.Combo("Combo 1",select_combo,combo_itens) then

 if select_combo == 1 then Se colocar teste no Combo então ...
-- Seu código

elseif select_combo == 2 then Se colocar test2 no Combo então ...
-- Seu código

elseif select_combo == 3 then -- Se colocar test3 no Combo então ...
-- Seu código
end


```
<img width="320" height="21" alt="1757379941887" src="https://github.com/user-attachments/assets/fd419980-ce58-4767-b318-f0ce78467253" />

ToggleButton : 
```lua


imgui.ToggleButton = require('imgui_addons').ToggleButton --Importa toggle button (Obrigatório)

toggle_status = imgui.ImBool(false) --Toggle 3 começa desligado

imgui.ToggleButton("Toggle que faz nada",toggle_status) -- ToggleButton com texto

-- Você pode pegar valores com '.v' Exemplo : toggle_status.v


```
<img width="160" height="19" alt="1757381059390" src="https://github.com/user-attachments/assets/95f80696-4e0c-4413-9ade-c36838604a10" />

```lua

script_name("Botoes teste") -- Nome do script (Aparece no console SampFuncs)

local imgui = require "imgui" --precisa do arquivo imgui
local key = require "vkeys" -- precisa do arquivo vkeys

local menu = imgui.ImBool(false) --Valor booleano false,janela começa fechada
local arr_str = {"test","test2","test3"} --Array de strings para o combo

local checked_test = imgui.ImBool(false) --Checkbox 1 começa desmarcado
local checked_test_2 = imgui.ImBool(false) --Checkbox 2 começa desmarcado
local checked_radio = imgui.ImInt(1) --Radio button começa na opção 1
local combo_select = imgui.ImInt(0) --Combo começa no primeiro item (índice 0)

--Configuração dos addons
imgui.ToggleButton = require('imgui_addons').ToggleButton --Importa toggle button
toggle_status = imgui.ImBool(false) --Toggle 1 começa desligado
toggle_status_2 = imgui.ImBool(false) --Toggle 2 começa desligado
toggle_status_3 = imgui.ImBool(false) --Toggle 3 começa desligado
imgui.HotKey = require('imgui_addons').HotKey --Importa hotkey
imgui.Spinner = require('imgui_addons').Spinner --Importa spinner (círculo girando)
imgui.BufferingBar = require('imgui_addons').BufferingBar --Importa barra de progresso
local str_id = {"test","test2","test3"} --Array não usado

function main()
    repeat wait(0) until isSampAvailable() --Espera o SA-MP carregar
 
    sampRegisterChatCommand('addons', function() --Registra comando /addons para abrir ou fechar o menu
        menu.v = not menu.v --Abre ou fecha o menu
    end)
 
    while true do --Loop infinito
        wait(0) --Espera 0 segundos
        imgui.Process = menu.v and true --Processa ImGui se menu estiver aberto
    end
end



function imgui.OnDrawFrame() --OnDrawFrame é nome obrigatório pois contém o conteúdo do menu
    if not menu.v then --Se menu fechado
        imgui.Process = false --Para de processar ImGui
    end
 
    if menu.v then --Se menu aberto
        imgui.SetNextWindowSize(imgui.ImVec2(400, 300), imgui.Cond.FirstUseEver) --Tamanho inicial 400x300, Cond.FirstUseEver permite fechar com X
        imgui.Begin('Aprendendo imgui', menu,imgui.WindowFlags.NoCollapse) --Título da janela, NoCollapse impede minimizar
 
        imgui.Text("Botoes") --Texto simples na janela
        imgui.Separator() --Linha horizontal separadora
 
        imgui.Checkbox("CheckBox 1",checked_test) --Checkbox que pode marcar/desmarcar
        imgui.Checkbox("CheckBox 2",checked_test_2) --Segundo checkbox
 
        imgui.Separator() --Outra linha separadora
 
        imgui.RadioButton("Radio 1",checked_radio,1) --Radio button opção 1
        imgui.SameLine() --Próximo elemento na mesma linha
        imgui.RadioButton("Radio 2",checked_radio,2) --Radio button opção 2
        imgui.SameLine() --Próximo elemento na mesma linha
        imgui.RadioButton("Radio 3",checked_radio,3) --Radio button opção 3
 
        imgui.Separator() --Linha separadora
 
        imgui.Combo("Combo 1",combo_select,arr_str) --Lista suspensa com opções do arr_str
 
        imgui.Separator() --Linha separadora
 
        imgui.Spinner(10,3) --Círculo girando, raio 10 e espessura 3
 
        imgui.Separator() --Linha separadora
 
        imgui.BufferingBar(0.5,imgui.ImVec2(200,10),false) --Barra de progresso 50%, tamanho 200x10
 
        imgui.Separator() --Linha separadora
 
        imgui.ToggleButton("##1",toggle_status) --Botão liga/desliga, ##1 é ID oculto
        imgui.ToggleButton("##2",toggle_status_2) --Segundo toggle button
        imgui.ToggleButton("Toggle que faz nada",toggle_status_3) -- ToggleButton com texto
 
 
        imgui.End() --Finaliza o código do menu
    end
end

```

Você precisa de [imgui_addons](https://vk.com/s/v1/doc/FNBCrsWE2odgm-knFwmEull3GbTl2VNt-HOpOodcX6nO_RdcLSA) na sua pasta Lib
Contém Radio Button,Checkbox,Combo,Spinner,Hotkey e BufferingBar

# imgui.SameLine() : Deixa o próximo item na mesmo linha​

Existem Parâmetros que você pode colocar dentro dos parênteses,mas não citarei nesse tutorial

Observe o RadioButton logo abaixo
Como ficou :
<img width="409" height="305" alt="1757211609438" src="https://github.com/user-attachments/assets/c54747eb-9927-4a1d-a1b4-56a6ddeea8b2" />



### *** [ImGui Notification](https://vk.com/s/v1/doc/STZ8DybSD-zbjbLaVVFvrgfRJ0ryh0pSAftfHg8jE8cwt9y63yc)  :***: Pequenas janelas tipo notificação, em resumo (óbvio né)​
Coloque lib_imgui_notf na sua pasta Moonloader

**Comando principal:**

```lua
-- notify.addNotify(titulo , texto , tipo , posição do texto , duração)
-- Exemplo: notify.addNotify("Notificacao","\n Notificao sem cor",2,2,6)
```

***Exemplo básico completo :***

```lua
local imgui = require "imgui" --precisa do arquivo imgui

local notify = import 'lib_imgui_notf.lua' --importa biblioteca de notificações (obrigatório para notification)

local key = require "vkeys" -- precisa do arquivo vkeys para abrir ou fehcar o menu


local menu = imgui.ImBool(false) --Valor booleano false,janela começa fechada

function imgui.OnDrawFrame() --OnDrawFrame é nome obrigatório pois contém o conteúdo do menu
    if menu.v then --Se menu aberto
        imgui.SetNextWindowSize(imgui.ImVec2(400, 300), imgui.Cond.FirstUseEver) --Tamanho inicial 400x300, Cond.FirstUseEver permite fechar com X
        imgui.Begin('Menu Notificacao', menu, imgui.WindowFlags.NoCollapse) --Título da janela, NoCollapse impede minimizar
 
        imgui.Text("Botao logo abaixo") --Texto simples na janela
 
        if imgui.Button("Aperte me") then --Botão que quando clicado executa o código dentro
            notify.addNotify("Notificacao","\n Notificao sem cor",2,2,6) --Cria notificação sem cor
        end
 
        if imgui.Button("Notificacao com cor ") then --Segundo botão para notificação colorida
            notify.addNotify("{FF0000}Notificacao","\n {FF99AA}Notificao {FFFF00}com {FF00FF}cor",2,2,6) --Notificação com cores hexadecimais
        end
 
        imgui.End() --Finaliza o código do menu
    end
end

function main()
    while true do --Loop infinito
        wait(0) --Espera 0 segundos
        if wasKeyPressed(key.VK_F3) then --Se F3 for apertado, menu abre ou fecha
            menu.v = not menu.v --.v pega o valor booleano da variável menu
        end
        imgui.Process = menu.v --O Menu será processado enquanto menu for verdadeiro
    end
end
```

**Usando cores em Hexadecimais, Sua notificação fica mais bonita (Você pode usar cores Hex no seu Menu também)**

<img width="411" height="307" alt="1757239289739" src="https://github.com/user-attachments/assets/8f17ce0a-9c3d-4cfd-a376-2e3a2bc7de94" />
Notifcação 👉
<img width="263" height="152" alt="1757239332973" src="https://github.com/user-attachments/assets/7016314b-410a-4a44-89a6-3de848940f2e" />


***Use quebra de linhas (\\n) para deixar a mensagem encima ou embaixo***

-----

### ***Flags de Janela (WindowFlags)***

#### ***Por quê usei `imgui.WindowFlags.NoCollapse` em `imgui.Begin('Menu Notificacao', menu, imgui.WindowFlags.NoCollapse)` ?***

Isso de chama 'flags', condições que você pode colocar em seu menu, por exemplo, não deixar ele ser redimensionável, sem Scroll, sem título, entre outros.

**Controle Básico da Janela**

```
imgui.WindowFlags.NoTitleBar     -- Remove o título da janela
imgui.WindowFlags.NoResize       -- Não deixa redimensionar
imgui.WindowFlags.NoMove         -- Não deixa mover a janela
imgui.WindowFlags.NoCollapse     -- Remove a setinha de minimizar
```

**Tamanho e Rolagem**

```
imgui.WindowFlags.AlwaysAutoResize        -- Ajusta sozinho ao conteúdo
imgui.WindowFlags.NoScrollbar             -- Remove barra de rolagem
imgui.WindowFlags.NoScrollWithMouse       -- Não rola com a rodinha do mouse
imgui.WindowFlags.AlwaysVerticalScrollbar -- Sempre mostra rolagem vertical
```

**Visual e Aparência**

```
imgui.WindowFlags.NoBackground      -- Janela transparente (sem fundo)
imgui.WindowFlags.MenuBar           -- Adiciona barra de menu no topo
```

**Configurações e Foco**

```
imgui.WindowFlags.NoSavedSettings        -- Não salva posição/tamanho
imgui.WindowFlags.NoFocusOnAppearing      -- Não foca quando abre
imgui.WindowFlags.NoBringToFrontOnFocus   -- Não vem pra frente ao clicar
```

**Exemplo Prático (HUD):**

```lua
-- Janela de HUD fixa (não move, não redimensiona, sem título)
imgui.Begin("Meu Menu", state,
    imgui.WindowFlags.NoTitleBar,
    imgui.WindowFlags.NoMove,
    imgui.WindowFlags.NoResize,
    imgui.WindowFlags.AlwaysAutoResize
)
```

### **💭 Dica: Use vírgulas para separar as flags, não o sinal de +**

-----

### ***[Fork Awesome (Ícones Font Awesome v5)](https://www.blast.hk/threads/156617/)***

#### ***Precisa de [forkawesome-webfont.ttf](https://github.com/ForkAwesome/Fork-Awesome/blob/master/fonts/forkawesome-webfont.ttf)***

***Verifique como é o ícone ou procurar um em [Icones Fork](https://www.google.com/search?q=https://forkaweso.me/Fork-Awesome/icons/%23new)***

**Exemplo de um menu com Fork Awesome (Meu Projeto Atual) :**
<img width="704" height="535" alt="1757240561961" src="https://github.com/user-attachments/assets/aa6a4f7e-82e2-4bfc-b47c-91b9f4bb6a8c" />


#### ***Como usar :***

***Você usará `fa.SEU_ICONE_AQUI` para colocar os ícones.***

**Onde pego os nomes dos ícones?**
No arquivo `fork.lua` você verá várias linhas como essa:

<img width="333" height="166" alt="1757242019642" src="https://github.com/user-attachments/assets/f5200a44-501f-4922-a999-758ed248c03e" />


\*\*\*Você Irá pegar o nome do icone que está dentro das aspas (Obviamente) e logo em seguida usar `fa.ICONE_COPIADO ..`

Obrigatório usar '..' (concatenação) antes de texto, ou deixar ele sem concatenar (Fica só o ícone se não tiver texto). Recomendo usar dois espaços antes do texto, para organizar.\*\*\*

***Exemplo :***

```lua
imgui.Button(fa.ICON_SEARCH.."  Lupa")
```

**Obrigatório colocar no seu codigo\! 👇**
Este código deve ser colocado no seu script principal para que a fonte dos ícones seja carregada.

```lua
local fa = require 'fork' --fork faIcons
local fa_glyph_ranges = imgui.ImGlyphRanges({ fa.min_range, fa.max_range })
local fa_font = nil


function imgui.BeforeDrawFrame()
    if fa_font == nil then
        local font_config = imgui.ImFontConfig()
        font_config.MergeMode = true
        fa_font = imgui.GetIO().Fonts:AddFontFromFileTTF('moonloader/resource/fonts/fontawesome-webfont.ttf', 14.0, font_config, fa_glyph_ranges)
    end
end
 
-- Função de ajuda para colorir texto com cores hexadecimais (TextColoredRGB)
function imgui.TextColoredRGB(text, render_text)
    local max_float = imgui.GetWindowWidth()
    local style = imgui.GetStyle()
    local colors = style.Colors
    local ImVec4 = imgui.ImVec4

    local explode_argb = function(argb)
        local a = bit.band(bit.rshift(argb, 24), 0xFF)
        local r = bit.band(bit.rshift(argb, 16), 0xFF)
        local g = bit.band(bit.rshift(argb, 8), 0xFF)
        local b = bit.band(argb, 0xFF)
        return a, r, g, b
    end

    local getcolor = function(color)
        if color:sub(1, 6):upper() == 'SSSSSS' then
            local r, g, b = colors[1].x, colors[1].y, colors[1].z
            local a = tonumber(color:sub(7, 8), 16) or colors[1].w * 255
            return ImVec4(r, g, b, a / 255)
        else
            local a, r, g, b = explode_argb(tonumber(color:sub(1, 8), 16))
            if not a then
                a, r, g, b = 255, 255, 255, 255
            end
            return ImVec4(r / 255, g / 255, b / 255, a / 255)
        end
    end
    
    local lines = { }
    local text_tokens = text:gmatch('{[^}]+}[^{]+')
    local current_x = 0
    local width_space = imgui.CalcTextSize(" "):GetX()

    imgui.PushID(render_text or text)
    if not render_text then
        render_text = text
    end

    for color_token, text_token in render_text:gmatch('({[^}]+})([^{]+)') do
        local color = getcolor(color_token:sub(2, -2))
        local size = imgui.CalcTextSize(text_token)

        if size.x + current_x > max_float then
            current_x = 0
        end

        imgui.SameLine(current_x > 0 and current_x or nil)
        current_x = current_x + size.x + width_space
        imgui.TextColored(color, text_token)
    end
    imgui.PopID()
end
```

### Certifique-se de ter colocado `[forkawesome-webfont.ttf](https://github.com/ForkAwesome/Fork-Awesome/blob/master/fonts/forkawesome-webfont.ttf)` que você baixou em `moonloader/resource/fonts/`\!\!\!

Exemplo : <img width="409" height="312" alt="1757242675973" src="https://github.com/user-attachments/assets/cefe8753-d8ba-45dd-a575-54e821b25af3" />


### **Início da CollapsingHeader (Abas) e Cabeçalho Recolhível:**

#### **Cabeçalho em Colapso**

```lua
if imgui.CollapsingHeader("Collapsing Header Teste") then
        -- Seu Conteúdo/Código. Exemplo :
     imgui.Button("Clique me")
    end
```

Viu? Não é difícil.

#### **Exemplo:**
<img width="365" height="158" alt="1757248823108" src="https://github.com/user-attachments/assets/0af69280-fb22-453b-b9e0-567b9b5dfd56" />



### **BeginChild:**

```lua
-- Variável que controla qual aba está sendo exibida
-- Começa como 1 (ou seja, primeira aba)
local tab = 1
-- Campo de texto (até 256 caracteres)
local texto_input = imgui.ImBuffer(256)
-- Número decimal (float), começa com 5.5
local numero_float = imgui.ImFloat(5.5)
-- Número inteiro (int), começa com 25
local slider_int = imgui.ImInt(25)
-- Número decimal (float), começa com 2.5
local slider_float = imgui.ImFloat(2.5)
-- Caixa de seleção (checkbox), começa desmarcada (false)
local checkbox_teste = imgui.ImBool(false)

        -- CHILD ESQUERDO: Botões para escolher as abas
 
        -- "BeginChild" cria uma área separada dentro da janela
        -- Aqui criamos o painel da esquerda, que funciona como menu lateral
        -- Parâmetros: nome, tamanho (largura 150px, altura automática), borda (true)
        imgui.BeginChild("abas", imgui.ImVec2(150, 0), true)

            -- Cada botão altera a variável "tab"
            -- Assim conseguimos trocar o conteúdo exibido no painel da direita

            -- Botão da primeira aba
            if imgui.Button("Aba Collapse", imgui.ImVec2(135, 40)) then
                tab = 1 -- Vai para aba 1
            end

            -- Botão da segunda aba
            if imgui.Button("Aba Elementos", imgui.ImVec2(135, 40)) then
                tab = 2 -- Vai para aba 2
            end

            -- Botão da terceira aba
            if imgui.Button("Aba Vazia", imgui.ImVec2(135, 40)) then
                tab = 3 -- Vai para aba 3
            end

        -- Fecha o painel da esquerda
        imgui.EndChild()

        -- "SameLine" faz com que o próximo elemento fique na mesma linha
        -- Isso coloca o painel da direita (conteúdo) ao lado do da esquerda
        imgui.SameLine()

 
        -- CHILD DIREITO: Conteúdo da aba selecionada
 
        -- Esse painel mostra o que pertence à aba escolhida
        imgui.BeginChild("conteudo", imgui.ImVec2(0, 0), true)
            -- Verifica qual aba está ativa e chama a função correspondente
            if tab == 1 then
                renderAbaCollapse()   -- Mostra a aba 1
            elseif tab == 2 then
                renderAbaElementos()  -- Mostra a aba 2
            elseif tab == 3 then
                renderAbaVazia()      -- Mostra a aba 3
            end
        -- Fecha o painel de conteúdo
        imgui.EndChild()

        -- Fecha a janela principal do ImGui
        imgui.End()
    end
end

-- Conteúdo da Aba 1 (CollapseHeader)
function renderAbaCollapse()
    -- Texto fixo no topo da aba
    imgui.Text("Exemplo de CollapsingHeader")
    -- Linha separadora
    imgui.Separator()

    -- Primeiro CollapseHeader
    -- Cria uma seção que pode ser aberta e fechada clicando na setinha
    if imgui.CollapsingHeader("Seção de Informações") then
        -- Se a seção estiver aberta, esses textos aparecem
        imgui.Text("Essa seção pode ser expandida ou recolhida.")
        imgui.Text("Clique na setinha ao lado do título.")
    end

    -- Segundo CollapseHeader
    if imgui.CollapsingHeader("Configurações Avançadas") then
        -- Dentro da seção, criamos um checkbox
        imgui.Checkbox("Ativar opção", checkbox_teste)
        imgui.Text("Útil para esconder opções avançadas.")
    end
end

-- Conteúdo da Aba 2 (Elementos básicos)
function renderAbaElementos()
    -- Texto inicial da aba
    imgui.Text("Elementos básicos do ImGui")
    imgui.Separator()

    -- Caixa de texto para o jogador digitar
    imgui.InputText("Digite algo:", texto_input)

    -- Campo para números decimais
    imgui.InputFloat("Número decimal:", numero_float)

    -- Slider para número inteiro (0 até 100)
    imgui.SliderInt("Slider inteiro:", slider_int, 0, 100)

    -- Slider para número decimal (0.0 até 10.0)
    imgui.SliderFloat("Slider decimal:", slider_float, 0.0, 10.0)

    -- Botão que envia uma mensagem no chat quando clicado
    if imgui.Button("Clique aqui") then
        sampAddChatMessage("Você clicou no botão!", -1)
    end
end

-- Conteúdo da Aba 3 (Aba vazia)
function renderAbaVazia()
    -- Apenas um texto simples
    imgui.Text("Uma aba sem nada")
end
```

Vou dar exemplos com fotos:

#### **Uma Aba sem nada:**

<img width="321" height="178" alt="1757247772871" src="https://github.com/user-attachments/assets/e7539c59-5644-4399-9407-c0788d2effde" />


#### **Uma Aba com CollapsingHeader e com conteúdo dentro dela:**

<img width="504" height="260" alt="1757247907210" src="https://github.com/user-attachments/assets/d43743e0-a071-4bf2-b946-d8bc7b070130" />


#### **Uma Aba com conteúdo apenas, sem CollapsingHeader:**

<img width="559" height="223" alt="1757248063426" src="https://github.com/user-attachments/assets/daa91950-8e24-43ac-a074-401fe17330c0" />


-----

### **Colocar Imagens em seu Menu ImGui:**

Primeiro tenha a imagem no diretório da moonloader ou guardada dentro de uma pasta da moonloader para colocar o caminho no `CreateTextureFromFile`.

#### **Como usar? Aqui vai um exemplo:**

```lua
local imagens = {
    foto = imgui.CreateTextureFromFile("moonloader/image/bode.png")}
imgui.Image(imagens.foto, imgui.ImVec2(100, 70)) -- 100 largura | 70 altura
```

#### **Ou apenas:**

```lua
local images = imgui.CreateTextureFromFile("moonloader/image/bode.png")
imgui.Image(images, imgui.ImVec2(100, 70)) -- 100 largura | 70 altura
```

**Certifique-se de ter a imagem no caminho correto com extensão correta.**

#### **Exemplo Real:**

```lua
local imgui = require "imgui"
local key = require "vkeys"
local menu = imgui.ImBool(false)
local images = imgui.CreateTextureFromFile("moonloader/image/bode.png") -- Pega a imagem que está nesse caminho

function imgui.OnDrawFrame()
 
    if menu.v then
        imgui.SetNextWindowSize(imgui.ImVec2(200, 200), imgui.Cond.FirstUseEver)
        imgui.Begin("Menu Imagem", menu, imgui.WindowFlags.NoCollapse)
         imgui.Text("Imagem de um bode logo abaixo")
         -- Aqui é um exemplo de onde você pode botar sua imagem
 
         imgui.Image(images, imgui.ImVec2(100, 100)) -- 100 largura | 100 altura
 
 
        imgui.End()
    end
end

function main()
    while true do
        wait(0) -- Espera 0ms (mantém o loop ativo sem travar o jogo)

        -- Detecta se o jogador apertou a tecla P
        if wasKeyPressed(key.VK_P) then
            -- Alterna entre abrir/fechar o menu
            menu.v = not menu.v
        end

        -- ImGui só processa quando o menu está aberto
        imgui.Process = menu.v
    end
end
```

#### **Exemplo da foto no Menu:**
<img width="222" height="173" alt="1757290821101" src="https://github.com/user-attachments/assets/69782ff0-58fe-4de1-8d88-41a5da9e679a" />


-----

### **Como trocar a cor do Menu ImGui?**

Particularmente, sou péssimo para explicar isso.

```lua
-- Como deixar seu menu ImGui bonito no SAMP
-- Cole esse codigo antes de criar suas janelas
-- Pega as configuracoes do menu
local style = imgui.GetStyle()
local colors = style.Colors
local clr = imgui.Col
local ImVec4 = imgui.ImVec4

-- Deixa as bordas arredondadas (bonito)
style.WindowRounding = 8.0              -- janela principal
style.ChildWindowRounding = 6.0         -- janelas pequenas
style.FrameRounding = 4.0               -- botoes e caixas
style.GrabRounding = 4.0                -- sliders
style.ScrollbarRounding = 9             -- barra de rolagem

-- Posicao e espacamento
style.WindowTitleAlign = imgui.ImVec2(0.5, 0.5)    -- titulo no centro
style.ItemSpacing = imgui.ImVec2(8, 6)              -- espaco entre botoes
style.ItemInnerSpacing = imgui.ImVec2(6, 4)         -- espaco dentro dos botoes
style.ScrollbarSize = 14.0                          -- tamanho da barra de rolagem
style.GrabMinSize = 12.0                            -- tamanho dos puxadores

-- CORES DO MENU (tema escuro com vermelho)
-- ImVec4(vermelho, verde, azul, transparencia) - todos de 0 a 1

-- Fundo das janelas
colors[clr.WindowBg] = ImVec4(0.08, 0.08, 0.10, 0.95)      -- fundo da janela (bem escuro)
colors[clr.ChildWindowBg] = ImVec4(0.10, 0.10, 0.12, 1.00) -- fundo das abas
colors[clr.PopupBg] = ImVec4(0.12, 0.12, 0.14, 0.98)       -- fundo dos menus

-- Barra do titulo (em cima da janela)
colors[clr.TitleBg] = ImVec4(0.18, 0.05, 0.05, 1.00)       -- titulo normal
colors[clr.TitleBgActive] = ImVec4(0.40, 0.10, 0.10, 1.00) -- titulo quando clica na janela

-- Cor dos textos
colors[clr.Text] = ImVec4(1.00, 1.00, 1.00, 0.95)          -- texto normal (branco)
colors[clr.TextDisabled] = ImVec4(0.50, 0.50, 0.50, 0.70)  -- texto apagado (cinza)

-- Cores dos botoes (muda quando passa mouse e clica)
colors[clr.Button] = ImVec4(0.40, 0.12, 0.12, 1.00)        -- botao normal
colors[clr.ButtonHovered] = ImVec4(0.70, 0.20, 0.20, 1.00) -- botao com mouse em cima
colors[clr.ButtonActive] = ImVec4(0.90, 0.30, 0.30, 1.00)  -- botao sendo clicado

-- Caixas de texto (onde voce digita)
colors[clr.FrameBg] = ImVec4(0.16, 0.06, 0.06, 1.00)       -- caixa normal
colors[clr.FrameBgHovered] = ImVec4(0.30, 0.12, 0.12, 1.00)-- caixa com mouse em cima
colors[clr.FrameBgActive] = ImVec4(0.45, 0.15, 0.15, 1.00) -- caixa quando esta digitando

-- Menus que abrem e fecham
colors[clr.Header] = ImVec4(0.40, 0.12, 0.12, 1.00)        -- menu fechado
colors[clr.HeaderHovered] = ImVec4(0.70, 0.20, 0.20, 1.00) -- menu com mouse em cima
colors[clr.HeaderActive] = ImVec4(0.90, 0.30, 0.30, 1.00)  -- menu aberto

-- Checkbox (quadradinho de marcar)
colors[clr.CheckMark] = ImVec4(0.95, 0.35, 0.35, 1.00)     -- cor do "check" quando marcado

-- Sliders (barrinhas de ajustar valor)
colors[clr.SliderGrab] = ImVec4(0.85, 0.25, 0.25, 1.00)        -- bolinha do slider
colors[clr.SliderGrabActive] = ImVec4(1.00, 0.40, 0.40, 1.00)  -- bolinha quando arrasta

-- Barra de rolagem (quando tem muito conteudo)
colors[clr.ScrollbarBg] = ImVec4(0.10, 0.10, 0.10, 0.6)        -- fundo da barra
colors[clr.ScrollbarGrab] = ImVec4(0.30, 0.10, 0.10, 0.8)      -- parte que arrasta
colors[clr.ScrollbarGrabHovered] = ImVec4(0.50, 0.20, 0.20, 0.9)   -- parte que arrasta com mouse
colors[clr.ScrollbarGrabActive] = ImVec4(0.70, 0.25, 0.25, 1.0)    -- parte que arrasta clicando

-- Linhas que separam as coisas
colors[clr.Separator] = ImVec4(0.50, 0.20, 0.20, 0.60)         -- linha normal
colors[clr.SeparatorHovered] = ImVec4(0.70, 0.30, 0.30, 0.80)  -- linha com mouse
colors[clr.SeparatorActive] = ImVec4(0.90, 0.40, 0.40, 1.00)   -- linha clicando

-- COMO USAR:
-- 1. Cole esse codigo no inicio do seu script
-- 2. Depois crie suas janelas normalmente
-- 3. O menu vai ficar com esse visual automaticamente

-- COMO MUDAR AS CORES:
-- Os numeros sao: (vermelho, verde, azul, transparencia)
-- Exemplo para fazer azul: ImVec4(0.1, 0.2, 0.8, 1.0)
-- Exemplo para fazer verde: ImVec4(0.1, 0.8, 0.2, 1.0)
```

**Não entendeu Bosta Nenhuma? Normal.**

**Está com preguiça de trocar as cores ou deixar as coisas sem bordas? Eu estou aqui.**

**Só copiar e colar no seu código**

```lua
-- 🎨 SELETOR DE CORES SIMPLES - Só copiar e colar onde quiser
local cor_tema = imgui.ImInt(1)
-- 🔹 Função simples pra mudar as cores
local function mudarCores(cor)
    local style = imgui.GetStyle()
    local colors = style.Colors
    local clr = imgui.Col
    local ImVec4 = imgui.ImVec4
    --  Suavidade das bordas e alinhamento
    style.WindowRounding = 8.0
    style.ChildWindowRounding = 6.0
    style.FrameRounding = 4.0
    style.GrabRounding = 4.0
    style.ScrollbarRounding = 9
    style.WindowTitleAlign = imgui.ImVec2(0.5, 0.5)
    style.ItemSpacing = imgui.ImVec2(8, 6)
    style.ItemInnerSpacing = imgui.ImVec2(6, 4)
    style.ScrollbarSize = 14.0
    style.GrabMinSize = 12.0
 
    if cor == 1 then  -- Azul
        colors[clr.WindowBg]        = ImVec4(0.08, 0.08, 0.10, 0.95)
        colors[clr.ChildWindowBg]   = ImVec4(0.10, 0.10, 0.12, 1.00)
        colors[clr.PopupBg]         = ImVec4(0.12, 0.12, 0.14, 0.98)
        colors[clr.TitleBgActive] = ImVec4(0.12, 0.20, 0.28, 1.00)
        colors[clr.Button] = ImVec4(0.15, 0.25, 0.45, 1.00)
        colors[clr.ButtonHovered] = ImVec4(0.25, 0.40, 0.65, 1.00)
        colors[clr.ButtonActive] = ImVec4(0.35, 0.55, 0.85, 1.00)
        colors[clr.Header] = ImVec4(0.15, 0.25, 0.45, 0.80)
        colors[clr.HeaderHovered] = ImVec4(0.25, 0.40, 0.65, 1.00)
        colors[clr.HeaderActive] = ImVec4(0.35, 0.55, 0.85, 1.00)
        colors[clr.CheckMark] = ImVec4(0.40, 0.65, 0.90, 1.00)
 
 
 
    elseif cor == 2 then -- Vermelho
        colors[clr.WindowBg]        = ImVec4(0.08, 0.08, 0.10, 0.95)
        colors[clr.ChildWindowBg]   = ImVec4(0.10, 0.10, 0.12, 1.00)
        colors[clr.PopupBg]         = ImVec4(0.12, 0.12, 0.14, 0.98)
        colors[clr.TitleBgActive] = ImVec4(0.28, 0.12, 0.12, 1.00)
        colors[clr.Button] = ImVec4(0.45, 0.15, 0.15, 1.00)
        colors[clr.ButtonHovered] = ImVec4(0.65, 0.25, 0.25, 1.00)
        colors[clr.ButtonActive] = ImVec4(0.85, 0.35, 0.35, 1.00)
        colors[clr.Header] = ImVec4(0.45, 0.15, 0.15, 0.80)
        colors[clr.HeaderHovered] = ImVec4(0.65, 0.25, 0.25, 1.00)
        colors[clr.HeaderActive] = ImVec4(0.85, 0.35, 0.35, 1.00)
        colors[clr.CheckMark] = ImVec4(0.90, 0.40, 0.40, 1.00)
 
    elseif cor == 3 then -- Verde
        colors[clr.WindowBg]        = ImVec4(0.08, 0.08, 0.10, 0.95)
        colors[clr.ChildWindowBg]   = ImVec4(0.10, 0.10, 0.12, 1.00)
        colors[clr.PopupBg]         = ImVec4(0.12, 0.12, 0.14, 0.98)
        colors[clr.TitleBgActive] = ImVec4(0.12, 0.28, 0.16, 1.00)
        colors[clr.Button] = ImVec4(0.15, 0.45, 0.20, 1.00)
        colors[clr.ButtonHovered] = ImVec4(0.25, 0.65, 0.30, 1.00)
        colors[clr.ButtonActive] = ImVec4(0.35, 0.85, 0.45, 1.00)
        colors[clr.Header] = ImVec4(0.15, 0.45, 0.20, 0.80)
        colors[clr.HeaderHovered] = ImVec4(0.25, 0.65, 0.30, 1.00)
        colors[clr.HeaderActive] = ImVec4(0.35, 0.85, 0.45, 1.00)
        colors[clr.CheckMark] = ImVec4(0.40, 0.90, 0.50, 1.00)
 
    elseif cor == 4 then -- Roxo
        colors[clr.WindowBg]        = ImVec4(0.08, 0.08, 0.10, 0.95)
        colors[clr.ChildWindowBg]   = ImVec4(0.10, 0.10, 0.12, 1.00)
        colors[clr.PopupBg]         = ImVec4(0.12, 0.12, 0.14, 0.98)
        colors[clr.TitleBgActive] = ImVec4(0.28, 0.12, 0.28, 1.00)
        colors[clr.Button] = ImVec4(0.35, 0.15, 0.45, 1.00)
        colors[clr.ButtonHovered] = ImVec4(0.50, 0.25, 0.65, 1.00)
        colors[clr.ButtonActive] = ImVec4(0.70, 0.35, 0.85, 1.00)
        colors[clr.Header] = ImVec4(0.35, 0.15, 0.45, 0.80)
        colors[clr.HeaderHovered] = ImVec4(0.50, 0.25, 0.65, 1.00)
        colors[clr.HeaderActive] = ImVec4(0.70, 0.35, 0.85, 1.00)
        colors[clr.CheckMark] = ImVec4(0.80, 0.40, 0.90, 1.00)
 
    elseif cor == 5 then -- Laranja
        colors[clr.WindowBg]        = ImVec4(0.08, 0.08, 0.10, 0.95)
        colors[clr.ChildWindowBg]   = ImVec4(0.10, 0.10, 0.12, 1.00)
        colors[clr.PopupBg]         = ImVec4(0.12, 0.12, 0.14, 0.98)
        colors[clr.TitleBgActive] = ImVec4(0.28, 0.20, 0.08, 1.00)
        colors[clr.Button] = ImVec4(0.45, 0.25, 0.10, 1.00)
        colors[clr.ButtonHovered] = ImVec4(0.65, 0.40, 0.15, 1.00)
        colors[clr.ButtonActive] = ImVec4(0.85, 0.55, 0.25, 1.00)
        colors[clr.Header] = ImVec4(0.45, 0.25, 0.10, 0.80)
        colors[clr.HeaderHovered] = ImVec4(0.65, 0.40, 0.15, 1.00)
        colors[clr.HeaderActive] = ImVec4(0.85, 0.55, 0.25, 1.00)
        colors[clr.CheckMark] = ImVec4(0.90, 0.60, 0.30, 1.00)
    end
end

function escolhercor()
    -- CollapsingHeader com seletor (cole onde quiser no seu menu)
    if imgui.CollapsingHeader(" Cor do Menu") then
        -- Vermelho
        local red    = imgui.ImVec4(1.0, 0.0, 0.0, 1.0)
        -- Azul
        local blue   = imgui.ImVec4(0.0, 0.0, 1.0, 1.0)
        -- Roxo (mistura de vermelho + azul)
        local purple = imgui.ImVec4(0.5, 0.0, 0.5, 1.0)
        -- Verde
        local green  = imgui.ImVec4(0.0, 1.0, 0.0, 1.0)
        -- Laranja (mistura de vermelho + verde, mas menos verde)
        local orange = imgui.ImVec4(1.0, 0.5, 0.0, 1.0)

        if imgui.RadioButton(" Azul", cor_tema, 1) then
            mudarCores(1)
        end
 
        if imgui.RadioButton(" Vermelho", cor_tema, 2) then
            mudarCores(2)
        end
 
        if imgui.RadioButton(" Verde", cor_tema, 3) then
            mudarCores(3)
        end
 
        if imgui.RadioButton(" Roxo", cor_tema, 4) then
            mudarCores(4)
        end
 
        if imgui.RadioButton(" Laranja", cor_tema, 5) then
            mudarCores(5)
        end
    end
end
```

**Apenas Chame `escolhercor()` para renderizar o conteúdo dela.**

**Vai ficar só uma CollapsingHeader, então não choras.**

**Teste você mesmo.**

#### **Como Fica:**

<img width="187" height="153" alt="1757293803325" src="https://github.com/user-attachments/assets/8239abc5-beba-46ff-838f-6b9e0fa39dde" />

-----

### **Como fazer Popup no seu ImGui:**

```lua
    -- PASSO 1: Botão que abre popup
    if imgui.Button("Abrir Popup") then
        imgui.OpenPopup("MeuPopup")  -- Abre popup por nome dele
    end
 
    -- PASSO 2: Criar o popup
    if imgui.BeginPopup("MeuPopup") then -- Pegue o nome do seu Popup e use em OpenPopup
 
        imgui.Text("Conteúdo do popup")
        imgui.Separator()
 
        -- Elementos dentro do popup
        imgui.Checkbox("Checkbox", checkbox_test)
        imgui.SliderInt("Slider", slider_value, 0, 100)
 
        -- Botão para fechar (Opcional)
        if imgui.Button("Fechar") then
            imgui.CloseCurrentPopup()
        end
 
        imgui.EndPopup()  -- Fecha popup
    end
```

#### **Como fica:**

<img width="418" height="107" alt="Untitled2" src="https://github.com/user-attachments/assets/7249467c-4fa5-40de-a3a3-4dbc383c7963" />


-----

### **Como fazer ToolTip (Dica para seu mouse):**

```lua
    imgui.Button("Passe o mouse aqui")
  
        if imgui.IsItemHovered() then -- IsItemHovered = detecta se o mouse está em cima do último elemento
            imgui.BeginTooltip() -- Inicia a tooltip
            imgui.Text("Esta e uma dica util")
            imgui.Text("Aparece quando voce passa o mouse")
            imgui.Text("Pode ter varias linhas")
            imgui.EndTooltip() -- SEMPRE feche o que abriu
        end
```

#### **Como fica:**

<img width="345" height="82" alt="Untitled3" src="https://github.com/user-attachments/assets/315448b3-1b93-4a6d-af9d-479f01b022af" />

-----

Irei adicionar mais coisas depois...

# [Moonloader](https://www.mediafire.com/file/eq8pmzd8f18mmgo/moonloader.rar/file) com todos os recursos já prontos, é só baixar. <br>
# Russos/Gringos não vão entender bem o que escrevi aqui, tradutor só vai estragar de vez o tutorial 😅 <br>
# Créditos A **[TheChampGuess](https://vk.com/thechampguess)**, aprendi quase tudo de imgui com ele. <br>
# Dê sugestões do que colocar aqui\! 😄
