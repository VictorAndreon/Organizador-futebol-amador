# Documentação do Projeto — Organizador de futebol amador

# Parte I — Documento de Especificação de Requisitos

> Versão no modelo da disciplina: [Documento_de_Requisitos.docx](documentos/Documento_de_Requisitos.docx)

| | |
|---|---|
| **Projeto / Sistema:** | Organizador de futebol amador |
| **Cliente / Solicitante:** | Prof. Mateus de Freitas Invernisi (APS - IFSUL) |
| **Responsável(is):** | Victor Hugo Andreon de Camargo |
| **Data:** | 04/11/2026 |
| **Versão:** | 1.0 |

## 1. Introdução

### 1.1 Sobre este documento

Este documento tem como objetivo apresentar e organizar os requisitos levantados para o sistema, servindo de referência para as etapas de projeto, desenvolvimento, testes e validação.

### 1.2 Descrição do Mini-Mundo

Hoje, as partidas de futebol amador são marcadas geralmente pelo WhatsApp, tanto no contato com a quadra quanto com os jogadores da pelada. A lista surge da vontade de jogar: alguém (o organizador) cria uma lista simples com a data e o local no cabeçalho, como "Futebol (data) — 1 - Jogador1; 2 - Jogador2", e o pessoal vai preenchendo.

Quando a lista lota, geralmente com 14 jogadores (futebol 7), ainda são aceitos 2 jogadores como reserva. Depois disso, o pessoal pede para que não escrevam mais seus nomes na lista. Quando alguém desiste, a pessoa retira o nome da lista e fica o vazio para alguém preencher, sem nenhuma ordem definida de quem entra no lugar.

A divisão dos times é feita na hora, por sorteio aleatório em um sorteador online.

O pagamento geralmente é avulso: a pessoa que coordena a lista paga a quadra e depois cobra de cada jogador individualmente. É usada a mesma lista do jogo, só que para pagamento: o jogador paga, coloca o emoji de certo ao lado do nome e envia o comprovante para quem pagou a quadra (no melhor dos casos). Na prática, o organizador tem que ficar cobrando quem ainda não pagou.

Os principais envolvidos são o **organizador**, que cria a lista, contata a quadra, paga e cobra os jogadores, e os **jogadores**, que se inscrevem, desistem e pagam sua parte. As informações relevantes são a partida (data, horário e local), a lista de jogadores e reservas, os times sorteados e quem pagou ou está devendo.

### 1.3 Propósito do Sistema

O propósito é auxiliar e facilitar a manutenção e organização dessas partidas, fazendo com que o controle da lista seja mais fácil, tanto no controle dos pagamentos quanto no sorteio dos times, registros das partidas, etc. Espera-se que o organizador tenha uma visão clara de quem confirmou, quem desistiu e quem está devendo, sem depender de mensagens soltas no WhatsApp, e que as vagas deixadas por desistências sejam preenchidas automaticamente pelos reservas.

## 2. Requisitos Funcionais

| ID | Descrição | Prioridade | Depende de |
|---|---|---|---|
| RF01 | O sistema deve permitir que o usuário se cadastre informando nome, telefone, e-mail, senha e posição preferida (linha ou goleiro). | Alta | — |
| RF02 | O sistema deve permitir que o usuário cadastrado se autentique com e-mail e senha. | Alta | RF01 |
| RF03 | O sistema deve permitir que o organizador crie uma partida informando data, horário, local, modalidade (futsal, society ou campo), número de vagas para titulares, número de vagas para reservas e valor total da quadra. | Alta | RF02 |
| RF04 | O sistema deve gerar um link de convite para cada partida, que o organizador pode compartilhar com os jogadores. | Alta | RF03 |
| RF05 | O sistema deve permitir que o organizador cancele uma partida que ainda não foi iniciada. | Média | RF03 |
| RF06 | O sistema deve permitir que o jogador confirme presença em uma partida por meio do link de convite. | Alta | RF02, RF04 |
| RF07 | O sistema deve inscrever o jogador como reserva quando todas as vagas de titulares da partida estiverem preenchidas. | Alta | RF06 |
| RF08 | O sistema deve permitir que o jogador cancele sua presença em uma partida. | Alta | RF06 |
| RF09 | O sistema deve promover automaticamente o primeiro reserva da fila para titular quando um titular cancelar sua presença. | Alta | RF07, RF08 |
| RF10 | O sistema deve exibir a lista da partida com titulares, reservas e quantidade de vagas restantes. | Alta | RF06 |
| RF11 | O sistema deve permitir que o organizador sorteie aleatoriamente os times entre os titulares confirmados. | Alta | RF06 |
| RF12 | O sistema deve permitir que o jogador informe o pagamento de sua parte anexando o comprovante. | Média | RF06 |
| RF13 | O sistema deve permitir que o organizador confirme ou registre manualmente o pagamento de um jogador. | Alta | RF06 |
| RF14 | O sistema deve exibir ao organizador a lista de jogadores com pagamento pendente em cada partida. | Alta | RF13 |
| RF15 | O sistema deve permitir que o organizador registre o placar final da partida. | Média | RF11 |
| RF16 | O sistema deve exibir o perfil do jogador com seu histórico de partidas disputadas e pendências financeiras. | Baixa | RF15 |

## 3. Requisitos Não Funcionais

| ID | Descrição | Categoria | Prioridade | Depende de |
|---|---|---|---|---|
| RNF01 | O sistema deve ter interface responsiva, adaptada para uso em smartphones, já que o acesso principal ocorre pelo link compartilhado no WhatsApp. | Usabilidade | Alta | RF04 |
| RNF02 | O jogador deve conseguir confirmar presença em no máximo 2 toques após abrir o link de convite, estando autenticado. | Usabilidade | Média | RF06 |
| RNF03 | O sistema deve processar a confirmação e o cancelamento de presença em no máximo 2 segundos. | Desempenho | Média | RF06, RF08 |
| RNF04 | Confirmações de presença simultâneas não podem resultar em mais inscritos do que o número de vagas da partida. | Confiabilidade | Alta | RF06, RF07 |
| RNF05 | As senhas dos usuários devem ser armazenadas de forma criptografada (hash), nunca em texto puro. | Segurança | Alta | RF01 |
| RNF06 | Apenas o organizador da partida pode cancelá-la, sortear os times, confirmar pagamentos e registrar o placar. | Segurança | Alta | RF05, RF11, RF13, RF15 |
| RNF07 | O comprovante de pagamento deve ser aceito nos formatos JPG, PNG ou PDF, com tamanho máximo de 5 MB. | Interface | Baixa | RF12 |

## 4. Regras de Negócio

| ID | Descrição | Prioridade | Depende de |
|---|---|---|---|
| RN01 | Uma partida não aceita mais titulares do que o número de vagas definido. Com os titulares completos, novos inscritos entram como reservas; com as reservas também completas, novas inscrições não são aceitas. | Alta | RF06, RF07 |
| RN02 | A fila de reservas segue a ordem de inscrição: quem se inscreveu primeiro é o primeiro a ser promovido a titular. | Alta | RF07, RF09 |
| RN03 | O valor a ser pago por cada jogador é o valor total da quadra dividido pelo número de inscritos (titulares e reservas) no momento do sorteio dos times, arredondado para cima no centavo. Os reservas também pagam, pois revezam com os titulares durante a partida. | Alta | RF03, RF11, RF13 |
| RN04 | O jogador que cancelar sua presença com menos de 12 horas de antecedência e cuja vaga não for preenchida por outro jogador continua responsável pelo pagamento da sua parte. | Média | RF08, RF09, RN03 |
| RN05 | Após o sorteio dos times, as inscrições da partida são encerradas e não são aceitas novas confirmações. | Alta | RF06, RF11 |
| RN06 | No sorteio, os jogadores com posição preferida de goleiro devem ser distribuídos um por time, enquanto houver goleiros disponíveis. | Média | RF01, RF11 |

## 5. Requisitos Suplementares

| ID | Descrição | Categoria | Prioridade | Depende de |
|---|---|---|---|---|
| RS01 | O sistema deve estar em conformidade com a LGPD no tratamento dos dados pessoais dos usuários (nome, telefone e e-mail). | Legal | Média | RF01 |
| RS02 | O sistema deve ser acessado pelo navegador, sem necessidade de instalação de aplicativo. | Instalação | Média | RF04 |
| RS03 | A interface do sistema deve estar em português brasileiro. | Internacionalização | Baixa | — |

---

# Parte II — Casos de Uso

## 6. Diagrama de Casos de Uso

![Diagrama de Casos de Uso](diagramas/casos_de_uso.png)

> Fonte do diagrama (PlantUML): [casos_de_uso.puml](diagramas/casos_de_uso.puml)

**Atores**

| Ator | Descrição |
|---|---|
| Jogador | Usuário que se inscreve nas partidas, cancela sua presença, informa pagamentos e acompanha seu perfil. |
| Organizador | Jogador responsável por criar e gerenciar a partida: sorteia os times, confirma pagamentos e registra o placar. Herda todos os casos de uso do Jogador (generalização). |

**Rastreabilidade: casos de uso × requisitos**

| Caso de uso | Ator(es) | Requisitos / Regras |
|---|---|---|
| UC01 - Cadastrar-se | Jogador | RF01 |
| UC02 - Autenticar-se | Jogador | RF02 |
| UC03 - Criar partida | Organizador | RF03 |
| UC04 - Gerar link de convite | — (incluído em UC03) | RF04 |
| UC05 - Cancelar partida | Organizador | RF05 |
| UC06 - Visualizar lista da partida | Jogador | RF10 |
| UC07 - Confirmar presença | Jogador | RF06, RN01, RN05 |
| UC08 - Entrar como reserva | — (estende UC07) | RF07, RN01 |
| UC09 - Cancelar presença | Jogador | RF08, RN04 |
| UC10 - Promover reserva | — (estende UC09) | RF09, RN02 |
| UC11 - Sortear times | Organizador | RF11, RN05, RN06 |
| UC12 - Calcular valor por jogador | — (incluído em UC11) | RN03 |
| UC13 - Registrar placar | Organizador | RF15 |
| UC14 - Informar pagamento | Jogador | RF12 |
| UC15 - Confirmar pagamento | Organizador | RF13 |
| UC16 - Consultar pendências | Organizador | RF14 |
| UC17 - Visualizar perfil | Jogador | RF16 |

## 7. Documentação dos Casos de Uso

> Convenções: **FA** = fluxo alternativo, numerado pelo passo do fluxo principal em que ocorre (ex.: FA 4a ocorre no passo 4). A situação da partida segue: *Inscrições abertas* → *Lotada* → *Times sorteados* → *Encerrada*, ou *Cancelada*.

### UC01 - Cadastrar-se

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador |
| **Requisitos** | RF01, RNF05, RS01 |
| **Pré-condições** | O usuário não possui cadastro no sistema. |
| **Pós-condições** | O usuário está cadastrado e pode se autenticar. |

**Fluxo principal**
1. O usuário acessa a opção "Criar conta".
2. O sistema exibe o formulário de cadastro.
3. O usuário informa nome, telefone, e-mail, senha e posição preferida (linha ou goleiro) e aceita os termos de uso de dados.
4. O sistema valida os dados.
5. O sistema armazena o cadastro, com a senha criptografada.
6. O sistema informa que o cadastro foi realizado e direciona o usuário para a autenticação.

**Fluxos alternativos**
- **FA 4a — E-mail já cadastrado:** o sistema informa que o e-mail já está em uso e retorna ao passo 3.
- **FA 4b — Dados obrigatórios ausentes ou inválidos:** o sistema destaca os campos com problema e retorna ao passo 3.

### UC02 - Autenticar-se

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF02 |
| **Pré-condições** | O usuário possui cadastro no sistema. |
| **Pós-condições** | O usuário está autenticado e tem acesso às funcionalidades do seu perfil. |

**Fluxo principal**
1. O usuário acessa o sistema (diretamente ou pelo link de convite de uma partida).
2. O sistema solicita e-mail e senha.
3. O usuário informa e-mail e senha.
4. O sistema valida as credenciais.
5. O sistema autentica o usuário e o direciona para a página inicial ou para a partida do link de convite.

**Fluxos alternativos**
- **FA 4a — Credenciais inválidas:** o sistema informa que e-mail ou senha estão incorretos e retorna ao passo 3.
- **FA 1a — Usuário sem cadastro:** o usuário escolhe "Criar conta" e é executado o UC01.

### UC03 - Criar partida

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF03, RF04 |
| **Pré-condições** | O organizador está autenticado. |
| **Pós-condições** | A partida está cadastrada com situação *Inscrições abertas*, possui um link de convite e o organizador consta como seu responsável. |

**Fluxo principal**
1. O organizador acessa a opção "Nova partida".
2. O sistema exibe o formulário da partida.
3. O organizador informa data, horário, local, modalidade (futsal, society ou campo), número de vagas para titulares, número de vagas para reservas e valor total da quadra.
4. O sistema valida os dados.
5. O sistema cadastra a partida com situação *Inscrições abertas*.
6. O sistema executa o UC04 - Gerar link de convite (**include**).
7. O sistema exibe a partida criada com o link de convite e a opção de compartilhá-lo.

**Fluxos alternativos**
- **FA 4a — Data e horário no passado:** o sistema informa que a partida deve ser marcada para uma data futura e retorna ao passo 3.
- **FA 4b — Número de vagas ou valor inválido:** se o número de vagas para titulares for menor que 2, o número de reservas for negativo ou o valor da quadra for menor ou igual a zero, o sistema informa o erro e retorna ao passo 3.

### UC04 - Gerar link de convite

| Campo | Descrição |
|---|---|
| **Ator(es)** | Nenhum ator direto (incluído em UC03) |
| **Requisitos** | RF04 |
| **Pré-condições** | A partida foi cadastrada (passo 5 do UC03). |
| **Pós-condições** | A partida possui um link de convite único. |

**Fluxo principal**
1. O sistema gera um código único para a partida.
2. O sistema monta o link de convite a partir desse código.
3. O sistema associa o link à partida e o devolve ao UC03.

**Fluxos alternativos**
- **FA 1a — Código já existente:** o sistema gera um novo código e repete o passo 1.

### UC05 - Cancelar partida

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF05, RNF06 |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida ainda não foi iniciada nem cancelada. |
| **Pós-condições** | A partida está com situação *Cancelada* e não aceita mais inscrições, sorteio ou pagamentos. |

**Fluxo principal**
1. O organizador acessa a partida e escolhe "Cancelar partida".
2. O sistema solicita a confirmação do cancelamento.
3. O organizador confirma.
4. O sistema altera a situação da partida para *Cancelada*.
5. O sistema exibe a partida como cancelada para todos os inscritos.

**Fluxos alternativos**
- **FA 3a — Organizador desiste:** o organizador não confirma e o caso de uso é encerrado sem alterações.
- **FA 1a — Usuário não é o organizador:** o sistema não exibe a opção de cancelamento (RNF06).

### UC06 - Visualizar lista da partida

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF10 |
| **Pré-condições** | O jogador está autenticado e possui o link de convite da partida. |
| **Pós-condições** | Nenhuma alteração no sistema. |

**Fluxo principal**
1. O jogador acessa a partida pelo link de convite.
2. O sistema exibe data, horário, local, modalidade e situação da partida.
3. O sistema exibe a lista de titulares e a fila de reservas, na ordem de inscrição.
4. O sistema exibe a quantidade de vagas restantes para titulares e reservas.

**Fluxos alternativos**
- **FA 3a — Times já sorteados:** além da lista, o sistema exibe a composição de cada time e o valor por jogador.
- **FA 1a — Link inválido:** o sistema informa que a partida não foi encontrada.

### UC07 - Confirmar presença

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF06, RN01, RN05, RNF02, RNF03, RNF04 |
| **Pré-condições** | O jogador está autenticado, possui o link de convite e ainda não está inscrito na partida. |
| **Pós-condições** | O jogador está inscrito na partida como titular ou como reserva. |

**Fluxo principal**
1. O jogador acessa a partida pelo link de convite.
2. O sistema exibe os dados da partida e a opção "Confirmar presença".
3. O jogador escolhe "Confirmar presença".
4. O sistema verifica se há vaga de titular.
5. O sistema inscreve o jogador como titular, registrando a data e a hora da inscrição.
6. O sistema exibe a lista atualizada, com o jogador entre os titulares.

**Fluxos alternativos**
- **FA 4a — Titulares completos:** o sistema executa o UC08 - Entrar como reserva (**extend**).
- **FA 4b — Titulares e reservas completos:** o sistema informa que a partida está lotada e não realiza a inscrição (RN01).
- **FA 2a — Inscrições encerradas:** se os times já foram sorteados ou a partida foi cancelada, o sistema não exibe a opção de confirmar e informa o motivo (RN05).
- **FA 4c — Duas confirmações simultâneas para a última vaga:** o sistema inscreve apenas o primeiro pedido processado; o outro segue o FA 4a ou o FA 4b (RNF04).

### UC08 - Entrar como reserva

| Campo | Descrição |
|---|---|
| **Ator(es)** | Nenhum ator direto (estende UC07) |
| **Requisitos** | RF07, RN01, RN02 |
| **Ponto de extensão** | Passo 4 do UC07, quando as vagas de titulares estão completas. |
| **Pré-condições** | As vagas de titulares estão completas e há vaga de reserva. |
| **Pós-condições** | O jogador está inscrito como reserva, no final da fila. |

**Fluxo principal**
1. O sistema informa ao jogador que as vagas de titulares estão completas.
2. O sistema inscreve o jogador como reserva, registrando a data e a hora da inscrição.
3. O sistema informa a posição do jogador na fila de reservas.
4. Se as vagas de reserva ficaram completas, o sistema altera a situação da partida para *Lotada*.

**Fluxos alternativos**
- Não há.

### UC09 - Cancelar presença

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF08, RN04 |
| **Pré-condições** | O jogador está autenticado e inscrito na partida. A partida ainda não foi iniciada nem cancelada. |
| **Pós-condições** | A inscrição do jogador está cancelada e sua vaga foi liberada ou ocupada por um reserva. |

**Fluxo principal**
1. O jogador acessa a partida e escolhe "Cancelar presença".
2. O sistema solicita a confirmação.
3. O jogador confirma.
4. O sistema cancela a inscrição do jogador.
5. O sistema verifica se o jogador era titular e se há reservas na fila.
6. O sistema exibe a lista atualizada.

**Fluxos alternativos**
- **FA 5a — Era titular e há reservas:** o sistema executa o UC10 - Promover reserva (**extend**).
- **FA 5b — Era titular e não há reservas:** a vaga de titular fica livre e, se a partida estava *Lotada*, volta para *Inscrições abertas*.
- **FA 4a — Cancelamento com menos de 12 horas de antecedência:** o sistema avisa o jogador que, se a vaga não for preenchida, ele continua responsável pelo pagamento da sua parte (RN04).
- **FA 3a — Jogador desiste:** o jogador não confirma e o caso de uso é encerrado sem alterações.

### UC10 - Promover reserva

| Campo | Descrição |
|---|---|
| **Ator(es)** | Nenhum ator direto (estende UC09) |
| **Requisitos** | RF09, RN02 |
| **Ponto de extensão** | Passo 5 do UC09, quando quem cancelou era titular e há reservas na fila. |
| **Pré-condições** | Um titular cancelou a presença e existe ao menos um reserva na fila. |
| **Pós-condições** | O primeiro reserva da fila passou a ser titular. |

**Fluxo principal**
1. O sistema identifica o primeiro reserva da fila, pela data e hora da inscrição (RN02).
2. O sistema altera a inscrição desse jogador de reserva para titular.
3. Se a partida estava *Lotada*, o sistema altera sua situação para *Inscrições abertas*, pois abriu uma vaga de reserva.

**Fluxos alternativos**
- **FA 2a — Times já sorteados:** o jogador promovido assume a vaga do titular que cancelou, no mesmo time. A partida continua com situação *Times sorteados*.

### UC11 - Sortear times

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF11, RN05, RN06, RNF06 |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida está com situação *Inscrições abertas* ou *Lotada* e possui ao menos 2 titulares. |
| **Pós-condições** | Os times estão definidos, a partida está com situação *Times sorteados*, as inscrições estão encerradas e o valor por jogador está calculado. |

**Fluxo principal**
1. O organizador acessa a partida e escolhe "Sortear times".
2. O sistema solicita a confirmação, informando que as inscrições serão encerradas.
3. O organizador confirma.
4. O sistema distribui os goleiros, um por time, enquanto houver goleiros disponíveis (RN06).
5. O sistema distribui aleatoriamente os demais titulares entre os times.
6. O sistema executa o UC12 - Calcular valor por jogador (**include**).
7. O sistema altera a situação da partida para *Times sorteados* (RN05).
8. O sistema exibe os times sorteados e o valor por jogador.

**Fluxos alternativos**
- **FA 3a — Organizador desiste:** o organizador não confirma e o caso de uso é encerrado sem alterações.
- **FA 4a — Nenhum goleiro inscrito:** o sistema pula o passo 4 e distribui todos os titulares aleatoriamente.
- **FA 8a — Organizador quer sortear novamente:** antes do início da partida, o organizador escolhe "Sortear de novo" e o fluxo retorna ao passo 4.

### UC12 - Calcular valor por jogador

| Campo | Descrição |
|---|---|
| **Ator(es)** | Nenhum ator direto (incluído em UC11) |
| **Requisitos** | RN03 |
| **Pré-condições** | Os times foram sorteados (passo 5 do UC11). |
| **Pós-condições** | Cada inscrito possui um pagamento pendente com o valor da sua parte. |

**Fluxo principal**
1. O sistema conta os inscritos da partida (titulares e reservas).
2. O sistema divide o valor total da quadra pelo número de inscritos, arredondando para cima no centavo.
3. O sistema registra, para cada inscrito, um pagamento com situação *Pendente* e o valor calculado.

**Fluxos alternativos**
- **FA 3a — Sorteio refeito (UC11, FA 8a):** se o número de inscritos não mudou, o sistema mantém os pagamentos já registrados.

### UC13 - Registrar placar

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF15, RNF06 |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida está com situação *Times sorteados* e a data e o horário da partida já passaram. |
| **Pós-condições** | O placar está registrado e a partida está com situação *Encerrada*. |

**Fluxo principal**
1. O organizador acessa a partida e escolhe "Registrar placar".
2. O sistema exibe os times sorteados.
3. O organizador informa a quantidade de gols de cada time.
4. O sistema valida os valores.
5. O sistema registra o placar e altera a situação da partida para *Encerrada*.
6. O sistema exibe o resultado final.

**Fluxos alternativos**
- **FA 4a — Valor inválido:** se algum valor for negativo ou não numérico, o sistema informa o erro e retorna ao passo 3.
- **FA 5a — Corrigir placar:** o organizador pode editar o placar de uma partida *Encerrada*; o fluxo retorna ao passo 3.

### UC14 - Informar pagamento

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF12, RNF07 |
| **Pré-condições** | O jogador está autenticado e possui um pagamento *Pendente* em uma partida (o valor é calculado no sorteio dos times). |
| **Pós-condições** | O pagamento está com situação *Informado*, com o comprovante anexado, aguardando a confirmação do organizador. |

**Fluxo principal**
1. O jogador acessa a partida ou seu perfil e escolhe "Informar pagamento".
2. O sistema exibe o valor a pagar.
3. O jogador anexa o comprovante.
4. O sistema valida o arquivo.
5. O sistema registra o comprovante e altera a situação do pagamento para *Informado*.
6. O sistema exibe o pagamento como aguardando confirmação do organizador.

**Fluxos alternativos**
- **FA 4a — Arquivo inválido:** se o arquivo não for JPG, PNG ou PDF, ou tiver mais de 5 MB, o sistema informa o erro e retorna ao passo 3 (RNF07).
- **FA 1a — Pagamento já confirmado:** o sistema informa que o pagamento já foi confirmado pelo organizador e não exibe a opção.

### UC15 - Confirmar pagamento

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF13, RNF06 |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida possui pagamentos *Pendentes* ou *Informados*. |
| **Pós-condições** | O pagamento do jogador está com situação *Confirmado*. |

**Fluxo principal**
1. O organizador acessa os pagamentos da partida.
2. O sistema lista os inscritos com o valor e a situação de cada pagamento.
3. O organizador seleciona um pagamento *Informado* e visualiza o comprovante.
4. O organizador escolhe "Confirmar".
5. O sistema altera a situação do pagamento para *Confirmado* e registra a data da confirmação.

**Fluxos alternativos**
- **FA 3a — Pagamento recebido fora do sistema (registro manual):** o organizador seleciona um pagamento *Pendente*, escolhe "Registrar pagamento" e o fluxo segue no passo 5, sem comprovante.
- **FA 4a — Comprovante recusado:** o organizador escolhe "Recusar"; o sistema volta o pagamento para *Pendente*.

### UC16 - Consultar pendências

| Campo | Descrição |
|---|---|
| **Ator(es)** | Organizador |
| **Requisitos** | RF14, RN04, RNF06 |
| **Pré-condições** | O organizador está autenticado e é o responsável por ao menos uma partida. |
| **Pós-condições** | Nenhuma alteração no sistema. |

**Fluxo principal**
1. O organizador acessa a opção "Pendências".
2. O sistema lista as partidas do organizador que possuem pagamentos não confirmados.
3. Para cada partida, o sistema exibe os jogadores com pagamento *Pendente* ou *Informado* e o valor devido.
4. O sistema exibe o total a receber.

**Fluxos alternativos**
- **FA 2a — Nenhuma pendência:** o sistema informa que todos os pagamentos estão confirmados.
- **FA 3a — Organizador seleciona um pagamento:** é executado o UC15 - Confirmar pagamento.

### UC17 - Visualizar perfil

| Campo | Descrição |
|---|---|
| **Ator(es)** | Jogador (e Organizador, por herança) |
| **Requisitos** | RF16 |
| **Pré-condições** | O jogador está autenticado. |
| **Pós-condições** | Nenhuma alteração no sistema. |

**Fluxo principal**
1. O jogador acessa a opção "Meu perfil".
2. O sistema exibe nome, telefone, e-mail e posição preferida.
3. O sistema exibe o histórico de partidas *Encerradas* das quais o jogador participou, com data, local, time e placar.
4. O sistema exibe os pagamentos do jogador que ainda não foram confirmados.

**Fluxos alternativos**
- **FA 3a — Nenhuma partida disputada:** o sistema informa que o jogador ainda não participou de partidas.
- **FA 4a — Nenhuma pendência:** o sistema informa que não há pagamentos pendentes.

---

# Parte III — Modelagem

## 8. Diagrama de Classes — Modelo Conceitual

![Diagrama de Classes — Modelo Conceitual](diagramas/classes_conceitual.png)

> Fonte do diagrama (PlantUML): [classes_conceitual.puml](diagramas/classes_conceitual.puml)

O modelo conceitual representa as entidades do domínio e seus relacionamentos, sem detalhes de implementação (tipos, métodos e navegabilidade são definidos no modelo de domínio).

**Classes**

| Classe | Descrição | Origem |
|---|---|---|
| Jogador | Pessoa cadastrada no sistema. Um jogador que cria partidas atua como organizador delas. | RF01, RF02 |
| Partida | Jogo marcado em uma data, horário e local, com limite de vagas e valor da quadra. | RF03, RF04, RF05 |
| Inscricao | Participação de um jogador em uma partida, como titular ou reserva. Guarda a data e a hora da inscrição, que definem a ordem da fila de reservas. | RF06–RF09, RN01, RN02 |
| Time | Equipe formada no sorteio, com o número de gols marcados na partida. | RF11, RF15, RN06 |
| Pagamento | Parte do valor da quadra devida por um inscrito, com o comprovante e a situação (pendente, informado ou confirmado). | RF12–RF14, RN03, RN04 |

**Associações**

| Associação | Multiplicidade | Significado |
|---|---|---|
| Jogador *organiza* Partida | 1 — 0..* | Toda partida tem um organizador; um jogador pode organizar nenhuma ou várias partidas. |
| Jogador *realiza* Inscricao | 1 — 0..* | Cada inscrição pertence a um jogador; um jogador pode se inscrever em várias partidas. |
| Partida *possui* Inscricao | 1 — 0..* | Cada inscrição é de uma partida; a partida começa sem inscritos. |
| Partida *é dividida em* Time | 1 — 0..* | Os times só existem após o sorteio, por isso a partida pode ter zero times. |
| Inscricao *compõe* Time | 0..* — 0..1 | Um time é composto por inscrições de titulares; reservas e inscrições anteriores ao sorteio não pertencem a nenhum time. |
| Inscricao *gera* Pagamento | 1 — 0..1 | O pagamento é criado no sorteio (RN03), por isso a inscrição pode ainda não ter pagamento. |

**Decisões de modelagem**

- **Organizador não é uma classe separada.** No diagrama de casos de uso, Organizador é uma especialização de Jogador. No domínio, ser organizador é um papel, representado pela associação *organiza*: o mesmo jogador pode organizar uma partida e jogar como inscrito em outra.
- **Inscricao é uma classe, e não apenas uma lista de jogadores na partida**, porque a participação tem dados próprios (data e hora, tipo e situação) e se relaciona com Time e Pagamento.
- **O pagamento é por inscrição, e não por jogador**, porque o valor é calculado para cada partida (RN03).

## 9. Diagrama de Classes — Modelo de Domínio

## 10. Segundo Diagrama UML

---

# Parte IV — Protótipo

## 11. Mapa do Site

## 12. Telas

---

## 13. Considerações Finais

## 14. Referências
