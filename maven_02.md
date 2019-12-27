# Maven 02
- Fazendo integração do Maven com o Eclipse

## Integrando projeto Maven no Eclipse
- File > Import
- Maven Projects > Next > Diretório do projeto > Enter
- Seleciona o pom.xml e importa > Finish
- O própio Maven baixa alguns plugins (campo inferior direito)
- Clica em Workbench (campo superior direito)
- Se adicionar uma dependência no pom.xml e salvar, o Maven já baixa automaticamente

## Repositório Remoto e Local
- Se executar o comando com -o, Maven executa o comando de maneira *offline*, sem bater na internet para verificar uma versão nova, executando mais rápido
```
mvn -o test
```
- Contudo, se o Maven necessitar de algum arquivo novo para executar a ação solicitada, ele não poderá realizar o download de dependências, uma vez que estamos trabalhando no modo offline. Por isso, é importante ter certeza de que temos todos os elementos necessários antes de operar nesse modo
- Quando o Maven busca na internet as dependências necessárias, ele busca no repositório central da ferramenta (Repositório Remoto) que está hospedado em *repo.maven.apache.org/maven2/*
 - Para acessá-lo usamos o Maven Repository (não é um acesso direto)
- Maven possui um diretório compartilhado entre os projetos para cada usuário do computador (Repositório Local), preenchido gradativamente:
 - .m2/Repository
- Facilita o uso entre projetos, não precisando realizar novos downloads
- Caso queiramos outro, basta usar as tags <repositories> para criá-las e usá-las em outras máquinas, por exemplo.
