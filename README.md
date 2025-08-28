# Sistema de Chamadas Inteligente para Refeitório Escolar
<!-- EXEMPLO: "Sistema de Chamadas Inteligente para Refeitório Escolar" -->

## 1) Problema
<!-- Escreva o problema sem falar de telas/tecnologias.
     Responda: Quem sofre? Onde? O que atrapalha? Por que isso importa?
     Exemplo: Alunos enfrentam filas longas e desorganizadas no refeitório escolar,
     o que gera atrasos e frustração.
     Objetivo inicial: Organizar o acesso ao refeitório de forma justa e eficiente. -->
Alunos, em escolas com alto volume de estudantes, têm dificuldade em acessar o refeitório de forma organizada.
Isso causa atrasos, aglomerações e insatisfação geral.
No início, o foco será estudantes do ensino médio com o objetivo de organizar a fila para reduzir o tempo de espera.

## 2) Atores e Decisores (quem usa / quem decide)
<!-- Liste os papéis envolvidos no projeto.
     Exemplo:
     Usuários principais: Alunos da escola
     Decisores/Apoiadores: Equipe gestora, coordenadores e responsáveis pelo refeitório -->
Usuários principais: Alunos da escola  
Decisores/Apoiadores: Coordenação pedagógica, responsáveis pelo refeitório, direção da escola

## 3) Casos de uso (de forma simples)
<!-- Formato "Ator: ações que pode fazer".
     DICA: Use "Manter (inserir, mostrar, editar, remover)" quando for CRUD.
     EXEMPLO:
     Todos: Logar/Deslogar do sistema; Manter dados cadastrais
     Gestores: Manter (inserir, mostrar, editar, remover) sobre as chamadas
     Aluno: Manter (inserir, mostrar, editar, remover) dados cadastrais
     -->
Todos: Logar/deslogar; Manter dados cadastrais  
Aluno: Ingressas na fila da chamada para o refeitório; Ver sua posição na fila  
Funcionário do refeitório: Visualizar lista de chamadas; Marcar aluno como atendido

## 4) Limites e suposições
<!-- Simples assim:
     - Limites = Indique prazos, limitações técnicas e suposições feitas.
     - Suposições = Também descreva um plano B, caso algo dê errado no ambiente de testes. -->
Limites: entrega até o fim do semestre; rodar no navegador; sem uso de serviços pagos  
Suposições: acesso à internet; computadores/celulares com navegador atualizado; tempo da coordenação para testes  
Plano B: se sem internet → rodar local usando LocalStorage; se sem coordenação → testar com 5 alunos simulando

## 5) Hipóteses + validação
<!-- Defina hipótese de valor e hipótese de viabilidade.
     Inclua também o plano de validação simples de cada uma. -->
H-Valor: Se os alunos visualizarem sua posição na fila do refeitório, então o tempo de espera parecerá menor e a experiência será mais positiva  
Validação (valor): testar com 5 alunos em simulação real; alvo: ≥4 acharem o sistema útil e fácil de entender

H-Viabilidade: Com HTML/CSS/JS + LocalStorage, gerar e mostrar a chamada na fila leva até 1 segundo  
Validação (viabilidade): medir 20 ações no protótipo; meta: ≥18 em até 1s

## 6) Fluxo principal e primeira fatia
<!-- Descreva o fluxo principal resumidamente e a primeira entrega mínima possível.
     Indique também critérios de aceite objetivos. -->
**Fluxo principal (curto):**  
1) Aluno faz login → 2) Gera chamada → 3) Sistema salva posição na fila → 4) Aluno vê sua posição atual

**Primeira fatia vertical (escopo mínimo):**  
Inclui: tela de login simples, botão "Entrar na fila", salvar posição local, lista visível de fila  
Critérios de aceite:  
- Aluno entra na fila e aparece na lista  
- Lista mostra ordem de chegada

## 7) Esboços de algumas telas (wireframes)
<!-- Insira links ou imagens com os esboços das principais telas.
     Pode ser feito no papel ou ferramentas como Figma, Excalidraw etc. -->
- Tela de login  
- Tela de chamada do aluno (botão "Entrar na fila")  
- Tela de visualização da fila (posição do aluno)  
- Painel do refeitório (lista de alunos chamados)

[Inserir link ou imagem dos wireframes aqui]

## 8) Tecnologias
<!-- Liste as tecnologias que serão usadas no projeto. -->

### 8.1 Navegador
**Navegador:** HTML/CSS/JS  
**Armazenamento local (se usar):** LocalStorage  
**Hospedagem:** GitHub Pages

### 8.2 Front-end (servidor de aplicação, se existir)
**Front-end (servidor):** —  
**Hospedagem:** —

### 8.3 Back-end (API/servidor, se existir)
**Back-end (API):** —  
**Banco de dados:** —  
**Deploy do back-end:** —

## 9) Plano de Dados (Dia 0) — somente itens 1–3
<!-- Especifique apenas o essencial para estruturar o banco de dados. -->

### 9.1 Entidades
<!-- EXEMPLO:
     - Usuario — pessoa que usa o sistema (aluno/professor)
     - Chamado — pedido de ajuda criado por um usuário -->
- Usuario — pessoa que usa o sistema (aluno ou funcionário)  
- Chamada — entrada na fila do refeitório

### 9.2 Campos por entidade
<!-- Use tipos simples: uuid, texto, número, data/hora, booleano, char. -->

### Usuario
| Campo           | Tipo                          | Obrigatório | Exemplo            |
|-----------------|-------------------------------|-------------|--------------------|
| id              | número                        | sim         | 1                  |
| nome            | texto                         | sim         | "João Silva"       |
| email           | texto                         | sim (único) | "joao@email.com"   |
| senha_hash      | texto                         | sim         | "$2a$10$..."       |
| papel           | número (0=aluno, 1=funcionário)| sim         | 0                  |
| dataCriacao     | data/hora                     | sim         | 2025-08-20 10:00   |
| dataAtualizacao | data/hora                     | sim         | 2025-08-20 10:10   |

### Chamada
| Campo           | Tipo               | Obrigatório | Exemplo                 |
|-----------------|--------------------|-------------|-------------------------|
| id              | número             | sim         | 101                     |
| usuario_id      | número (fk)        | sim         | 1                       |
| status          | char               | sim         | 'a' (ativo) / 'f' (finalizado) |
| dataCriacao     | data/hora          | sim         | 2025-08-20 10:05        |
| dataAtualizacao | data/hora          | sim         | 2025-08-20 10:20        |

### 9.3 Relações entre entidades
<!-- Frases simples bastam. EXEMPLO:
     Um Usuario tem muitos Chamados (1→N).
     Um Chamado pertence a um Usuario (N→1). -->
- Um Usuario tem muitas Chamadas (1→N)  
- Uma Chamada pertence a um Usuario (N→1)
