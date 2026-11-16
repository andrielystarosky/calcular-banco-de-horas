# Meu Banco de Horas

Calculadora responsiva de banco de horas, feita com HTML, CSS e JavaScript puro. Interface clara com detalhes em degradê azul. Não requer instalação de dependências, compilação, servidor de aplicação ou banco de dados.

## Arquivos

| Arquivo | Conteúdo |
| --- | --- |
| `index.html` | Página completa, com estrutura HTML, estilos no bloco `<style>` e lógica no bloco `<script>`. |
| `README.md` | Documentação do projeto. |

O pacote contém o código da aplicação, sem credenciais, histórico Git ou configurações vinculadas à hospedagem original.

## Executar

1. Extraia o ZIP.
2. Abra a pasta `banco-de-horas`.
3. Abra `index.html` no navegador.

Para desenvolvimento, recomenda-se usar um servidor HTTP local, pois o comportamento de armazenamento em arquivos abertos diretamente pode variar conforme o navegador.

### Com VS Code

Abra a pasta no VS Code e sirva o `index.html` com uma extensão de servidor local, caso já utilize uma.

### Com Python instalado

No terminal, dentro da pasta do projeto:

```bash
python -m http.server 8000
```

No Windows, também pode usar:

```powershell
py -m http.server 8000
```

Acesse `http://localhost:8000`. Para encerrar, pressione `Ctrl+C` no terminal. Use sempre a mesma origem e porta para acessar os mesmos dados locais.

## Aba Jornada de trabalho

1. Informe entrada e saída.
2. Informe a duração total do intervalo em horas e minutos.
3. Defina a jornada prevista no formato de horas e minutos.
4. Se a saída acontecer no dia seguinte, marque a opção correspondente.
5. Clique em **Calcular jornada**.

O resultado mostra o total trabalhado e a diferença em relação à jornada prevista.

Exemplo: entrada às 08:00, saída às 17:30, intervalo de 1h e jornada prevista de 8h resultam em 8h30 trabalhadas e saldo de +0h30.

A jornada é calculada assim:

```text
Tempo decorrido = saída − entrada + 24h, se marcado dia seguinte
Tempo trabalhado = tempo decorrido − intervalo
Saldo do dia = tempo trabalhado − jornada prevista
```

Esta aba calcula um dia por vez. Não mantém histórico diário e não transfere o saldo automaticamente para a segunda aba. Os campos desta aba não são persistidos.

## Aba Somar e subtrair

1. Defina o sinal do saldo inicial: positivo ou negativo.
2. Informe suas horas e minutos iniciais.
3. Escolha **Somar** ou **Subtrair**.
4. Informe o tempo da movimentação.
5. Clique em **Adicionar ao cálculo**.
6. Repita para cada movimentação.

O saldo final é atualizado a cada lançamento. O botão `×` remove uma movimentação; **Limpar cálculo** zera o saldo inicial e remove todos os lançamentos, sem confirmação e sem opção de desfazer.

Exemplo manual: saldo inicial de +16h, somar 2h, subtrair 1h e somar 47min produz +17h47. O botão de preenchimento de exemplo foi removido desta versão.

Os minutos devem estar entre 0 e 59. Para 90 minutos, informe 1 hora e 30 minutos. Movimentações precisam ser maiores que zero. As horas e minutos são inteiros.

## Como os cálculos funcionam

Todos os tempos são convertidos para minutos inteiros antes das operações:

```text
Total em minutos = horas × 60 + minutos
Saldo final = saldo inicial com sinal + soma das movimentações com sinal
```

A exibição converte o resultado novamente para horas e minutos. `17h47` significa 17 horas e 47 minutos, e não 17,47 horas decimais. Saldos negativos são exibidos com `−`; saldos positivos, com `+`.

## Armazenamento e privacidade

A segunda aba salva automaticamente o saldo inicial e as movimentações no `localStorage`, na chave `banco-horas-v1`. O cálculo é executado no navegador; o código não envia os lançamentos a nenhum servidor e não usa serviços externos, cookies de rastreamento ou bibliotecas remotas.

- Os dados pertencem ao navegador, perfil e origem utilizados.
- Não há conta, sincronização entre dispositivos, exportação de dados ou backup automático.
- Limpar os dados do navegador pode apagar os lançamentos.
- Navegação privada pode impedir a persistência ou apagar os dados ao encerrar a sessão.
- Mudar de domínio, protocolo ou porta cria outro contexto de armazenamento.
- Em computador compartilhado, outras pessoas com acesso ao mesmo perfil podem consultar os dados.
- Se o navegador bloquear o armazenamento, o cálculo continua disponível na sessão, mas pode não ser salvo; a interface não exibe aviso dessa falha.

O ZIP contém somente o código: não inclui os lançamentos salvos no seu navegador.

## Personalizar

Edite `index.html` em um editor de texto, como VS Code.

### Textos e título

Altere `<title>`, o título `<h1>`, as legendas e os textos dos botões no HTML.

### Cores e aparência

Os estilos ficam entre `<style>` e `</style>`. A parte final do bloco contém os ajustes visuais mais recentes; quando há regras repetidas, a regra posterior prevalece.

| Uso | Cor |
| --- | --- |
| Fundo | `#F7F8FA` |
| Cards | `#FFFFFF` |
| Texto principal | `#20242C` |
| Azul principal | `#2563EB` |
| Final do degradê da faixa de saldo | `#38BDF8` |
| Saldo positivo na lista | `#238163` |
| Saldo negativo na lista | `#C34D5B` |

Procure por `button.primary` para alterar o botão principal e `.result:before` para alterar a faixa em degradê do card de saldo. A interface utiliza fontes disponíveis no sistema, sem download de fontes externas.

### Funções principais

| Função | Responsabilidade |
| --- | --- |
| `tab(n)` | Alterna as duas abas. |
| `calculate()` | Calcula jornada, intervalo e saldo diário. |
| `fmt(n)` | Formata minutos como horas e minutos. |
| `render()` | Atualiza saldo final e lista de movimentações. |
| `save()` | Persiste os dados da segunda aba. |
| `resetAll()` | Limpa o cálculo da segunda aba. |

O envio do formulário `movement` adiciona os lançamentos. O trecho final do script recupera os dados locais, atualiza a segunda aba e calcula os valores iniciais da jornada.

## Publicar online

O projeto é estático. A pasta a publicar deve conter `index.html` na raiz. Não é necessário comando de build, npm, PHP ou banco de dados. Se o serviço pedir diretório de saída, selecione a pasta que contém `index.html`.

### Hospedagem estática

Envie `index.html` para a raiz pública do serviço escolhido. Em hospedagem tradicional, essa raiz pode ser uma pasta como `public_html`. O README não é necessário para o funcionamento online.

### Hospedagem integrada com Git

Crie um repositório com os arquivos desta pasta e configure o serviço para publicar a raiz como site estático, sem etapa de compilação. Os nomes e fluxos de configuração variam conforme o provedor.

Ao publicar em uma hospedagem própria, as regras de acesso dependem desse serviço. O código fornecido não implementa login, senha nem restrição de visitantes. O acesso privado do site original é oferecido pela plataforma de hospedagem e não acompanha o HTML.

## Conferência manual

| Verificação | Resultado esperado |
| --- | --- |
| Entrada 08:00; saída 17:00; intervalo 1h; prevista 8h | 8h00 trabalhadas; saldo 0h00. |
| Entrada 08:00; saída 17:30; intervalo 1h; prevista 8h | Saldo +0h30. |
| Entrada 08:00; saída 16:00; intervalo 1h; prevista 8h | Saldo −1h00. |
| Entrada 22:00; saída 06:00; dia seguinte marcado; intervalo zero; prevista 8h | Saldo 0h00. |
| Intervalo maior que o período da jornada | Mensagem de erro. |
| Inicial +16h; +2h; −1h; +47min | Saldo +17h47. |
| Inicial −2h; somar 30min | Saldo −1h30. |
| Remover um lançamento pelo × | Recalcula o total. |
| Recarregar na mesma origem, com armazenamento permitido | Recupera os dados da segunda aba. |
| Limpar cálculo | Saldo zerado e lista vazia. |

## Limitações atuais

- Controle pessoal baseado nos tempos informados; sem adicionais, tolerâncias, arredondamentos, feriados, regras trabalhistas ou regras específicas da empresa.
- Não calcula valores financeiros, horas noturnas reduzidas ou percentuais de horas extras.
- A jornada prevista é um horário de duração inferior a 24h; o controle de jornada não foi pensado para períodos com mais de uma virada de dia.
- Não oferece histórico por data, múltiplas pessoas, edição direta de lançamentos, relatórios ou integração com sistema de ponto.
- Para corrigir uma movimentação, remova-a e adicione novamente.
- Os campos não foram projetados para valores extremos de horas ou edição manual de dados no armazenamento.

## Solução de problemas

**O cálculo não ficou salvo:** utilize a mesma origem e o mesmo perfil de navegador; confira permissões de armazenamento e evite navegação privada. Para desenvolvimento, use um servidor local com porta fixa.

**O visual antigo continua aparecendo:** recarregue a página ignorando o cache (`Ctrl+F5` no Windows) e confira se o arquivo atualizado foi enviado para a pasta correta.

**A saída é menor que a entrada:** se a jornada atravessou a meia-noite, marque a opção de saída no dia seguinte.

**Preciso informar 75 minutos:** use 1 hora e 15 minutos.

**Quero usar em outro dispositivo:** esta versão não sincroniza dados. Abra o site no outro dispositivo e informe os lançamentos novamente.

## Dependências

Nenhuma dependência de execução. Apenas um navegador moderno com JavaScript habilitado. Python é opcional e serve somente para hospedar os arquivos localmente durante o desenvolvimento.
