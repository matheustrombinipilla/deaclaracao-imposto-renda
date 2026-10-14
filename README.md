# IR Fácil: planilha de controle de dados para a declaração do Imposto de Renda

Planilha em Excel que organiza, em um só lugar, as informações necessárias para preencher a declaração do Imposto de Renda de pessoa física: dados do titular, informes de rendimentos e despesas dedutíveis. Tem menu lateral de navegação, validação de dados na digitação e resumos que se atualizam sozinhos.

> Projeto educacional para portfólio. Todos os dados de exemplo (nomes, CPF, empresas, valores) são **fictícios**. A planilha organiza informações; ela não calcula o imposto devido nem substitui o programa oficial da Receita Federal ou orientação de um contador.

## O que o sistema faz

| Tela | Para que serve |
|---|---|
| **TITULAR** | Guarda os dados pessoais do contribuinte e mostra o quanto da tela já foi preenchido. |
| **INFORMES** | Lista cada informe de rendimentos recebido (fonte pagadora, tipo, valor e IR retido) e soma tudo por tipo de rendimento. |
| **NOTAS** | Registra recibos e notas de despesas dedutíveis (saúde, educação etc.) e soma por categoria. |

### Tela 1: TITULAR

Campos: ano-calendário, nome, CPF, nascimento, título de eleitor, cônjuge, rua, rua abreviada, CEP, telefone, celular, e-mail e três perguntas de SIM/NÃO (houve alterações da entrega anterior, dependente cônjuge, residente no exterior).

- **Rua abreviada** é calculada automaticamente a partir da rua (corta endereços longos em 30 caracteres).
- **Preenchimento** mostra o percentual de campos preenchidos (fica em âmbar enquanto estiver abaixo de 100%).
- **Alerta de consistência:** se "Dependente cônjuge" for SIM e o campo do cônjuge estiver vazio, a célula fica vermelha e aparece um aviso.

### Tela 2: INFORMES

- Até 15 informes, um por linha: fonte pagadora, CNPJ/CPF, tipo de rendimento, rendimento anual, IR retido e situação do comprovante.
- **Totais** de rendimento e de IR retido.
- **Resumo por tipo** (Salário, Aluguel, Pró-labore, Aplicações financeiras, Dividendos, Outros).
- Aviso automático se algum valor ficar sem tipo informado.

### Tela 3: NOTAS

- Até 20 lançamentos: data, descrição, categoria, valor, número do recibo/nota e situação do comprovante.
- **Resumo por categoria** com quantidade de lançamentos, total e percentual do total.
- **Educação considerada:** aplica um limite anual editável (ver Premissas) sobre o total de educação.
- Aviso automático se algum valor ficar sem categoria.

## Recursos do Excel usados

### Validação de dados

| Campo | Regra |
|---|---|
| Ano-calendário | inteiro entre 2000 e 2100 |
| CPF | formato `000.000.000-00` |
| Nascimento | data válida, não futura |
| Título de eleitor | 12 dígitos numéricos |
| CEP | formato `00000-000` |
| Telefone / Celular | formato `(DD) 0000-0000` ou `(DD) 90000-0000` |
| E-mail | precisa conter `@` e um ponto depois dele |
| SIM/NÃO, tipo, categoria, comprovante | lista suspensa |
| CNPJ / CPF (informes) | 18 ou 14 caracteres, com pontuação |
| Rendimento | número maior ou igual a zero |
| IR retido | número entre 0 e o rendimento da mesma linha |
| Data da nota | dentro do ano-calendário informado na tela TITULAR |
| Valor da nota | número maior que zero |

Cada campo mostra uma dica ao ser selecionado e uma mensagem de erro clara quando o dado é recusado.

### Navegação e interatividade

- Menu lateral e botões "PRÓXIMO →", "← VOLTAR" e "VOLTAR AO INÍCIO" criados com a função `HYPERLINK`. O item da tela atual fica destacado.
- Formatação condicional: comprovante "Pendente" em vermelho e "Recebido" em verde, além dos alertas de consistência.
- Listas suspensas alimentadas por uma aba de apoio oculta (`Listas`), com intervalos nomeados.

### Funções e nomes

`SOMA`, `SOMASE`, `CONT.SE`, `CONT.VALORES`, `LINS`, `SE`, `ESQUERDA`, `NÚM.CARACT`, `MÍNIMO`, `HYPERLINK`, além dos intervalos nomeados `Ano_Calendario`, `Limite_Educacao`, `Lista_SimNao`, `Lista_TipoRend`, `Lista_CategDesp` e `Lista_Status`.

## Como usar

1. Abra `controle_ir.xlsx` e comece pela aba **TITULAR**.
2. Preencha apenas as células sombreadas (verde-claro). As demais são calculadas.
3. Avance pelo botão **PRÓXIMO →** ou pelo menu lateral para **INFORMES** e **NOTAS**.
4. Substitua as linhas de exemplo pelos seus dados reais. Para limpar um exemplo, selecione a linha e apague o conteúdo (as validações permanecem).
5. Marque o comprovante de cada linha como **Recebido** ou **Pendente** para acompanhar o que ainda falta juntar.

### Exemplo incluído (dados fictícios)

- Rendimentos: R$ 105.200,00, com R$ 6.600,50 de IR retido, em 3 informes.
- Despesas: R$ 3.950,00 em 3 lançamentos (saúde, educação e previdência privada).
- Educação considerada dentro do limite: R$ 1.200,00.

## Premissas e limitações

- O **limite anual de educação (R$ 3.561,50)** é um valor de referência editável (célula na aba NOTAS). É uma premissa minha: confirme o valor vigente no site da Receita Federal antes de usar.
- As listas de tipos de rendimento e categorias de despesa são simplificadas e podem ser editadas na aba oculta `Listas` (clique com o botão direito em qualquer aba, "Reexibir").
- A validação de CPF verifica o formato, não os dígitos verificadores.
- A planilha não calcula o imposto a pagar ou a restituir.
- Os prints foram gerados com o LibreOffice; no Excel, a aparência pode variar levemente.

## Estrutura do repositório

```
controle_ir.xlsx
README.md
prints/
```
