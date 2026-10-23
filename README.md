# OrcamentoChurrasco__system
#🍖 Big Bull BBQ — Sistema de Orçamentos de Eventos

> **Projeto de Extensão Universitária** desenvolvido para automatizar a triagem e coleta de preferências de clientes para eventos de churrasco, integrando as solicitações diretamente ao WhatsApp do churrasqueiro para fechamento manual de propostas.

---

## 📌 Sobre o Projeto

O **Big Bull BBQ** é uma aplicação web responsiva projetada para atuar como um auxiliar comercial no atendimento ao cliente. O sistema guia o usuário por um formulário estruturado para coletar informações essenciais do evento e montar um cardápio personalizado, garantindo que o profissional receba todos os dados necessários para elaborar a proposta comercial.

### 🎯 Escopo do Sistema
- **Dentro do escopo:** Coleta de dados do responsável, data/horários, quantidade de convidados por faixa etária, infraestrutura do local, seleção modular de itens do cardápio, campo de observações e geração de mensagem formatada via API do WhatsApp.
- **Fora do escopo:** Cálculo automático de preços, exibição de taxa de deslocamento/combustível, exibição de condições de pagamento (como sinal) e armazenamento permanente de dados em banco de dados.

---

## 📏 Regras de Negócio (RN)

As 14 regras abaixo definem o comportamento esperado do sistema e os critérios de aceite:

| Código | Categoria | Regra de Negócio | Descrição / Critério de Aceite no Sistema |
| :---: | :--- | :--- | :--- |
| **RN01** | Convidados | Faixa etária: isentos | Crianças de **0 a 4 anos** não entram no cálculo de consumo de carnes e alimentos (não pagam). |
| **RN02** | Convidados | Faixa etária: valor diferenciado | Crianças de **5 a 11 anos** têm consumo intermediário (pagam valor diferenciado/meia). |
| **RN03** | Convidados | Faixa etária: valor integral | Pessoas com **12 anos ou mais** são contadas como adultos (consumo e valor integral). |
| **RN04** | Convidados | Mínimo de evento | **Não há mínimo** de convidados para realizar o evento. |
| **RN05** | Cardápio | Mínimo: carnes | A seleção de carnes exige a escolha de no **mínimo 3 tipos**. |
| **RN06** | Cardápio | Mínimo: acompanhamentos | A seleção de acompanhamentos exige a escolha de no **mínimo 3 tipos**. |
| **RN07** | Cardápio | Mínimo: entradas | A seleção de entradas exige a escolha de no **mínimo 1 tipo**. |
| **RN08** | Cardápio | Itens opcionais | As categorias **Sobremesas** e **Molhos** são de seleção opcional (mínimo 0). |
| **RN09** | Logística | Região de atendimento | O atendimento abrange **qualquer região** (cálculo de deslocamento baseado na quilometragem). |
| **RN10** | Logística | Ocultação do frete | A taxa de deslocamento/combustível **não deve ser exibida** no formulário inicial; é embutida posteriormente na proposta. |
| **RN11** | Infraestrutura | Checagem de churrasqueira | É **obrigatório** perguntar se o local do evento possui churrasqueira (*Sim/Não*). |
| **RN12** | Infraestrutura | Ocultação de estrutura própria | Se o local não tiver churrasqueira, o sistema **não precisa exibir custos ou informações adicionais** sobre a logística de churrasqueira portátil (alinhamento feito manualmente). |
| **RN13** | Financeiro | Orçamento manual | O site **não calcula preço total nem estimativa monetária**. Serve apenas como coletor de preferências para envio via WhatsApp. |
| **RN14** | Financeiro | Ocultação de condições de pagamento | Informações de pagamento (como o sinal obrigatório de 50%) **não devem aparecer no site**; são tratadas na negociação manual. |

---

## ⚙️ Requisitos Funcionais (RF)

| Código | Requisito | Descrição |
| :---: | :--- | :--- |
| **RF01** | Cadastrar dados do responsável | Coletar o nome do responsável pelo evento e o número de telefone (WhatsApp) para contato. |
| **RF02** | Definir data e horário | Permitir que o cliente informe a data do evento, o horário de início do evento e o horário estipulado para iniciar o serviço de alimentação ("servir a comida"). |
| **RF03** | Classificar faixa etária e divisão de convidados | Coletar a quantidade de pessoas por faixa etária: crianças de 0 a 4 anos (isentas do cálculo de consumo), crianças de 5 a 11 anos (faixa intermediária, valor diferenciado) e adultos a partir de 12 anos (público integral). |
| **RF04** | Verificar infraestrutura do local | Perguntar obrigatoriamente se o local possui churrasqueira (*Sim/Não*) e coletar o endereço ou descrição do local. |
| **RF05** | Selecionar cardápio personalizado item por item | Disponibilizar um catálogo interativo por categorias, com escolha modular dos itens: carnes tradicionais (mínimo 3 tipos), acompanhamentos (mínimo 3 tipos), entradas (mínimo 1 tipo); molhos e sobremesas são opcionais. |
| **RF06** | Utilizar campo de observações livres | Fornecer um campo de texto livre para recados ou detalhes complementares sobre o evento. |
| **RF07** | Gerar envio de mensagem para o WhatsApp | Ao finalizar o preenchimento e validar as regras, formatar as escolhas em uma mensagem estruturada e redirecioná-la via API do WhatsApp ao número de atendimento do churrasqueiro, apoiando o fechamento manual da proposta. |

---

## 🛡️ Requisitos Não Funcionais (RNF)

| Código | Requisito | Descrição |
| :---: | :--- | :--- |
| **RNF01** | Usabilidade e responsividade (mobile first) | A maioria dos clientes acessará por smartphone, via links do Instagram ou WhatsApp. A interface deve ser totalmente responsiva, leve e intuitive em telas menores. |
| **RNF02** | Desempenho e velocidade | O site deve carregar rapidamente em conexões móveis padrão, usando tecnologias modernas de front-end (como React/Next.js) hospedadas em nuvem de alta performance (ex.: Vercel). |
| **RNF03** | Disponibilidade (uptime) | O sistema deve ficar disponível 24 horas por dia, 7 dias por semana, para que clientes montem orçamentos a qualquer momento. |
| **RNF04** | Privacidade e segurança de dados (LGPD) | O sistema não deve armazenar dados sensíveis dos clientes em banco de dados de forma permanente. As informações são repassadas diretamente pelo canal seguro do WhatsApp, preservando a privacidade. |
| **RNF05** | Ausência de cálculo financeiro automático | Por decisão de negócio, taxas de deslocamento e orçamentos finais são calculados manualmente pelo profissional. O sistema não exibe preços finais nem estimativas monetárias ao usuário final. |

---

## 🛠️ Tecnologias e Arquitetura

- **Front-end:** HTML5, CSS3, JavaScript (ES6+) / React (Next.js)
- **Estilização:** Tailwind CSS (com Design System rústico/premium)
- **Hospedagem & Deploy:** Vercel
- **Integração:** API URI Scheme do WhatsApp (`https://api.whatsapp.com/send`)

---

## 👨‍💻 Autor e Contexto Acadêmico

Desenvolvido como **Projeto de Extensão Universitária** focado na aplicação prática de Engenharia de Requisitos, Análise de Sistemas e Desenvolvimento Web para impacto real em um empreendimento local.
