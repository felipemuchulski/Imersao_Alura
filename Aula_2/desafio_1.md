> Prompt
Questão: Tenho uma tabela de usuários no meu banco de dados PostgreSQL  que necessita todas informações preenchidas, para não ocorrerem erros. As informações são as seguintes : ID Usuário, Nome Completo, CPF, Endereço, Cargo e Escolaridade. Se eu utilizar o comando INSERT INTO  e deixar uma informação faltando, como posso adicionar ela depois?

Resposta: Suponhamos que você tenha deixado faltando o "Cargo" do usuário, você irá utilizar o comando UPDATE para alterar o valor do campo da coluna vazio. Por exemplo: 
UPDATE usuarios 
SET cargo = 'cargo atual'
 WHERE id_user = '1';


Questão: Como posso organizar a minha tabela para que na hora da inserção de valores, eles sejam obrigatorios e não fiquem como "NULL" nas colunas da tabela "usuarios". Fazer isso levando em consideração que o banco de dados  é o PostgreSQL

Resposta: 

> Output:
Resposta: Para garantir que as informações em sua tabela "usuarios" sejam preenchidas e não permitam valores NULL, você pode utilizar a restrição "NOT NULL" ao criar ou alterar a tabela.
1. Ao criar a tabela:
CREATE TABLE usuarios (
    id_usuario SERIAL PRIMARY KEY,
    nome_completo VARCHAR(255) NOT NULL,
    cpf VARCHAR(11) NOT NULL UNIQUE,
    endereco VARCHAR(255) NOT NULL,
    cargo VARCHAR(255) NOT NULL,
    escolaridade VARCHAR(255) NOT NULL
);

No exemplo acima, a cláusula NOT NULL após cada tipo de dado (VARCHAR) especifica que a coluna não pode conter valores nulos.

2. Alterando uma tabela existente:
Se a tabela "usuarios" já existe, você pode adicionar a restrição NOT NULL usando o comando ALTER TABLE:
ALTER TABLE usuarios
ALTER COLUMN nome_completo SET NOT NULL,
ALTER COLUMN cpf SET NOT NULL,
ALTER COLUMN endereco SET NOT NULL,
ALTER COLUMN cargo SET NOT NULL,
ALTER COLUMN escolaridade SET NOT NULL;

Observações:
Ao definir a restrição NOT NULL, qualquer tentativa de inserir um novo registro com valores ausentes nas colunas especificadas resultará em um erro.
Lembre-se de que as restrições NOT NULL também se aplicam a atualizações de registros existentes.
Você pode considerar o uso de outras restrições, como UNIQUE, para garantir a integridade dos dados em sua tabela.