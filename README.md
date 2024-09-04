Monorepo
Por ser um time fullstack, a estratégia de monorepo faz mais sentido. Nesse sentido irá funcionar somente como uma organização das pastas.
O uso de ferramentas para trabalhar com monorepo auxilia em algumas questões, como ter um eslint especifico para cada repo, ou seja, gerenciar de uma forma melhor dependencias duplicadas.
Nesse projetos vamos utilizar o Workspace e Turborepo (acelera os processos do monorepo, por exemplo faz o build somente para o frontend e não para ambos os projetos).

# SAAS (Software as a Service)
É um software criado para resolver um problema que será utilizado por alguém (pessoas e/ou empresas)

## Single Tenant vc Multi Tenant

### Single Tenant
Single Tenant é quando temos uma única instancia do software que será utilizado pela empresa. Ou seja, cada empresa tem sua infra exclusiva para utilizar o software.

### Multi Tenant
Multi Tenant é quando temos um software sendo utilizado por mais de uma empresa. Essas empresas usam a mesma extrutura.
IMPORTANTE
NÃO QUER DIZER que seja multi subdomínios. (emp1.app.com, emp2.app.com). Um exemplo de software assim é o Stripe.
Também NÃO QUER DIZER um banco por empresa.
A grande maioria dos SaaS que são Multi Tenant não usam um banco por empresa.
Essa solução é aplicanda principalmente quando falamos de dois segmentos específicos:
- Orgãos Públicos (governo);
- LGPD / Contrato individual (Grandes empresas como Samsung, Itaú, etc...);

## Autorização
Hoje existem dois modelos mais comuns para a parte de autenticação.

### RBAC (Role Based Authorization Control)
Quando nos temos algumas roles definidas (admin, billing, developer) onde cada um deles tem permissões específicas. Quando criamos um usuário, escolhemos uma delas para aplicar a permissão.
Esse controle não é granular, é algo mais alto nível.

### ABAC - Attribute Based Authorization Control
Nós temos um nível mais granular para a permissão, ou seja, utilizamos os atributos da entidade para determinar se determinado cargo por ou não fazer algo.
Por exemplo, o ADMIN pode alterar todos os campos de um projeto, um developer pode apenas alterar o título do projeto.

Um ponto interessante é se o nosso SaaS tem a necessidade de permitir que os usuários criem novas Roles.
Na esmagadora maioria dos casos, não existe essa necessidade e conseguimos definir cargos e permitir que o usuário apelas defina o cargo pro usuário que está cadastrando.
A grande vantagem dessa abordagem que não precisamos ter as tabelas de roles em nosso banco de dados, possibilitando assim que criemos um arquivo de configuração que pode ser alterado por meio de um commit.
Isso torna o nosso banco de dados muito mais simples.
```json
{
  "admin": ["create_project", , "view_project", "delete_project", ...],
  "member": ["view_project", ...],
  ...
}
```