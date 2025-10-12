# 🎮 Tutorial ImGui Lua para SA-MP

<div align="center">

![ImGui Lua Banner](./assets/images/banner.png)

Um tutorial completo e em português sobre **ImGui Lua** para criar interfaces gráficas modernas em SA-MP com MoonLoader.

**Acesso Rápido:** [Documentação](#documentação) • [Exemplos](#exemplos-práticos) • [Instalação](#instalação) • [FAQ](#faq)

![License](https://img.shields.io/badge/License-MIT-green.svg)
![Language](https://img.shields.io/badge/Language-Lua-blue.svg)
![Platform](https://img.shields.io/badge/Platform-SA--MP-orange.svg)
![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)

**[⬆ Versão em HTML](./index.html) | [📖 Documentação Completa](./docs/README.md) | [🚀 Versão Online](https://seu-site.com)**

</div>

---

## 📑 Sumário

1. [Sobre o Projeto](#sobre-o-projeto)
2. [Características](#características)
3. [Pré-requisitos](#pré-requisitos)
4. [Instalação Rápida](#instalação-rápida)
5. [Primeiros Passos](#primeiros-passos)
6. [Documentação](#documentação)
7. [Exemplos Práticos](#exemplos-práticos)
8. [Recursos Avançados](#recursos-avançados)
9. [Troubleshooting](#troubleshooting)
10. [Contribuições](#contribuições)
11. [FAQ](#faq)
12. [Créditos](#créditos)

---

## Sobre o Projeto

Este repositório é um **guia completo e prático** para programadores iniciantes e intermediários que desejam aprender a criar interfaces gráficas modernas usando **ImGui Lua** em **SA-MP**.

O projeto inclui:
- Tutorial estruturado em 10 níveis de dificuldade
- 15+ exemplos prontos para usar
- Documentação com imagens
- Scripts reutilizáveis
- Comunidade ativa

---

## Características

- ✅ **Tutorial Passo a Passo** - Do zero ao avançado
- ✅ **Exemplos Funcionais** - Copie e use imediatamente
- ✅ **Documentação em Português** - Claro e completo
- ✅ **Sem Dependências Externas** - Apenas Lua puro
- ✅ **Código Comentado** - Fácil de aprender
- ✅ **Recursos Avançados** - Temas, efeitos, animações
- ✅ **Totalmente Gratuito** - Licença MIT
- ✅ **Comunidade Ativa** - Discord e GitHub

---

## Pré-requisitos

### Sistema Operacional

- Windows 7 ou superior
- Processador: Qualquer um
- RAM: 512MB mínimo

### Software Necessário

| Software | Versão | Obrigatório | Download |
|----------|--------|-----------|----------|
| SA-MP | 0.3.7 | ✅ Sim | [sa-mp.com](https://sa-mp.com) |
| MoonLoader | 1.0+ | ✅ Sim | [BlastHack](https://www.blast.hk) |
| ASI Loader | Qualquer | ✅ Sim | [GitHub](https://github.com/ThirteenAG/Ultimate-ASI-Loader) |
| ImGui Lua | Último | ✅ Sim | [GitHub](https://github.com/THE-FYP/ImGui-Lua) |
| Lua | 5.1+ | ✅ Sim | [lua.org](https://www.lua.org) |
| Notepad++ | Qualquer | ❌ Não* | [notepad-plus-plus.org](https://notepad-plus-plus.org) |
| Sublime Text | Qualquer | ❌ Não* | [sublimetext.com](https://www.sublimetext.com) |

*IDE recomendada para melhor experiência

---

## Instalação Rápida

### Método 1: Instalação Automática (Recomendado)

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/imgui-lua-tutorial.git
cd imgui-lua-tutorial

# Execute o instalador
# Windows
instalador.bat

# Linux/Mac
chmod +x instalador.sh
./instalador.sh
```

### Método 2: Instalação Manual

**Passo 1:** Instale os pré-requisitos
```bash
# Baixe SA-MP 0.3.7
# Instale normalmente

# Baixe e instale MoonLoader
# Coloque na pasta raiz de SA-MP
```

**Passo 2:** Instale as bibliotecas
```bash
# Copie para sa-mp/moonloader/lib/
- imgui.lua
- imgui_addons.lua
- vkeys.lua
```

**Passo 3:** Clone este repositório
```bash
git clone https://github.com/seu-usuario/imgui-lua-tutorial.git
cp -r imgui-lua-tutorial/examples/* sa-mp/moonloader/
```

**Passo 4:** Verifique a instalação
```lua
-- Abra sa-mp/moonloader/test.lua
local imgui = require "imgui"
print("ImGui carregado com sucesso!")
```

---

## Primeiros Passos

### Seu Primeiro Script em 30 Segundos

1. Crie `sa-mp/moonloader/hello.lua`:

```lua
script_name("Primeiro Menu")

local imgui = require "imgui"
local key = require "vkeys"

local menu = imgui.ImBool(false)

function imgui.OnDrawFrame()
  if menu.v then
    imgui.Begin('Olá Mundo!', menu)
    imgui.Text('Bem-vindo ao ImGui!')
    imgui.End()
  end
end

function main()
  while true do
    wait(0)
    if wasKeyPressed(key.VK_F2) then
      menu.v = not menu.v
    end
    imgui.Process = menu.v
  end
end
```

2. Abra SA-MP e pressione **F2**
3. Pronto! Seu menu apareceu!

---

## Documentação

### Estrutura do Tutorial

O tutorial está dividido em **5 seções principais**:

#### 🟢 Nível 1: Conceitos Básicos
- Criar seu primeiro menu
- Estrutura básica de um script ImGui
- Variáveis principais (ImBool, ImInt, ImFloat, ImBuffer)

[👉 Ir para Nível 1](./docs/nivel-1-basico.md)

#### 🟡 Nível 2: Elementos Essenciais
- Buttons
- Checkboxes
- Sliders
- Input Text
- Radio Buttons

[👉 Ir para Nível 2](./docs/nivel-2-elementos.md)

#### 🟠 Nível 3: Layouts Avançados
- Combo Box
- Popup Windows
- Abas (Tabs)
- BeginChild
- Organização visual

[👉 Ir para Nível 3](./docs/nivel-3-layouts.md)

#### 🔴 Nível 4: Customização e Efeitos
- Cores personalizadas (ImVec4)
- Temas completos
- Animações
- Ícones e imagens
- WindowFlags

[👉 Ir para Nível 4](./docs/nivel-4-customizacao.md)

#### 🟣 Nível 5: Projeto Completo
- Integração com SA-MP
- Salvar/carregar configurações
- Performance e otimização
- Debug e troubleshooting

[👉 Ir para Nível 5](./docs/nivel-5-avancado.md)

---

## Elementos Principais com Imagens

### 1. Button (Botão)

![Button Demo](./assets/images/elementos/button.png)

```lua
if imgui.Button("Clique aqui", imgui.ImVec2(200, 40)) then
  sampAddChatMessage("Botão clicado!", -1)
end
```

**Características:**
- Tamanho customizável com ImVec2
- Retorna `true` quando clicado
- Pode ter cor personalizada

---

### 2. Checkbox

![Checkbox Demo](./assets/images/elementos/checkbox.png)

```lua
local opcao = imgui.ImBool(false)
imgui.Checkbox("Ativar modo", opcao)
print(opcao.v) -- true ou false
```

**Características:**
- Armazena valores booleanos
- Sempre visível
- Rótulo editável

---

### 3. Slider Integer

![Slider Int Demo](./assets/images/elementos/slider-int.png)

```lua
local valor = imgui.ImInt(50)
imgui.SliderInt("Velocidade", valor, 0, 100)
print(valor.v) -- Número entre 0 e 100
```

**Características:**
- Valores inteiros (0, 1, 2, etc)
- Range customizável
- Exibe o valor atual

---

### 4. Slider Float

![Slider Float Demo](./assets/images/elementos/slider-float.png)

```lua
local velocidade = imgui.ImFloat(0.5)
imgui.SliderFloat("Opacidade", velocidade, 0.0, 1.0)
print(velocidade.v) -- Decimal (0.5, 0.75, etc)
```

**Características:**
- Valores decimais (0.0 a 1.0)
- Precisão ajustável
- Ideal para opacidade e efeitos

---

### 5. Input Text

![Input Text Demo](./assets/images/elementos/input-text.png)

```lua
local texto = imgui.ImBuffer(256)
imgui.InputText("Digite seu nome", texto)
print(texto.v) -- "John Doe"
```

**Características:**
- Até 256 caracteres
- Teclado integrado
- Placeholder opcional

---

### 6. Radio Button

![Radio Button Demo](./assets/images/elementos/radio-button.png)

```lua
local opcao = imgui.ImInt(1)
imgui.RadioButton("Opção 1", opcao, 1)
imgui.SameLine()
imgui.RadioButton("Opção 2", opcao, 2)
imgui.SameLine()
imgui.RadioButton("Opção 3", opcao, 3)
```

**Características:**
- Apenas uma opção pode ser selecionada
- Valores numéricos
- Alinhamento flexível

---

### 7. Combo Box

![Combo Demo](./assets/images/elementos/combo.png)

```lua
local items = {"Vermelho", "Verde", "Azul"}
local selected = imgui.ImInt(0)
imgui.Combo("Cor", selected, items)
```

**Características:**
- Lista suspensa
- Itens personalizáveis
- Índice baseado em 0

---

### 8. Popup

![Popup Demo](./assets/images/elementos/popup.png)

```lua
if imgui.Button("Abrir") then
  imgui.OpenPopup("popup_id")
end

if imgui.BeginPopup("popup_id") then
  imgui.Text("Conteúdo do popup")
  if imgui.Button("Fechar") then
    imgui.CloseCurrentPopup()
  end
  imgui.EndPopup()
end
```

**Características:**
- Janelas flutuantes
- Modal ou não-modal
- Fechamento automático

---

## Exemplos Práticos

### Exemplo 1: Menu de Admin Simples

```lua
script_name("Admin Menu")
local imgui = require "imgui"
local key = require "vkeys"

local menu = imgui.ImBool(false)
local playerid = imgui.ImInt(0)

function imgui.OnDrawFrame()
  if menu.v then
    imgui.SetNextWindowSize(imgui.ImVec2(300, 250), imgui.Cond.FirstUseEver)
    imgui.Begin("Painel Admin", menu)
    
    imgui.Text("ID do Jogador:")
    imgui.InputInt("##playerid", playerid)
    
    if imgui.Button("Kick", imgui.ImVec2(130, 40)) then
      sampSendChat("/kick " .. playerid.v)
    end
    imgui.SameLine()
    if imgui.Button("Ban", imgui.ImVec2(130, 40)) then
      sampSendChat("/ban " .. playerid.v)
    end
    
    imgui.End()
  end
end

function main()
  while true do
    wait(0)
    if wasKeyPressed(key.VK_F5) then
      menu.v = not menu.v
    end
    imgui.Process = menu.v
  end
end
```

📁 Arquivo completo: `examples/01_admin_menu.lua`

---

### Exemplo 2: Menu de Configurações

```lua
script_name("Settings Menu")
local imgui = require "imgui"

local menu = imgui.ImBool(false)
local tab = imgui.ImInt(1)

-- Configurações
local config = {
  volume = imgui.ImFloat(0.8),
  qualidade = imgui.ImInt(2),
  idioma = imgui.ImInt(0),
  efeitos = imgui.ImBool(true),
}

function imgui.OnDrawFrame()
  if menu.v then
    imgui.SetNextWindowSize(imgui.ImVec2(400, 350), imgui.Cond.FirstUseEver)
    imgui.Begin("Configurações", menu)
    
    -- Abas
    if imgui.Button("Áudio", imgui.ImVec2(95, 35)) then tab.v = 1 end
    imgui.SameLine()
    if imgui.Button("Gráficos", imgui.ImVec2(95, 35)) then tab.v = 2 end
    imgui.SameLine()
    if imgui.Button("Idioma", imgui.ImVec2(95, 35)) then tab.v = 3 end
    
    imgui.Separator()
    
    if tab.v == 1 then
      imgui.Text("Volume:")
      imgui.SliderFloat("##volume", config.volume, 0.0, 1.0)
    elseif tab.v == 2 then
      imgui.Text("Qualidade:")
      local quality = {"Baixa", "Média", "Alta"}
      imgui.Combo("##quality", config.qualidade, quality)
      imgui.Checkbox("Efeitos especiais", config.efeitos)
    elseif tab.v == 3 then
      local langs = {"Português", "English", "Español"}
      imgui.Combo("Idioma##lang", config.idioma, langs)
    end
    
    imgui.End()
  end
end

function main()
  while true do
    wait(0)
    if wasKeyPressed(VK_F6) then
      menu.v = not menu.v
    end
    imgui.Process = menu.v
  end
end
```

📁 Arquivo completo: `examples/02_settings_menu.lua`

---

### Exemplo 3: Menu com Abas Completo

[📁 Ver arquivo completo](./examples/03_full_menu_tabs.lua)

---

## Recursos Avançados

### Customização de Cores

![Colors Demo](./assets/images/recursos/colors.png)

```lua
local style = imgui.GetStyle()
local colors = style.Colors
local clr = imgui.Col

-- Tema escuro personalizado
colors[clr.WindowBg] = imgui.ImVec4(0.1, 0.1, 0.12, 0.95)
colors[clr.Button] = imgui.ImVec4(0.4, 0.1, 0.1, 1.0)
colors[clr.ButtonHovered] = imgui.ImVec4(0.7, 0.2, 0.2, 1.0)
colors[clr.ButtonActive] = imgui.ImVec4(0.9, 0.3, 0.3, 1.0)
colors[clr.Text] = imgui.ImVec4(1.0, 1.0, 1.0, 0.95)

-- Bordas arredondadas
style.WindowRounding = 8.0
style.FrameRounding = 4.0
```

**Cores disponíveis:**
- WindowBg, ChildBg, PopupBg
- Button, ButtonHovered, ButtonActive
- Text, TextDisabled
- Border, BorderShadow

---

### Animações e Efeitos

```lua
local animation_time = 0

function imgui.OnDrawFrame()
  imgui.Begin("Animações")
  
  -- Pulsação
  animation_time = (animation_time + 0.02) % 2
  local alpha = math.abs(math.sin(animation_time * 3.14))
  
  imgui.PushStyleColor(imgui.Col.Button, imgui.ImVec4(1, 0, 0, alpha))
  imgui.Button("Botão Pulsante", imgui.ImVec2(200, 40))
  imgui.PopStyleColor()
  
  imgui.End()
end
```

---

### Ícones e Imagens

```lua
-- Carregar imagem
local logo = imgui.CreateTextureFromFile("moonloader/image/logo.png")

function imgui.OnDrawFrame()
  imgui.Begin("Galeria")
  imgui.Image(logo, imgui.ImVec2(200, 150))
  imgui.End()
end
```

---

### WindowFlags Avançadas

```lua
imgui.Begin("Menu", menu,
  imgui.WindowFlags.NoTitleBar,      -- Remove barra de título
  imgui.WindowFlags.NoResize,         -- Não pode redimensionar
  imgui.WindowFlags.NoMove,           -- Não pode mover
  imgui.WindowFlags.NoCollapse,       -- Sem botão minimizar
  imgui.WindowFlags.AlwaysAutoResize, -- Ajusta ao conteúdo
  imgui.WindowFlags.NoScrollbar       -- Remove scrollbar
)
```

---

## Troubleshooting

### O menu não aparece

**Causa:** `imgui.Process` não está ativo

```lua
function main()
  while true do
    wait(0)
    imgui.Process = menu.v  -- ✅ Correto
    -- imgui.Process = true -- ❌ Errado (sempre ligado)
  end
end
```

---

### Erro: "imgui is nil"

**Causa:** ImGui não foi carregado

```lua
-- ❌ Errado
local imgui = "imgui"

-- ✅ Correto
local imgui = require "imgui"
```

---

### Cores ficam estranhas

**Causa:** Valores acima de 1.0 em ImVec4

```lua
-- ❌ Errado (valores de RGB padrão)
imgui.ImVec4(255, 0, 0, 255)

-- ✅ Correto (valores 0.0-1.0)
imgui.ImVec4(1.0, 0.0, 0.0, 1.0)
```

---

### Script trava o jogo

**Causa:** `main()` sem `wait(0)`

```lua
-- ❌ Errado
function main()
  while true do
    -- sem wait
  end
end

-- ✅ Correto
function main()
  while true do
    wait(0)
    -- seu código
  end
end
```

---

### Valores não são acessados

**Causa:** Esquecimento do `.v`

```lua
local checkbox = imgui.ImBool(false)

-- ❌ Errado
if checkbox then end

-- ✅ Correto
if checkbox.v then end
```

Para mais soluções, [consulte o guia de troubleshooting](./docs/troubleshooting.md)

---

## Estrutura de Diretórios

```
imgui-lua-tutorial/
│
├── 📄 README.md                      # Este arquivo
├── 📄 LICENSE                        # Licença MIT
├── 📄 CONTRIBUTING.md                # Guia de contribuição
├── 📄 .gitignore
├── 📄 index.html                     # Versão HTML do tutorial
│
├── 📁 docs/                          # Documentação
│   ├── README.md
│   ├── nivel-1-basico.md
│   ├── nivel-2-elementos.md
│   ├── nivel-3-layouts.md
│   ├── nivel-4-customizacao.md
│   ├── nivel-5-avancado.md
│   ├── api-reference.md
│   ├── troubleshooting.md
│   ├── faq.md
│   └── glossario.md
│
├── 📁 examples/                      # Exemplos prontos
│   ├── 01_hello_world.lua
│   ├── 02_admin_menu.lua
│   ├── 03_settings_menu.lua
│   ├── 04_full_menu_tabs.lua
│   ├── 05_colors_theme.lua
│   ├── 06_images_gallery.lua
│   ├── 07_animations.lua
│   ├── 08_notifications.lua
│   ├── 09_performance.lua
│   ├── 10_complete_game_menu.lua
│   ├── addons/
│   │   ├── toggle_button.lua
│   │   ├── spinner.lua
│   │   └── progress_bar.lua
│   └── templates/
│       ├── minimal.lua
│       ├── professional.lua
│       └── gaming.lua
│
├── 📁 assets/                        # Recursos
│   ├── images/
│   │   ├── banner.png
│   │   ├── logo.png
│   │   └── elementos/
│   │       ├── button.png
│   │       ├── checkbox.png
│   │       ├── slider-int.png
│   │       ├── slider-float.png
│   │       ├── input-text.png
│   │       ├── radio-button.png
│   │       ├── combo.png
│   │       └── popup.png
│   │
│   └── recursos/
│       ├── colors.png
│       ├── themes/
│       └── icons/
│
├── 📁 tools/                         # Ferramentas
│   ├── color-picker.lua
│   ├── code-generator.lua
│   ├── performance-monitor.lua
│   └── debug-helper.lua
│
└── 📁 scripts/                       # Scripts de automação
    ├── instalador.bat
    ├── instalador.sh
    └── setup.py
```

---

## Contribuições

Adoramos contribuições! Aqui estão formas de contribuir:

### 1. Reportar Bugs

[Abra uma issue](https://github.com/seu-usuario/imgui-lua-tutorial/issues/new?labels=bug)

Inclua:
- Descrição clara do problema
- Passos para reproduzir
- Seu sistema operacional
- Versões instaladas

### 2. Sugerir Melhorias

[Abra uma discussão](https://github.com/seu-usuario/imgui-lua-tutorial/discussions)

### 3. Contribuir com Código

```bash
# Fork o projeto
git clone https://github.com/seu-usuario/imgui-lua-tutorial.git
cd imgui-lua-tutorial

# Crie uma branch
git checkout -b feature/minha-feature

# Faça suas mudanças
git add .
git commit -m "Adiciona minha feature"

# Push
git push origin feature/minha-feature

# Abra um Pull Request
```

**Diretrizes:**
- Código bem comentado
- Siga o estilo existente
- Adicione testes quando possível
- Atualize documentação

---

## FAQ

### P: Preciso saber Lua antes?
**R:** Sim, o tutorial assume conhecimento básico de Lua. Recomendamos [este curso](https://www.youtube.com/watch?v=jMsCOS1b0eo).

### P: Funciona em Mac/Linux?
**R:** SA-MP é Windows-only, mas o código Lua funciona em qualquer plataforma.

### P: Posso usar em outros projetos?
**R:** Sim! A licença é MIT, totalmente gratuita.

### P: Como reportar um bug?
**R:** [Abra uma issue no GitHub](https://github.com/seu-usuario/imgui-lua-tutorial/issues)

### P: Qual é a performance?
**R:** ImGui é muito otimizado. Funciona bem em PCs de 2008+.

[Ver mais FAQs](./docs/faq.md)

---

## Performance e Otimização

### Dicas de Performance

1. **Use `##` para esconder labels desnecessários**
   ```lua
   imgui.Button("##1")  -- Sem overhead de texto
   ```

2. **Não crie texturas a cada frame**
   ```lua
   -- Cache de imagens
   local images = {}
   if not images.logo then
     images.logo = imgui.CreateTextureFromFile("path/logo.png")
   end
   ```

3. **Use `IsItemHovered()` com moderação**
   ```lua
   if imgui.Button("Test") then end
   if imgui.IsItemHovered() then end  -- Apenas se necessário
   ```

---

## Recursos Adicionais

### Links Úteis

- [ImGui Oficial (C++)](https://github.com/ocornut/imgui)
- [Documentação Lua](https://www.lua.org/docs.html)
- [SA-MP Wiki](https://wiki.sa-mp.com)
- [BlastHack Forum](https://www.blast.hk)
- [Community Discord](#discord)

### Ferramentas Recomendadas

| Ferramenta | Uso |
|-----------|-----|
| [Notepad++](https://notepad-plus-plus.org) | Editor com syntax highlighting |
| [LuaStudio](http://www.kdj.net/luastudio/) | IDE Lua completa |
| [ImGui Test Engine](https://github.com/ocornut/imgui_test_engine) | Testes para ImGui |

---

## Changelog

### v2.0.0 (Atual)
- ✨ Documentação completa
- ✨ 10+ exemplos
- ✨ Guias de performance
- 🐛 Correções várias

### v1.5.0
- ✨ Adicionar suporte a Windows 7
- ✨ Novos temas

### v1.0.0
- 🎉 Versão inicial

[Ver histórico completo](./CHANGELOG.md)

---

## Licença

Este projeto está sob licença **MIT** - você é livre para usar, modificar e distribuir.

```
MIT License

Copyright (c) 2024 TheChampGuess

Permissão é concedida para usar este software gratuitamente...
```

[📄 Ver licença completa](./LICENSE)

---

## Suporte e Comunidade

### Discord

[🎮 Junte-se ao nosso Discord](https://discord.gg/seu-servidor)

### Redes Sociais

- [Twitter](https://twitter.com/seu-usuario)
- [YouTube](https://youtube.com/seu-canal)
- [GitHub](https://github.com/seu-usuario)

### Contato

- Email: seu-email@exemplo.com
- Forum: [BlastHack](https://www.blast.hk)

---

## Créditos

### Criado por

**TheChampGuess** - [GitHub](https://github.com/seu-usuario) | [Email](mailto:seu-email@exemplo.com)

### Colaboradores

- [Colaborador 1](https://github.com)
- [Colaborador 2](https://github.com)
- [Comunidade SA-MP](https://sa-mp.com)

### Agradecimentos

- Comunidade BlastHack
- Desenvolvedores ImGui
- Comunidade SA-MP Brasil
- Todos os contribuidores

---

## Status do Projeto

- ✅ Documentação: 100%
- ✅ Exemplos: 10/10
- ✅ Testes: Em progresso
- ⏳ CI/CD: Planejado

---

<div align="center">

### Feito com ❤️ para a Comunidade SA-MP

**Se gostou, deixe uma ⭐ no repositório!**

[⬆ Voltar ao topo](#-tutorial-imgui-lua-para-sa-mp)

**Última atualização:** 2024 | **Mantido por:** TheChampGuess

</div>
