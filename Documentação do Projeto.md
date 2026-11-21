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

### 1.4 Escopo do Sistema

**Público-alvo:** organizadores e jogadores de grupos de futebol amador (futsal, society e campo).

**Contexto de uso:** o organizador cria a partida no sistema e compartilha o link de convite no grupo de WhatsApp; os jogadores acessam pelo celular para confirmar presença, acompanhar a lista e informar seus pagamentos.

**Funcionalidades contempladas:** cadastro e autenticação de usuários; criação e cancelamento de partidas com link de convite; confirmação e cancelamento de presença, com fila de reservas e promoção automática; sorteio aleatório dos times; cálculo do valor por jogador; registro e controle de pagamentos; registro do placar; perfil do jogador com histórico e pendências.

**Fora do escopo:** pagamento online (Pix, cartão ou integração bancária); reserva de quadra junto ao dono do espaço; organização de campeonatos; notificações (e-mail, push ou WhatsApp); grupos fixos e mensalistas. Esses itens são candidatos a melhorias futuras.

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
| RN04 | O jogador que cancelar sua presença após o sorteio dos times continua responsável pelo pagamento da sua parte, pois o valor por jogador já foi calculado. | Média | RF08, RF11, RN03 |
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

> Especificação no modelo da disciplina (baseado em BEZERRA, 2014). **Fluxos alternativos (FA)** são caminhos válidos diferentes do fluxo principal; **fluxos de exceção (FE)** tratam erros ou situações que impedem o objetivo do caso de uso. Cada fluxo indica o passo do fluxo principal em que ocorre. A situação da partida segue: *Inscrições abertas* → *Lotada* → *Times sorteados* → *Encerrada*, ou *Cancelada*.

### UC01 - Cadastrar-se

| **Caso de uso** | UC01 - Cadastrar-se |
|---|---|
| **Ator principal** | Jogador |
| **Atores secundários** | — |
| **Resumo** | O usuário cria sua conta no sistema informando seus dados pessoais e sua posição preferida. |
| **Pré-condições** | O usuário não possui cadastro no sistema. |
| **Pós-condições** | O usuário está cadastrado e pode se autenticar. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O usuário acessa a opção "Criar conta".<br>2. O sistema exibe o formulário de cadastro.<br>3. O usuário informa nome, telefone, e-mail, senha e posição preferida (linha ou goleiro) e aceita os termos de uso de dados.<br>4. O sistema valida os dados.<br>5. O sistema armazena o cadastro, com a senha criptografada.<br>6. O sistema informa que o cadastro foi realizado e direciona o usuário para a autenticação. |
| **FLUXOS ALTERNATIVOS** | |
| — | Não há. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — E-mail já cadastrado** | No passo 4, o sistema informa que o e-mail já está em uso e retorna ao passo 3. |
| **FE02 — Dados ausentes ou inválidos** | No passo 4, o sistema destaca os campos obrigatórios não preenchidos ou inválidos e retorna ao passo 3. |
| **Requisitos relacionados** | RF01, RNF05, RS01 |

### UC02 - Autenticar-se

| **Caso de uso** | UC02 - Autenticar-se |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O usuário cadastrado entra no sistema informando e-mail e senha. |
| **Pré-condições** | O usuário possui cadastro no sistema. |
| **Pós-condições** | O usuário está autenticado e tem acesso às funcionalidades do seu perfil. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O usuário acessa o sistema, diretamente ou pelo link de convite de uma partida.<br>2. O sistema solicita e-mail e senha.<br>3. O usuário informa e-mail e senha.<br>4. O sistema valida as credenciais.<br>5. O sistema autentica o usuário e o direciona para a página inicial ou para a partida do link de convite. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Usuário sem cadastro** | No passo 2, o usuário escolhe "Criar conta" e é executado o UC01 - Cadastrar-se. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Credenciais inválidas** | No passo 4, o sistema informa que e-mail ou senha estão incorretos e retorna ao passo 3. |
| **Requisitos relacionados** | RF02 |

### UC03 - Criar partida

| **Caso de uso** | UC03 - Criar partida |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | O organizador cadastra uma nova partida com data, local, vagas e valor da quadra, e recebe o link de convite para compartilhar. |
| **Pré-condições** | O organizador está autenticado. |
| **Pós-condições** | A partida está cadastrada com situação *Inscrições abertas*, possui um link de convite e o organizador consta como seu responsável. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa a opção "Nova partida".<br>2. O sistema exibe o formulário da partida.<br>3. O organizador informa data, horário, local, modalidade (futsal, society ou campo), número de vagas para titulares, número de vagas para reservas e valor total da quadra.<br>4. O sistema valida os dados.<br>5. O sistema cadastra a partida com situação *Inscrições abertas*.<br>6. O sistema executa o UC04 - Gerar link de convite (**include**).<br>7. O sistema exibe a partida criada com o link de convite e a opção de compartilhá-lo. |
| **FLUXOS ALTERNATIVOS** | |
| — | Não há. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Data e horário no passado** | No passo 4, o sistema informa que a partida deve ser marcada para uma data futura e retorna ao passo 3. |
| **FE02 — Vagas ou valor inválidos** | No passo 4, se o número de vagas para titulares for menor que 2, o número de reservas for negativo ou o valor da quadra for menor ou igual a zero, o sistema informa o erro e retorna ao passo 3. |
| **Requisitos relacionados** | RF03, RF04 |

### UC04 - Gerar link de convite

| **Caso de uso** | UC04 - Gerar link de convite |
|---|---|
| **Ator principal** | — (incluído em UC03 - Criar partida) |
| **Atores secundários** | — |
| **Resumo** | O sistema gera um link único para a partida, que será compartilhado com os jogadores. |
| **Pré-condições** | A partida foi cadastrada (passo 5 do UC03). |
| **Pós-condições** | A partida possui um link de convite único. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O sistema gera um código único para a partida.<br>2. O sistema monta o link de convite a partir desse código.<br>3. O sistema associa o link à partida e retorna ao UC03. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Código já existente** | No passo 1, se o código gerado já pertencer a outra partida, o sistema gera um novo código e repete o passo 1. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF04 |

### UC05 - Cancelar partida

| **Caso de uso** | UC05 - Cancelar partida |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | O organizador cancela uma partida que ainda não aconteceu. |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida ainda não foi iniciada nem cancelada. |
| **Pós-condições** | A partida está com situação *Cancelada* e não aceita mais inscrições, sorteio ou pagamentos. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa a partida e escolhe "Cancelar partida".<br>2. O sistema solicita a confirmação do cancelamento.<br>3. O organizador confirma.<br>4. O sistema altera a situação da partida para *Cancelada*.<br>5. O sistema exibe a partida como cancelada para todos os inscritos. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Organizador desiste** | No passo 3, o organizador não confirma e o caso de uso é encerrado sem alterações. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Usuário não é o organizador** | No passo 1, se o usuário não for o responsável pela partida, o sistema não exibe a opção de cancelamento (RNF06). |
| **Requisitos relacionados** | RF05, RNF06 |

### UC06 - Visualizar lista da partida

| **Caso de uso** | UC06 - Visualizar lista da partida |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O jogador consulta os dados da partida, os titulares, a fila de reservas e as vagas restantes. |
| **Pré-condições** | O jogador está autenticado e possui o link de convite da partida. |
| **Pós-condições** | Nenhuma alteração no sistema. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O jogador acessa a partida pelo link de convite.<br>2. O sistema exibe data, horário, local, modalidade e situação da partida.<br>3. O sistema exibe a lista de titulares e a fila de reservas, na ordem de inscrição.<br>4. O sistema exibe a quantidade de vagas restantes para titulares e reservas. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Times já sorteados** | No passo 3, além da lista, o sistema exibe a composição de cada time e o valor por jogador. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Link inválido** | No passo 1, se o link não corresponder a nenhuma partida, o sistema informa que a partida não foi encontrada. |
| **Requisitos relacionados** | RF10 |

### UC07 - Confirmar presença

| **Caso de uso** | UC07 - Confirmar presença |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O jogador se inscreve na partida pelo link de convite, ocupando uma vaga de titular ou, se não houver, de reserva. |
| **Pré-condições** | O jogador está autenticado, possui o link de convite e ainda não está inscrito na partida. |
| **Pós-condições** | O jogador está inscrito na partida como titular ou como reserva. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O jogador acessa a partida pelo link de convite.<br>2. O sistema exibe os dados da partida e a opção "Confirmar presença".<br>3. O jogador escolhe "Confirmar presença".<br>4. O sistema verifica se há vaga de titular.<br>5. O sistema inscreve o jogador como titular, registrando a data e a hora da inscrição.<br>6. O sistema exibe a lista atualizada, com o jogador entre os titulares. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Titulares completos** | No passo 4, se não houver vaga de titular, o sistema executa o UC08 - Entrar como reserva (**extend**). |
| **FA02 — Confirmações simultâneas para a última vaga** | No passo 4, se dois jogadores confirmarem ao mesmo tempo, o sistema inscreve apenas o primeiro pedido processado; o outro segue o FA01 ou o FE01 (RNF04). |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Partida lotada** | No passo 4, se titulares e reservas estiverem completos, o sistema informa que a partida está lotada e não realiza a inscrição (RN01). |
| **FE02 — Inscrições encerradas** | No passo 2, se os times já foram sorteados ou a partida foi cancelada, o sistema não exibe a opção de confirmar e informa o motivo (RN05). |
| **Requisitos relacionados** | RF06, RN01, RN05, RNF02, RNF03, RNF04 |

### UC08 - Entrar como reserva

| **Caso de uso** | UC08 - Entrar como reserva |
|---|---|
| **Ator principal** | — (estende UC07 - Confirmar presença) |
| **Atores secundários** | — |
| **Resumo** | Quando as vagas de titulares estão completas, o sistema inscreve o jogador no final da fila de reservas. Ponto de extensão: passo 4 do UC07. |
| **Pré-condições** | As vagas de titulares estão completas e há vaga de reserva. |
| **Pós-condições** | O jogador está inscrito como reserva, no final da fila. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O sistema informa ao jogador que as vagas de titulares estão completas.<br>2. O sistema inscreve o jogador como reserva, registrando a data e a hora da inscrição.<br>3. O sistema informa a posição do jogador na fila de reservas. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Reservas completas após a inscrição** | No passo 2, se a inscrição preencher a última vaga de reserva, o sistema altera a situação da partida para *Lotada* (RN01). |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF07, RN01, RN02 |

### UC09 - Cancelar presença

| **Caso de uso** | UC09 - Cancelar presença |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O jogador desiste da partida, liberando sua vaga para um reserva ou para novas inscrições. |
| **Pré-condições** | O jogador está autenticado e inscrito na partida. A partida ainda não foi iniciada nem cancelada. |
| **Pós-condições** | A inscrição do jogador está cancelada e sua vaga foi liberada ou ocupada por um reserva. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O jogador acessa a partida e escolhe "Cancelar presença".<br>2. O sistema solicita a confirmação.<br>3. O jogador confirma.<br>4. O sistema cancela a inscrição do jogador.<br>5. O sistema verifica se o jogador era titular e se há reservas na fila.<br>6. O sistema exibe a lista atualizada. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Era titular e há reservas** | No passo 5, o sistema executa o UC10 - Promover reserva (**extend**). |
| **FA02 — Era titular e não há reservas** | No passo 5, a vaga de titular fica livre e, se a partida estava *Lotada*, volta para *Inscrições abertas*. |
| **FA03 — Cancelamento após o sorteio** | No passo 2, se os times já foram sorteados, o sistema avisa que o jogador continua responsável pelo pagamento da sua parte (RN04). No passo 4, o pagamento já registrado para a inscrição é mantido. |
| **FA04 — Jogador desiste** | No passo 3, o jogador não confirma e o caso de uso é encerrado sem alterações. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Partida já iniciada ou encerrada** | No passo 1, se a partida já começou ou foi encerrada, o sistema não exibe a opção de cancelar presença. |
| **Requisitos relacionados** | RF08, RN04 |

### UC10 - Promover reserva

| **Caso de uso** | UC10 - Promover reserva |
|---|---|
| **Ator principal** | — (estende UC09 - Cancelar presença) |
| **Atores secundários** | — |
| **Resumo** | Quando um titular cancela, o sistema passa o primeiro reserva da fila para titular. Ponto de extensão: passo 5 do UC09. |
| **Pré-condições** | Um titular cancelou a presença e existe ao menos um reserva na fila. |
| **Pós-condições** | O primeiro reserva da fila passou a ser titular. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O sistema identifica o primeiro reserva da fila, pela data e hora da inscrição (RN02).<br>2. O sistema altera a inscrição desse jogador de reserva para titular.<br>3. Se a partida estava *Lotada*, o sistema altera sua situação para *Inscrições abertas*, pois abriu uma vaga de reserva. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Times já sorteados** | No passo 2, o jogador promovido assume a vaga do titular que cancelou, no mesmo time, e a partida continua com situação *Times sorteados*. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF09, RN02 |

### UC11 - Sortear times

| **Caso de uso** | UC11 - Sortear times |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | O organizador sorteia aleatoriamente os titulares entre os times, o que encerra as inscrições e define o valor por jogador. |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida está com situação *Inscrições abertas* ou *Lotada*. |
| **Pós-condições** | Os times estão definidos, a partida está com situação *Times sorteados*, as inscrições estão encerradas e o valor por jogador está calculado. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa a partida e escolhe "Sortear times".<br>2. O sistema solicita a confirmação, informando que as inscrições serão encerradas.<br>3. O organizador confirma.<br>4. O sistema distribui os goleiros, um por time, enquanto houver goleiros disponíveis (RN06).<br>5. O sistema distribui aleatoriamente os demais titulares entre os times.<br>6. O sistema executa o UC12 - Calcular valor por jogador (**include**).<br>7. O sistema altera a situação da partida para *Times sorteados* (RN05).<br>8. O sistema exibe os times sorteados e o valor por jogador. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Organizador desiste** | No passo 3, o organizador não confirma e o caso de uso é encerrado sem alterações. |
| **FA02 — Nenhum goleiro inscrito** | No passo 4, o sistema pula a distribuição de goleiros e distribui todos os titulares aleatoriamente. |
| **FA03 — Sortear novamente** | No passo 8, antes do início da partida, o organizador escolhe "Sortear de novo" e o fluxo retorna ao passo 4. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Titulares insuficientes** | No passo 1, se a partida tiver menos de 2 titulares, o sistema informa que não é possível sortear os times. |
| **Requisitos relacionados** | RF11, RN05, RN06, RNF06 |

### UC12 - Calcular valor por jogador

| **Caso de uso** | UC12 - Calcular valor por jogador |
|---|---|
| **Ator principal** | — (incluído em UC11 - Sortear times) |
| **Atores secundários** | — |
| **Resumo** | O sistema divide o valor da quadra entre todos os inscritos e registra o pagamento pendente de cada um. |
| **Pré-condições** | Os times foram sorteados (passo 5 do UC11). |
| **Pós-condições** | Cada inscrito possui um pagamento *Pendente* com o valor da sua parte. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O sistema conta os inscritos da partida (titulares e reservas).<br>2. O sistema divide o valor total da quadra pelo número de inscritos, arredondando para cima no centavo (RN03).<br>3. O sistema registra, para cada inscrito, um pagamento com situação *Pendente* e o valor calculado. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Sorteio refeito** | No passo 3, se o sorteio foi refeito (UC11, FA03) e o número de inscritos não mudou, o sistema mantém os pagamentos já registrados. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RN03 |

### UC13 - Registrar placar

| **Caso de uso** | UC13 - Registrar placar |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | Após o jogo, o organizador informa os gols de cada time e encerra a partida. |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida está com situação *Times sorteados* e a data e o horário da partida já passaram. |
| **Pós-condições** | O placar está registrado e a partida está com situação *Encerrada*. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa a partida e escolhe "Registrar placar".<br>2. O sistema exibe os times sorteados.<br>3. O organizador informa a quantidade de gols de cada time.<br>4. O sistema valida os valores.<br>5. O sistema registra o placar e altera a situação da partida para *Encerrada*.<br>6. O sistema exibe o resultado final. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Corrigir placar** | No passo 1, se a partida já estiver *Encerrada*, o organizador escolhe "Editar placar" e o fluxo segue a partir do passo 2. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Valor inválido** | No passo 4, se algum valor for negativo ou não numérico, o sistema informa o erro e retorna ao passo 3. |
| **Requisitos relacionados** | RF15, RNF06 |

### UC14 - Informar pagamento

| **Caso de uso** | UC14 - Informar pagamento |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O jogador anexa o comprovante do pagamento da sua parte para que o organizador confirme. |
| **Pré-condições** | O jogador está autenticado e possui um pagamento *Pendente* em uma partida (o valor é calculado no sorteio dos times). |
| **Pós-condições** | O pagamento está com situação *Informado*, com o comprovante anexado, aguardando a confirmação do organizador. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O jogador acessa a partida ou seu perfil e escolhe "Informar pagamento".<br>2. O sistema exibe o valor a pagar.<br>3. O jogador anexa o comprovante.<br>4. O sistema valida o arquivo.<br>5. O sistema registra o comprovante e altera a situação do pagamento para *Informado*.<br>6. O sistema exibe o pagamento como aguardando confirmação do organizador. |
| **FLUXOS ALTERNATIVOS** | |
| — | Não há. |
| **FLUXOS DE EXCEÇÃO** | |
| **FE01 — Arquivo inválido** | No passo 4, se o arquivo não for JPG, PNG ou PDF, ou tiver mais de 5 MB, o sistema informa o erro e retorna ao passo 3 (RNF07). |
| **FE02 — Pagamento já confirmado** | No passo 1, se o pagamento já foi confirmado pelo organizador, o sistema informa isso e não exibe a opção. |
| **Requisitos relacionados** | RF12, RNF07 |

### UC15 - Confirmar pagamento

| **Caso de uso** | UC15 - Confirmar pagamento |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | O organizador confere o comprovante de um jogador e confirma o pagamento, ou registra manualmente um pagamento recebido fora do sistema. |
| **Pré-condições** | O organizador está autenticado e é o responsável pela partida. A partida possui pagamentos *Pendentes* ou *Informados*. |
| **Pós-condições** | O pagamento do jogador está com situação *Confirmado*. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa os pagamentos da partida.<br>2. O sistema lista os inscritos com o valor e a situação de cada pagamento.<br>3. O organizador seleciona um pagamento *Informado* e visualiza o comprovante.<br>4. O organizador escolhe "Confirmar".<br>5. O sistema altera a situação do pagamento para *Confirmado* e registra a data da confirmação. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Registro manual** | No passo 3, se o jogador pagou fora do sistema, o organizador seleciona um pagamento *Pendente*, escolhe "Registrar pagamento" e o fluxo segue no passo 5, sem comprovante. |
| **FA02 — Comprovante recusado** | No passo 4, o organizador escolhe "Recusar" e o sistema volta o pagamento para *Pendente*. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF13, RNF06 |

### UC16 - Consultar pendências

| **Caso de uso** | UC16 - Consultar pendências |
|---|---|
| **Ator principal** | Organizador |
| **Atores secundários** | — |
| **Resumo** | O organizador consulta quem ainda não pagou em cada uma das suas partidas e o total a receber. |
| **Pré-condições** | O organizador está autenticado e é o responsável por ao menos uma partida. |
| **Pós-condições** | Nenhuma alteração no sistema. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O organizador acessa a opção "Pendências".<br>2. O sistema lista as partidas do organizador que possuem pagamentos não confirmados.<br>3. Para cada partida, o sistema exibe os jogadores com pagamento *Pendente* ou *Informado* e o valor devido.<br>4. O sistema exibe o total a receber. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Nenhuma pendência** | No passo 2, se não houver pagamentos não confirmados, o sistema informa que todos os pagamentos estão confirmados. |
| **FA02 — Confirmar a partir das pendências** | No passo 3, o organizador seleciona um pagamento e é executado o UC15 - Confirmar pagamento. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF14, RN04, RNF06 |

### UC17 - Visualizar perfil

| **Caso de uso** | UC17 - Visualizar perfil |
|---|---|
| **Ator principal** | Jogador (e Organizador, por herança) |
| **Atores secundários** | — |
| **Resumo** | O jogador consulta seus dados, seu histórico de partidas e seus pagamentos pendentes. |
| **Pré-condições** | O jogador está autenticado. |
| **Pós-condições** | Nenhuma alteração no sistema. |
| **FLUXO PRINCIPAL** | |
| **Fluxo principal** | 1. O jogador acessa a opção "Meu perfil".<br>2. O sistema exibe nome, telefone, e-mail e posição preferida.<br>3. O sistema exibe o histórico de partidas *Encerradas* das quais o jogador participou, com data, local, time e placar.<br>4. O sistema exibe os pagamentos do jogador que ainda não foram confirmados. |
| **FLUXOS ALTERNATIVOS** | |
| **FA01 — Nenhuma partida disputada** | No passo 3, o sistema informa que o jogador ainda não participou de partidas. |
| **FA02 — Nenhuma pendência** | No passo 4, o sistema informa que não há pagamentos pendentes. |
| **FLUXOS DE EXCEÇÃO** | |
| — | Não há. |
| **Requisitos relacionados** | RF16 |

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

![Diagrama de Classes — Modelo de Domínio](diagramas/classes_dominio.png)

> Fonte do diagrama (PlantUML): [classes_dominio.puml](diagramas/classes_dominio.puml)

O modelo de domínio detalha o modelo conceitual com os tipos dos atributos, os métodos relevantes, as multiplicidades e a navegabilidade das associações.

**Convenções**

- `-` atributo privado; `+` método público.
- Associação **sem seta**: navegável nos dois sentidos. Associação **com seta**: navegável apenas no sentido da seta.
- **Losango preenchido** (composição): a parte só existe enquanto o todo existir. Inscrições e times pertencem a uma partida, e o pagamento pertence a uma inscrição.
- Os valores fixos dos atributos (posição, modalidade e situações) são representados por **enumerações**.
- `Decimal` é usado para valores monetários, evitando erros de arredondamento de ponto flutuante (RN03).

**Navegabilidade**

| Associação | Navegabilidade | Justificativa |
|---|---|---|
| Jogador *organiza* Partida | Bidirecional | A partida precisa saber quem é seu organizador para validar as permissões (RNF06); o organizador precisa listar suas partidas para consultar pendências (UC16). |
| Jogador *realiza* Inscricao | Bidirecional | A lista da partida exibe o nome de cada inscrito (UC06); o perfil do jogador lista suas inscrições para montar o histórico (UC17). |
| Partida *possui* Inscricao | Bidirecional (composição) | A partida controla vagas e fila de reservas a partir das inscrições (UC07–UC10); o histórico do jogador precisa chegar à partida a partir da inscrição (UC17). |
| Partida *é dividida em* Time | Partida → Time (composição) | Os times são acessados sempre a partir da partida (UC06, UC11, UC13); o time não precisa conhecer a partida. |
| Time *compõe* Inscricao | Bidirecional | O time lista seus jogadores (UC06); a inscrição precisa saber seu time para o reserva promovido assumir a vaga no mesmo time (UC10, FA01) e para o histórico (UC17). |
| Inscricao *gera* Pagamento | Inscricao → Pagamento (composição) | O pagamento é sempre acessado a partir da inscrição (UC14–UC16). |

**Métodos × casos de uso**

| Classe | Método | Caso de uso |
|---|---|---|
| Jogador | `autenticar()` | UC02 |
| Jogador | `criarPartida()` | UC03 |
| Jogador | `consultarHistorico()` | UC17 |
| Jogador | `consultarPendencias()` | UC14, UC17 |
| Partida | `gerarLinkConvite()` | UC04 |
| Partida | `inscrever()` | UC07, UC08 |
| Partida | `cancelarInscricao()` | UC09 |
| Partida | `promoverReserva()` | UC10 |
| Partida | `vagasRestantes()` | UC06, UC07 |
| Partida | `sortearTimes()` | UC11 |
| Partida | `calcularValorPorJogador()` | UC12 |
| Partida | `encerrar()` | UC13 |
| Partida | `cancelar()` | UC05 |
| Partida | `listarPendencias()` | UC16 |
| Inscricao | `promover()` | UC10 |
| Inscricao | `cancelar()` | UC09 |
| Time | `adicionarJogador()` | UC10, UC11 |
| Time | `registrarGols()` | UC13 |
| Pagamento | `informar()` | UC14 |
| Pagamento | `confirmar()` | UC15 |
| Pagamento | `recusar()` | UC15 |
| Pagamento | `registrarManualmente()` | UC15 |

O cadastro (UC01) não aparece como método de Jogador porque é a própria criação do objeto (construtor).

## 10. Segundo Diagrama UML

---

# Parte IV — Protótipo

## 11. Mapa do Site

## 12. Telas

---

## 13. Considerações Finais

## 14. Referências
