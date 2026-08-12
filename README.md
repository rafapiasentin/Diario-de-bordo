# Diário de Bordo — Tema 3: Segurança de Banco de Dados

**Disciplina:** Projeto de Banco de Dados
**Cenário:** EdTech (Alunos, Disciplinas e Professores)
**Data:** 12/08/2026
**Equipe:** Rafael Piasentin, Bruno Parente, Eduardo Fuse

---

## 1. Resumo estruturado do tema

### O que é segurança de banco de dados?

Segurança de banco de dados é o conjunto de ferramentas, controles e medidas destinadas a garantir **confidencialidade**, **integridade** e **disponibilidade** dos dados. A confidencialidade é o elemento mais comprometido na maioria das violações.

Deve proteger:
- Os dados armazenados no banco
- O SGBD (sistema de gerenciamento do banco de dados)
- As aplicações associadas
- O servidor físico/virtual e o hardware subjacente
- A infraestrutura de rede usada para acessar o banco

> **Regra de Anderson:** quanto mais acessível e usável for o banco de dados, mais vulnerável ele é; quanto mais protegido, mais difícil de acessar e usar. Segurança e usabilidade estão em tensão constante.

### Principais ameaças

| Ameaça | Descrição breve |
|---|---|
| Ameaças internas | Usuário malicioso, negligente, ou credenciais roubadas (phishing) |
| Erro humano | ~49% das violações relatadas |
| Vulnerabilidades de software do SGBD | Falta de aplicação de patches de segurança |
| Injeção de SQL/NoSQL | Inserção de código malicioso em consultas |
| Estouro de buffer | Escrita de dados além do espaço de memória alocado |
| Malware | Software malicioso via endpoints conectados à rede |
| Ataques a backups | Backups mal protegidos, tão vulneráveis quanto o banco principal |
| DoS/DDoS | Sobrecarga do servidor para negar serviço a usuários legítimos |

### Melhores práticas

- Segurança física do servidor
- Controle de acesso administrativo e de rede (princípio do menor privilégio)
- Segurança de contas e dispositivos de usuários
- Criptografia de dados em repouso e em trânsito
- Atualização constante do software do SGBD (patches)
- Segurança de aplicações e servidores web
- Segurança de backups (mesmos controles do banco principal)
- **Auditoria**: registro de todos os logins e operações sobre dados sensíveis

### Tipos de controle

- **Administrativos** — instalação, mudança e configuração do banco
- **Preventivos** — acesso, criptografia, tokenização, mascaramento
- **Investigativos (detetives)** — monitoramento de atividade e prevenção de perda de dados

---

## 1.1 Pontos de foco do tema (respostas diretas)

### Quais são os pilares da segurança?

Segundo o material da IBM, a segurança de banco de dados se apoia em três pilares clássicos, conhecidos como a **tríade CID (Confidencialidade, Integridade e Disponibilidade)**:

- **Confidencialidade** — garantir que apenas usuários autorizados acessem os dados. É o pilar mais comprometido na maioria das violações.
- **Integridade** — garantir que os dados são exatos, consistentes e não foram alterados de forma não autorizada.
- **Disponibilidade** — garantir que os dados e o sistema estejam acessíveis a usuários legítimos sempre que necessário (contraponto direto a ataques DoS/DDoS).

A esses três, soma-se a tensão constante descrita pela **Regra de Anderson**: quanto mais acessível/usável for o banco, mais vulnerável ele fica a ameaças; quanto mais protegido, mais difícil se torna acessá-lo e utilizá-lo. Ou seja, segurança e usabilidade puxam em direções opostas, e a modelagem/gestão do banco precisa equilibrar os dois lados.

### O que é criptografia (no contexto de banco de dados)?

Criptografia é a técnica que transforma os dados em um formato ilegível para quem não possui a chave correta, protegendo-os mesmo que o atacante consiga acessar fisicamente o banco ou os backups. O material recomenda:

- Criptografar dados **em repouso** (armazenados no disco) e **em trânsito** (circulando pela rede).
- Aplicar criptografia também às **credenciais de acesso** (nunca guardar senhas em texto puro — devem ser armazenadas como hash).
- Gerenciar as **chaves de criptografia** seguindo boas práticas (rotação, restrição de acesso às chaves, etc.).
- Usar **tokenização/mascaramento de dados** quando for necessário exibir apenas parte da informação sensível (ex: mostrar só os últimos dígitos de um CPF/NIF).

Na prática, a criptografia funciona como a **última linha de defesa**: mesmo que todos os outros controles falhem e ocorra uma violação, os dados criptografados continuam protegidos, pois são inúteis sem a chave.

### Como o controle de acessos afeta a modelagem?

O controle de acessos (quem pode ver/alterar o quê) tem impacto direto em como desenhamos o modelo de dados, não é apenas uma questão de configuração do SGBD:

- **Princípio do menor privilégio** → leva a pensar em **perfis/papéis de usuário** (ex: Aluno, Professor, Administrador) como parte do modelo, não só como configuração externa.
- **Separação de dados sensíveis** → pode levar a **isolar atributos sensíveis em tabelas próprias** (ex: separar dados de autenticação dos dados de perfil), para aplicar políticas de acesso mais restritas só onde é necessário.
- **Necessidade de auditoria** → exige modelar **tabelas/entidades de log** (quem acessou, quando, que operação fez) associadas às tabelas que guardam dados sensíveis.
- **Rastreabilidade de alterações** → pode levar à inclusão de atributos como `criado_por`, `alterado_por`, `data_alteracao` nas entidades críticas.
- **Confidencialidade por design** → o modelador já pensa, desde o modelo conceitual, em quais entidades/atributos vão precisar de controle de acesso diferenciado, em vez de tratar segurança como algo "adicionado depois".

Ou seja: controle de acessos não é só sobre *permissões no SGBD* — ele molda quais entidades, atributos e relacionamentos extras (como tabelas de log e papéis) precisam existir no modelo desde o início.

---

## 2. Laboratório Prático — brModelo web

### Modelo conceitual (cenário EdTech: Alunos, Disciplinas, Professores)

Façam o modelo conceitual simples no [brModelo web](https://www.brmodeloweb.com/), exportem a imagem (PNG) e insiram abaixo.

<!--
Como inserir a imagem no Markdown:
![Modelo Conceitual EdTech](./modelo-conceitual-edtech.png)

Coloquem o arquivo de imagem na mesma pasta deste .md (ou em uma pasta /img)
e ajustem o caminho conforme necessário.
-->

![Modelo Conceitual EdTech](./modelo-conceitual-edtech.png)

<!-- Breve descrição do modelo desenhado -->
**Descrição do modelo:**

<!-- preencher: entidades, relacionamentos e atributos principais desenhados -->

---

## 3. Foco de Segurança: Auditoria e Privacidade

### 3.1 Atributos que representam dados sensíveis

Identifiquem, no cenário EdTech (Alunos, Disciplinas, Professores), quais atributos são dados sensíveis (ex: CPF, senha, e-mail, dados de saúde, dados financeiros, etc.) e classifiquem o motivo.

| Entidade | Atributo sensível | Por que é sensível? |
|---|---|---|
| <!-- ex: Aluno --> | <!-- ex: CPF --> | <!-- ex: identificação fiscal única, dado pessoal protegido por lei --> |
| | | |
| | | |
| | | |

<!--
Dica de raciocínio (podem apagar este comentário):
- Dados de identificação civil (CPF, RG, número de matrícula)
- Credenciais de acesso (senha — deve estar sempre em hash, nunca em texto puro)
- Contatos pessoais (e-mail, telefone, endereço)
- Dados acadêmicos sensíveis (notas, se houver regras de privacidade específicas)
- Dados financeiros (se houver pagamento de mensalidades)
-->

### 3.2 Tabelas que precisam de logs (registros) de acesso

Identifiquem quais tabelas do modelo precisam de auditoria/logs de acesso para garantir segurança, e justifiquem.

| Tabela | Precisa de log de acesso? | Justificativa |
|---|---|---|
| <!-- ex: Professor --> | <!-- Sim/Não --> | <!-- ex: alterações de notas devem ser rastreáveis --> |
| | | |
| | | |

<!--
Dica de raciocínio (podem apagar este comentário):
- Quem acessou/alterou notas e quando?
- Quem consultou dados pessoais de alunos/professores?
- Tentativas de login falhadas (possível ataque de força bruta)?
- Alterações em dados de credenciais (troca de senha, permissões)?
-->

### 3.3 Recomendações de segurança para o cenário

<!-- preencher: 3 a 5 recomendações práticas de segurança para este cenário EdTech,
com base nas melhores práticas estudadas na seção 1 -->

---

## 4. Referência Bibliográfica

HEUSER, Carlos Alberto. **Projeto de Banco de Dados**. Bookman, [edição conforme plano de ensino].

<!-- preencher: capítulo/páginas específicas usadas como embasamento teórico da modelagem -->

---

## 5. Reflexão da equipe

<!-- preencher: principais aprendizados, dificuldades encontradas no brModelo,
dúvidas que restaram -->