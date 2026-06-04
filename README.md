# Logitech G-Hub Recoil Script - Rainbow Six Siege

Este é um script de automação e compensação de recuo dinâmico desenvolvido em **Lua**, projetado especificamente para ser executado através do ecossistema de scripts do software **Logitech G-Hub**.

O script foi estruturado de forma inteligente para separar os operadores entre **Atacantes** e **Defensores**, além de incluir suporte a armas primárias e secundárias, otimizando a interface no console e permitindo uma troca ágil de posições durante as rodadas.

---

## 🚀 Funcionalidades

* **Separação por Lados (Ataque/Defesa):** O painel do console filtra dinamicamente e exibe apenas os operadores do lado atual, reduzindo a poluição visual.
* **Troca Rápida de Lado:** Atalho dedicado que pula instantaneamente do Ataque para a Defesa (e vice-versa), redefinindo a seleção diretamente para o operador inicial do lado (`Sledge` no ataque / `Smoke` na defesa).
* **Suporte a Duas Armas por Operador:** Cada operador possui tabelas de recuo independentes para a arma **Primária** e **Secundária**.
* **Interface Limpa e Scannable:** O layout do console foi simplificado para exibir apenas o lado atual, a arma selecionada, o status do script (`[ ON ]` / `[ OFF ]`) e a tabela de operadores disponíveis, marcando o selecionado com um `[✅]`.
* **Recuo Dinâmico por Estágios:** Sistema avançado baseado em tempo que altera o comportamento do mouse dependendo de há quantos milissegundos o gatilho está pressionado.

---

## 🎮 Controles e Atalhos

Para navegar pelos operadores, alternar armas e ligar/desligar as funções, utilize as seguintes combinações:

### 🔄 Seleção de Operadores (Dentro do Lado Atual)

* `Right CTRL` + `Botão Avançar do Mouse (MB5)`: Seleciona o **Próximo** operador da lista.
* `Right CTRL` + `Botão Voltar do Mouse (MB4)`: Seleciona o operador **Anterior** da lista.

### ⚙️ Sistema e Troca de Lados

* `Right ALT` + `Botão Avançar do Mouse (MB5)`: Liga / Desliga a execução do script.
* `Right ALT` + `Botão Voltar do Mouse (MB4)`: Altera entre **ATACANTES** ↔️ **DEFENSORES** (Pula direto para *Sledge* ou *Smoke* e reseta a arma atual para a Primária).

### 🔫 Troca de Armas (Primária ↔️ Secundária)

* `Click no Scroll do Mouse`: Alterna instantaneamente entre os perfis de recuo da arma **Primária `[P]` e **Secundária `[S]**`. O console do G-Hub atualiza o indicador em tempo real para que você saiba exatamente qual tabela de recuo está ativa.

---

## 🛠️ Como Funcionam os Parâmetros de Eixo?

Cada operador possui uma linha de configuração detalhada e duplicada para abranger as duas armas. A estrutura funciona como uma linha do tempo em milissegundos (`ms`).

Exemplo de estrutura interna:
`ops = { {n="Nome", p={...valores da arma primária...}, s={...valores da arma secundária...}} }`

### 📐 Entendendo as Variáveis / Configurando o recoil:

* **`r` (Recoil Inicial):** A força vertical padrão. Assim que você **segura** o botão direito do mouse (mira) e clica para atirar, o mouse é empurrado para baixo com essa intensidade constante para anular o coice inicial do jogo.
* **Eixo Horizontal (Esquerda / Direita):**
* `x1` e `x2`: Quantidade de pixels que o mouse se moverá horizontalmente. Valores **negativos** movem o mouse para a esquerda, valores **positivos** para a direita.
* `tm1` e `tm2`: O tempo de atraso (em milissegundos) que o script espera após o clique inicial para começar a aplicar as forças `x1` e `x2`, respectivamente.


* **Eixo Vertical Dinâmico (Cima / Baixo):**
* `y1` e `y2`: Força vertical adicional aplicada para armas cujo recuo aumenta ou diminui ao longo da rajada.
* `tym1` e `tym2`: O tempo de disparo contínuo (em milissegundos) necessário para ativar as correções `y1` e `y2`.



> 💡 **Nota Prática:** Variáveis que começam com `tm` ou `tym` servem como **cronômetros (gatilhos de tempo)**, enquanto `r`, `x` e `y` definem a **força real de movimento** aplicada ao sensor do mouse.

---

## 📦 Como Instalar

1. Abra o software **Logitech G-Hub**, vá na aba superior e clique em **Perfis**.
2. Clique em **Adicionar Jogos e Aplicativos** e selecione o executável do **Rainbow Six Siege**.
3. Na tela de Perfis, clique nos 3 pontinhos do perfil **Padrão** do jogo e selecione **Criar Script LUA**.
4. Em seguida, na parte inferior, clique em **Crie um novo Script de LUA**.
5. Apague o código pré-escrito e cole o script completo.
6. Na parte superior esquerda, clique em **Script** e em seguida **Salvar e executar**.
7. Aumente o tamanho do console na parte inferior da tela para obter a visualização ideal do painel de operadores.

---

## ⚙️ Como Configurar e Ajustar no Jogo

⚠️ **IMPORTANTE:** O script funciona com **qualquer** configuração de sensibilidade, DPI ou FOV que você utilize no jogo ele apenas deve ser ajustado conforme a necessidade. Ele vem com valores *padrão* em todos os operadores, os quais **não** vão funcionar perfeitamente na sua tela logo de início. Você deve calibrar os eixos manualmente para os perfis `p` (primária) e `s` (secundária) de cada personagem.

### 🏋️‍♂️ Passo a Passo para Calibração:

1. Entre no **Campo de Tiro** do Rainbow Six Siege.
2. Escolha o operador que deseja ajustar.
3. Atire contra o alvo com a arma **Primária** sem mover o mouse e observe o comportamento do tiro:
* **Se a arma subir:** Aumente o valor de `r` dentro do bloco `p={...}` do operador.
* **Se a arma descer demais:** Diminua o valor de `r` no bloco `p={...}`.
* **Se a arma puxar para os lados:** Ajuste os valores de `x1`/`x2` correspondentes.


4. Role o **Scroll do Mouse** para mudar o script para o modo secundário, equipe a pistola/SMG secundária no jogo e repita o processo ajustando os valores dentro do bloco `s={...}`.
5. Dê Alt-Tab para o G-Hub, altere os números na tabela do operador, salve (`Ctrl + S`) e teste novamente no jogo.

---
⚠️ *Aviso: Este script foi desenvolvido apenas para fins de estudo de automação de periféricos utilizando a API oficial da Logitech. Use com responsabilidade.*
