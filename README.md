# Diário de Bordo — Tema 3: Segurança de Banco de Dados

**Disciplina:** Projeto de Banco de Dados
**Data:** 12/08/2026
**Equipe:** Rafael Piasentin, Bruno Parente, Eduardo Fuse

## 1. Resumo estruturado

### Pilares da segurança

A segurança de banco de dados se apoia na tríade **CID**:
- **Confidencialidade** — só usuários autorizados acessam os dados.
- **Integridade** — os dados são exatos e não sofrem alteração indevida.
- **Disponibilidade** — o sistema permanece acessível a usuários legítimos.

**Regra de Anderson:** quanto mais acessível/usável o banco, mais vulnerável; quanto mais protegido, mais difícil de usar. Segurança e usabilidade estão em tensão.

### O que é criptografia

Técnica que transforma os dados em formato ilegível sem a chave correta. Deve ser aplicada:
- Em **repouso** (dados armazenados) e em **trânsito** (dados na rede).
- Às **credenciais** (senhas nunca em texto puro — sempre em hash).
- Com **tokenização/mascaramento** para expor só parte do dado sensível (ex: últimos dígitos de um CPF).

É a última linha de defesa: mesmo que o atacante acesse o banco, os dados criptografados continuam inúteis sem a chave.

### Como o controle de acessos afeta a modelagem

- Leva a modelar **perfis/papéis de usuário** (Aluno, Professor, Admin).
- Leva a **isolar atributos sensíveis** em tabelas próprias, com acesso mais restrito.
- Exige criar **tabelas de log/auditoria** associadas às entidades sensíveis.
- Pode exigir atributos de rastreabilidade (`criado_por`, `alterado_por`, `data_alteracao`).

---

## 2. Laboratório Prático — brModelo web

Modelo conceitual simples do cenário EdTech:

![Modelo Conceitual EdTech](./modelo-conceitual-edtech.png)

---

## 3. Auditoria e Privacidade

### Atributos com dados sensíveis

| Entidade | Atributo sensível | Por quê? |
|---|---|---|
| <!-- ex: Aluno --> | <!-- ex: CPF --> | <!-- ex: dado pessoal protegido por lei --> |
| | | |
| | | |

### Tabelas que precisam de log de acesso

| Tabela | Justificativa |
|---|---|
| <!-- ex: Professor --> | <!-- ex: alterações de notas devem ser rastreáveis --> |
| | |

---

## 4. Referência Bibliográfica

HEUSER, Carlos Alberto. **Projeto de Banco de Dados**. Bookman.