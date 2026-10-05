# InverterLab — Histórico de versões

Simulador educacional de inversores de frequência, baseado no Altus AD600M.
Projeto independente e não oficial, desenvolvido por **Caio Bondarchuk** e **Breno Rossi**.

- Repositório: https://github.com/caiobondarchuk/inverterlab_simulador-ad600m
- Versão online: https://caiobondarchuk.github.io/inverterlab_simulador-ad600m/

Este documento registra a evolução do sistema versão por versão: o que foi adicionado, corrigido ou removido em cada uma e como o trabalho foi conduzido. As informações vêm da análise dos arquivos de cada versão e do histórico das conversas de desenvolvimento.

---

## Como ler este histórico

**Numeração.** Os arquivos foram nomeados `V03`, `V04` … `V10` durante o desenvolvimento. Aqui eles ganham um número de versão para o GitHub:

| Arquivo | Versão | Nome do sistema na época |
|---|---|---|
| `SimInversor - Altus AD600M - V03` | **v0.3** | SimInversor |
| `SimInversor - Altus AD600M - V04` | **v0.4** | SimInversor |
| `SimInversor_Altus_AD600M_V05` | **v0.5** | SimInversor |
| `SimInversor_Altus_AD600M_V06` | **v0.6** | SimInversor |
| `SimInversor_Altus_AD600M_V07` | **v0.7** | SimInversor |
| `SimInversor_Altus_AD600M_V08` | **v0.8** | SimInversor |
| `SimInversor_Altus_AD600M_V09` | **v0.9** | SimInversor |
| `SimInversor_Altus_AD600M_V10` | **v0.10** | SimInversor |
| `InverterLab_V10` | **v1.0 — primeira versão pública** | InverterLab |

Observações:
- O arquivo final se chama `InverterLab_V10` porque o nome "V10" foi mantido na troca de marca. Para o histórico, ele é a **v1.0**, e o `SimInversor_..._V10` anterior aparece como **v0.10**.
- As versões V01 e V02 não foram enviadas para este levantamento e por isso **não estão documentadas**.
- As datas de cada versão não foram registradas durante o desenvolvimento, então não aparecem aqui.

**Origem de cada versão.**
- **v0.3 e v0.4:** base construída antes das conversas registradas neste histórico. Foram descritas a partir do código. O processo detalhado não foi registrado.
- **v0.5:** continuação feita pelo próprio autor, sem a minha participação. Também descrita a partir do código.
- **v0.6 a v1.0:** desenvolvidas nas conversas deste projeto. Para elas, o processo está documentado em detalhe.

---

## Resumo

| Versão | Tema principal |
|---|---|
| **v0.3** | Base do simulador: bancada, simulação, IHM, motor, osciloscópio e exercícios |
| **v0.4** | Painel do inversor aberto pela bancada e edição bloqueada durante a simulação |
| **v0.5** | Novo cálculo elétrico por potenciais, fontes por fase, contator completo e novos disjuntores |
| **v0.6** | Correção dos bugs da v0.5, desfazer/refazer e arraste de fios |
| **v0.7** | Novos símbolos, cores de corrente por tipo, menu da paleta retrátil e limpeza dos exercícios |
| **v0.8** | Fios paralelos sem sobreposição, brilho suave, potenciômetro e motor no inspetor |
| **v0.9** | Emendas (nós) nos fios |
| **v0.10** | Idioma EN/PT, créditos, símbolos corrigidos, rótulos e remoção do CLP |
| **v1.0** | Parâmetros do manual, marca InverterLab e primeira versão pública |

---

## v0.3 — Base do simulador

**Arquivo:** `SimInversor - Altus AD600M - V03` · 134 KB

**O que existe nesta versão**
- **Bancada de montagem** com paleta de componentes organizada em categorias: Alimentação, Proteção, Inversor, Motor, Comando, Sensores, Sinalização, CLP e Auxiliar. São 16 componentes na paleta: rede trifásica 380V, fonte 24VCC, disjuntor tripolar, inversor Altus AD600M, motor trifásico, botoeiras NA e NF, chave seletora, potenciômetro, contator, sensor indutivo, fim de curso, sinaleiro, buzina, CLP simulado e bloco de bornes.
- **Simulação elétrica** com a bancada travada em modo de edição ou de simulação.
- **IHM & Parâmetros:** réplica do teclado do inversor (PRG, RUN, STOP, JOG…), navegação por grupos e **121 parâmetros em 29 grupos**.
- **Motor trifásico** parametrizável, ligado a um motor de cálculo do inversor com **21 códigos de falha**.
- **Osciloscópio:** gráficos em tempo real.
- **Exercícios guiados:** 5 exercícios, de iniciante a avançado (partida simples via IHM, partida por botoeiras, velocidade por potenciômetro, diagnóstico de falta de fase e intertravamento com contator).
- **3 exemplos prontos:** partida básica, partida por botoeira (DI1) e velocidade por potenciômetro.
- **Menus** Arquivo, Editar e Ver (novo, abrir, salvar `.json`, exportar `.svg`, desfazer, refazer, duplicar, excluir, grade, rótulos e zoom).
- Tema claro e escuro.
- A bancada abria com o exemplo "Partida básica" já carregado.

**Processo:** não registrado neste levantamento.

---

## v0.4 — Painel do inversor e modo de simulação

**Arquivo:** `SimInversor - Altus AD600M - V04` · 149 KB (+15 KB)

**Adicionado**
- **Painel do inversor** aberto ao clicar no inversor na bancada. Tem display, botões RUN, STOP e JOG, parâmetros rápidos e mensagem de falha com reset.
- **Edição bloqueada durante a simulação**, com avisos como "Pare a simulação para editar a bancada". Os componentes continuam acionáveis (botões, chaves e sensores).
- **Mensagens de início e parada da simulação** mais claras ("edição bloqueada" / "edição liberada").

**Alterado**
- A bancada passou a abrir **vazia**, com uma mensagem de boas-vindas. Na v0.3 ela abria com o exemplo já carregado.

**Processo:** não registrado neste levantamento.

---

## v0.5 — Novo cálculo elétrico e contator completo

**Arquivo:** `SimInversor_Altus_AD600M_V05` · 158 KB (+9 KB)

**Adicionado**
- **Novo cálculo elétrico por potenciais.** O simulador passou a calcular qual potencial (L1, L2, L3, N, PE, +24V, 0V) chega a cada terminal. Isso permite identificar curto-circuito e usar o neutro e o terra.
- **Fontes separadas por fase:** Fase L1, L2, L3, Neutro N, Terra PE, +24 VCC e 0 V, cada uma como componente próprio.
- **Contator completo:** bobina, contato NA, contato NF e contatos de potência (3P). Os contatos seguem a bobina de mesma TAG.
- **Novos disjuntores:** bipolar e disjuntor-motor.
- **Fios acesos na simulação:** os fios e componentes passaram a mudar de cor quando energizados.
- **Quarto exemplo:** "Comando com selo (K1)", no estilo do CADe_SIMU.
- **Migração de projetos antigos** para os novos componentes.

**Problemas conhecidos nesta versão** (relatados pelo autor e corrigidos na v0.6)
- Os itens da paleta mostravam a palavra "undefined" no lugar do símbolo.
- O painel do inversor não atualizava os Hz ao dar RUN.
- Os fios do inversor até o motor não acendiam.
- Os itens "Alternar grade", Desfazer, Refazer e Duplicar do menu não funcionavam.
- O cursor selecionava texto e imagens ao arrastar componentes ou fios.

**Processo:** desenvolvida pelo autor, sem registro neste levantamento.

---

## v0.6 — Correção dos bugs da v0.5

**Arquivo:** `SimInversor_Altus_AD600M_V06` · 164 KB (+6 KB)

**Contexto.** O autor enviou a v0.5 com capturas de tela dos problemas e pediu para corrigir tudo e adicionar três melhorias: fios que "brilham" em vez de mudar de cor, mover fios depois de conectados (como no FluidSIM) e menus funcionando.

**Corrigido**
- **"undefined" na paleta:** a paleta agora desenha o mesmo símbolo usado na bancada, em vez de um ícone que não existia para as fontes de fase.
- **Hz no painel do inversor:** o painel só era desenhado ao abrir e ao clicar nos botões. Passou a atualizar a cada ciclo da simulação.
- **Fios do inversor ao motor:** a energização só partia das fontes. Agora os terminais U, V e W do inversor também energizam os fios até o motor quando há frequência de saída.
- **Alternar grade:** o menu enviava o nome `grade` e o código esperava `grid`.
- **Seleção de texto:** a bancada passou a bloquear seleção e arrasto nativo do navegador ao conectar fios ou mover componentes.

**Adicionado**
- **Brilho nos fios:** em vez de trocar a cor, o fio fica mais grosso e com um halo.
- **Arraste de fios:** o trecho do meio do fio pode ser movido, com botão "Redefinir trajeto" no inspetor.
- **Desfazer, Refazer e Duplicar** funcionando, com atalhos Ctrl+Z, Ctrl+Y e Ctrl+D e até 100 passos de histórico. "Remover todas as ligações" também entrou no histórico.

**Processo**
- As correções descritas por uma IA anterior não estavam no arquivo enviado, então o trabalho foi refeito sobre o arquivo real.
- Cada bug foi investigado até a causa. Exemplos: o menu da grade usava um nome diferente do esperado, e o painel do inversor só se redesenhava quando clicado.
- As mudanças foram aplicadas por script, com substituições de texto exato. O script falha de forma visível se um trecho não for encontrado.
- Depois de cada ciclo, o código passou por verificação de sintaxe e teste automático no navegador.

**Testes realizados:** a paleta sem "undefined" (19 de 26 itens com símbolo); adicionar, duplicar, desfazer e refazer um componente (resultado 1, 2, 1, 2); ausência de erros no console.

---

## v0.7 — Símbolos, cores de corrente e limpeza

**Arquivo:** `SimInversor_Altus_AD600M_V07` · 166 KB (+2 KB)

**Contexto.** O autor enviou imagens da simbologia desejada e pediu cores por tipo de corrente, arrasto de fios também na horizontal, paleta retrátil e limpeza dos exercícios.

**Adicionado**
- **Novos símbolos**, redesenhados a partir das imagens enviadas: botoeiras NA e NF (com acionamento tracejado e "E"), contatos NA e NF do contator, contatos de potência, disjuntores monopolar, bipolar e tripolar (com -Q, ligação mecânica e bloco térmico/magnético), buzzer, potenciômetro (zigue-zague com seta) e sensor indutivo.
- **Dois componentes novos:** disjuntor monopolar e sensor capacitivo.
- **Cores de brilho por tipo de corrente:** CA em vermelho, corrente contínua em amarelo, negativo (0V) em azul escuro e neutro em azul claro. O terra (PE) ficou em verde. Valem para fios, terminais e componentes.
- **Arraste de fios em dois eixos:** o eixo é escolhido pela direção em que o usuário começa a arrastar, com encaixe na grade.
- **Categorias da paleta retráteis**, como um menu "dropdown".

**Removido**
- O **bloco de bornes** e a categoria "Auxiliar".
- Os exercícios 2 a 5 e os exemplos extras: ficou só **"Partida simples via IHM"** nos exercícios e em Arquivo → Carregar exemplo.

**Processo**
- Cada símbolo foi desenhado em SVG seguindo a imagem enviada e conferido por captura de tela. A espessura do traço e o tamanho dos ícones da paleta foram ajustados depois da primeira captura.
- Projetos antigos com o componente removido passaram a abrir sem ele, e os fios ligados a ele são descartados.

**Testes realizados:** captura dos símbolos; simulação com fonte 24V, 0V, neutro e fase mostrando as quatro cores de brilho (`dc`, `neg`, `neu`, `ac`); recolher e expandir categorias.

---

## v0.8 — Fios organizados e inspetor mais completo

**Arquivo:** `SimInversor_Altus_AD600M_V08` · 169 KB (+3 KB)

**Adicionado**
- **Fios paralelos sem sobreposição:** um algoritmo de roteamento afasta automaticamente fios que ficariam um em cima do outro, em passos de meia grade. Vale também para fios arrastados pelo usuário.
- **Fios travados durante a simulação:** não é mais possível clicar neles nem trocar a cor enquanto a simulação está ligada.
- **Potenciômetro ajustável na simulação:** o valor analógico pode ser alterado pelo inspetor com a simulação rodando.
- **Especificações do motor no inspetor:** plaqueta editável com a simulação parada e somente leitura durante a simulação.

**Alterado**
- **Brilho mais suave** nos fios e componentes (o anterior estava forte demais).

**Processo**
- O potenciômetro não podia ser alterado porque, durante a simulação, o clique no componente não o selecionava e o inspetor nunca abria. A correção foi permitir a seleção dos componentes não acionáveis, sem quebrar o clique de botões e disjuntores.
- O desvio de fios paralelos foi calculado sobre os segmentos de cada fio, ignorando os trechos que saem do mesmo terminal, que podem coincidir.

**Testes realizados:** nenhuma sobreposição de fios no exemplo e num caso de dois fios paralelos; fios sem resposta a clique durante a simulação; o slider do potenciômetro alterando o valor; plaqueta do motor visível no inspetor.

**Pendência registrada:** o pedido de **trocar o idioma** feito neste ciclo **não foi entregue na v0.8**. Foi entregue na v0.10.

---

## v0.9 — Emendas (nós)

**Arquivo:** `SimInversor_Altus_AD600M_V09` · 173 KB (+4 KB)

**Contexto.** O autor enviou uma imagem de um circuito com uma emenda entre fios e pediu uma forma de conectar fios com nós, como no exemplo.

**Adicionado**
- **Emendas nos fios.** Três formas de criar: soltar um fio sobre outro fio, clicar duas vezes num fio ou usar Alt + arrastar sobre o fio.
- **Arrastar a partir da emenda** para ligar outro fio. Com Shift + arrastar, a emenda é movida.
- **Excluir uma emenda** com Del. Quando ela tem exatamente dois fios, eles são unidos de novo em um só.
- As dicas da bancada e a ajuda explicam as emendas.

**Processo**
- A emenda foi modelada como um componente oculto com um único terminal. Assim, ela herda sem esforço o salvamento, o desfazer, o cálculo elétrico e o brilho.
- Ao criar uma emenda, o fio original é dividido em dois, preservando a cor.
- O roteamento foi ajustado para a emenda não ter "haste" e os fios chegarem a ela em formato de L, o que reproduz o desenho original do fio.

**Testes realizados:** criação de duas emendas arrastando terminais sobre um fio (5 fios no total) e simulação mostrando todos os fios energizados em 24V.

---

## v0.10 — Idioma, créditos e acabamento

**Arquivo:** `SimInversor_Altus_AD600M_V10` · 207 KB (+34 KB)

**Contexto.** O autor pediu correções de símbolos e de rótulos, um botão de idioma no canto superior direito, a retirada do CLP e uma área de créditos.

**Adicionado**
- **Idioma EN/PT:** botão no canto superior direito. O sistema abria em **inglês**, e a escolha fica salva no navegador. Cobre menus, abas, paleta, inspetor, avisos, ajuda, exercício, nomes e opções dos parâmetros e mensagens de falha.
- **Créditos:** item Ver → Créditos e a mesma informação na janela de Ajuda.

**Corrigido e alterado**
- **Buzzer** e **contato fechado (NF) do contator** redesenhados a partir das imagens enviadas.
- **Rótulos sobrepostos:** o nome do componente agora fica acima dos números dos terminais.
- **Botão "Rótulos":** passou a esconder também o nome dos componentes, além dos números dos terminais.

**Removido**
- O **CLP** e sua categoria. Projetos antigos que o usavam abrem sem ele.

**Processo**
- O tradutor trabalha sobre o texto que aparece na tela: um dicionário PT→EN e regras para frases com números. Um observador de mudanças traduz o que a interface criar depois.
- Uma varredura automática percorreu todas as telas em inglês procurando texto ainda em português. Ela encontrou uma frase, que foi corrigida.

**Testes realizados:** navegação em EN e PT; alternância de idioma ida e volta; símbolos e rótulos por captura de tela; janela de créditos.

---

## v1.0 — Primeira versão pública (InverterLab)

**Arquivo:** `InverterLab_V10` · 416 KB (+209 KB)

Esta é a versão publicada no GitHub e no GitHub Pages. Consolida tudo o que as versões anteriores trouxeram.

**Marca e textos**
- O sistema passou a se chamar **InverterLab**, com a logo nos modos claro e escuro, favicon e novo título.
- Todos os textos passaram a deixar claro que é um simulador **baseado no** Altus AD600M, **educacional e não oficial**, com aviso de que não há vínculo com a Altus.
- A janela de **Créditos** ganhou os links do GitHub de Caio Bondarchuk e de Breno Rossi.

**Parâmetros conforme o manual** (fonte: Manual do Usuário AD600M Rev. B e Guia de Aplicação Rápida)
- **572 parâmetros em 29 grupos** (P0 a PF, A0 a A3, B0 a B6, U0 e U1), com código, nome, padrão de fábrica, faixa, unidade, opções e atributos (☆ ★ ○ ●). Os nomes e as opções estão em português e em inglês.
- **Tabela de falhas** com os 30 códigos do manual (eram 21).
- **Funções dos terminais DI** (P5-00 a P5-03): FWD, REV, JOG, reset de falha, parada livre, pausa, falha externa e multivelocidade.
- **Saída a relé** TA/TB/TC conforme o parâmetro P6-00.
- **Outros parâmetros ligados à simulação:** sentido de rotação (P0-13), limite superior de frequência (P0-15/P0-16), frequência de partida (P1-04) e modo de parada (P1-13).
- **Reset de parâmetros (P0-28) funcionando:** restaura o padrão de fábrica sem mexer nos parâmetros do motor, nos registros de falha e no P0-20, e só com o inversor parado. Também grava e restaura um backup e apaga os registros de falha.
- **Auto-ajuste do motor (P4-00)** simulado.
- **Monitores U1 e registro de falhas U0** atualizados durante a simulação.
- **Motor padrão** conforme manual e guia: 1,5 kW, 380 V, 3,8 A, 50 Hz, 1450 rpm e 4 polos.
- **Parâmetros ★** só podem ser alterados com o inversor parado.

**Processo**
- As tabelas foram extraídas do PDF do manual por script. Um conjunto de regras identifica as opções de cada parâmetro e converte as faixas. Casos especiais (P0-03, P0-14, P4-01, P4-03 e a continuação das opções de P5-00 em outra página) foram tratados à mão.
- Os nomes e as opções foram traduzidos por índice, para não desalinhar com o manual. O inglês usa o texto original do manual.
- Os parâmetros do motor mudaram de código (agora P4-01 a P4-07), então projetos salvos em versões anteriores abrem com os parâmetros do inversor nos padrões do manual.

**Falha encontrada depois da entrega e corrigida**
- Ao carregar o exemplo "Partida simples via IHM", só os componentes apareciam e os fios não. Além disso, o inversor deixou de ser arrastável.
- **Causa:** uma lista da IHM ainda apontava para o código antigo `P5-04`, que não existe mais no manual. A consulta gerava um erro que interrompia a montagem do exemplo e a seleção do inversor.
- **Correção:** a lista passou a usar P5-00 a P5-03.

**Testes realizados**
- Simulação do inversor com FWD, REV e parada.
- Multivelocidade (30 Hz, com 60% de 50 Hz).
- Falha externa (Err28) e reset por terminal.
- Reset de parâmetros pelo P0-28.
- Painel do inversor (12,58 Hz), monitores U1 e relé energizado.
- Depois da falha relatada: o exemplo carrega 6 componentes e 9 fios, o inversor é arrastado e o clique simples ainda abre o painel.

**Limitações conhecidas**
- A tomada TA/TB/TC assume **TA comum, TB normalmente fechado e TC normalmente aberto**. O guia não deixa isso claro, então vale conferir no equipamento.
- Os parâmetros estão no manual, mas **nem todos têm efeito na simulação**: o simulador usa um modelo V/F simplificado.
- A fonte Roboto Condensed é carregada do Google Fonts quando há internet.

---

## Pacotes e ferramentas de distribuição

Criados depois da v1.0, sem mudar o comportamento do simulador:

- **Versão web / PWA:** `index.html`, `manifest.webmanifest`, `sw.js` (uso offline) e ícones, gerados a partir da logo. É o conteúdo publicado no GitHub Pages. Testada localmente, inclusive abrindo a página sem internet.
- **Projeto Electron (`.exe` para Windows):** `main.js`, `package.json` e ícone `.ico`. **Não foi testado**, porque o `.exe` só pode ser gerado no Windows. Ainda precisa de um teste de instalação.
- **`scripts/baixar-fontes.js`:** baixa as fontes do Google Fonts para uso 100% offline. A lógica de processamento foi testada, mas o download real, não.
- **Arquivo avulso com JetBrains Mono embutida** e **ferramenta `Embutir-fontes-InverterLab.html`**, que embute também a Roboto Condensed no arquivo. Servem para distribuir **um único HTML** que abre igual em qualquer computador, mesmo sem internet. A ferramenta foi testada com internet simulada, não com o Google Fonts real.

---

## Evolução em números

Contagens medidas abrindo cada versão no navegador.

| Versão | Tamanho | Itens na paleta | Parâmetros | Códigos de falha | Exercícios | Idiomas |
|---|---|---|---|---|---|---|
| v0.3 | 134 KB | 16 | 121 | 21 | 5 | PT |
| v0.4 | 149 KB | 16 | 121 | 21 | 5 | PT |
| v0.5 | 158 KB | 26 | 121 | 21 | 5 | PT |
| v0.6 | 164 KB | 26 | 121 | 21 | 5 | PT |
| v0.7 | 166 KB | 27 | 121 | 21 | 1 | PT |
| v0.8 | 169 KB | 27 | 121 | 21 | 1 | PT |
| v0.9 | 173 KB | 27 (mais a emenda, que não aparece na paleta) | 121 | 21 | 1 | PT |
| v0.10 | 207 KB | 26 | 121 | 21 | 1 | EN / PT |
| v1.0 | 416 KB | 26 | 572 | 30 | 1 | EN / PT |

Obs.: o salto de itens na v0.5 vem das fontes separadas por fase (7 itens no lugar de 2) e dos novos componentes do contator e dos disjuntores. O tamanho do arquivo mais que dobrou entre a v0.10 e a v1.0, principalmente por causa da base de parâmetros do manual e da logo embutida.

---

## Como o trabalho foi conduzido

Entre a v0.6 e a v1.0, o ciclo foi sempre o mesmo:

1. **Relato do autor**, quase sempre com capturas de tela dos problemas e imagens da simbologia desejada.
2. **Leitura do arquivo real** enviado, sem assumir o que havia na versão anterior.
3. **Busca da causa de cada problema**, em vez de corrigir só o sintoma.
4. **Alterações por script**, com substituição de texto exato, para falhar de forma visível quando algo não era encontrado.
5. **Verificação de sintaxe** de cada bloco de JavaScript.
6. **Teste automático no navegador**, com capturas de tela, para confirmar o comportamento.
7. **Entrega do arquivo**, com a lista do que mudou e do que ficou pendente ou sem teste.

Limites do processo: não houve acesso à internet no ambiente de desenvolvimento, então o download real das fontes e a geração do `.exe` não puderam ser testados.

---

## Pendências e próximos passos

- Testar o instalador `.exe` (Electron) em um computador Windows.
- Embutir a fonte Roboto Condensed no arquivo, para uso offline total.
- Exercícios guiados com **vídeo-tutorial do YouTube** em cada um. Funcionam bem quando o sistema está hospedado, como no GitHub Pages.
- Voltar com o componente **CLP**, que foi retirado na v0.10 a pedido do autor.
- Mais exercícios, já que ficou só um desde a v0.7.
- Conferir no equipamento real a ligação do relé TA/TB/TC.
- Criar *releases* no GitHub para cada versão (v0.3 … v1.0), anexando o arquivo correspondente.
