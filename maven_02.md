# Integrando projeto Maven no Eclipse

File > Import
Maven Projects > Next > Diretorio do projeto > Enter
Seleciona o pom.xml e importa > Finish
Baixa alguns plugins (campo inferior direito)
Clica em Workbench (campu superior direito)
Fica na parte do projeto na direita

adiciona uma dependencia no pom, salva
e daí ele já vai baixando automaticamente e poe no classpath

# Repositório Remoto e Local

mvn -o test
executa o comando de maneira offline, sem bater na internet para verificar versão nova, executa mais rapido

Contudo, se o Maven necessitar de algum arquivo novo para executar a ação solicitada, ele não poderá realizar o download de dependências, uma vez que estamos trabalhando no modo offline. Por isso, é importante que tenhamos certeza de que temos todos os elementos necessários antes de operarmos nesse modo.

Quando dizemos que o Maven busca na internet as dependências necessárias, estamos nos referindo ao repositório central da ferramenta. Considerando a imensidão da internet, uma busca completa seria praticamente impossível.

Atualmente, o repositório central do Maven está hospedado em repo.maven.apache.org/maven2/. Vamos acessá-lo e clicar em "br/ > com/ > caelum/ > vraptor/", e encontraremos diferentes versões de VRaptor. Clicaremos sobre a versão 4.2.0-RC3/, e encontraremos códigos fonte em formato .jar, Javadocs que podem ser descompactados, e assim por diante.

No repositório central armazenamos as bibliotecas a serem compartilhadas com o mundo do Maven.

Não é comum acessarmos o repositório manualmente, para isso utilizamos o Maven Repository, como aprendemos nas últimas aulas. O repositório central é o que chamamos de repositório remoto, e lá coletamos os elementos necessários para a execução de tarefas em um projeto.

Se compilarmos esse projeto, ele não irá baixar as ferramentas de compilação, afinal elas já foram adquiridas no momento em que estávamos criando o projeto produtos. Quando formos executar testes, também não será necessário fazer o download da biblioteca JUnit. Isso quer dizer que, além do repositório remoto, temos um diretório compartilhado entre todos os nossos projetos, isto é, um repositório local preenchido gradativamente.

Vamos descobrir em que local o Maven está guardando os arquivos. Primeiramente, observaremos os diretórios do usuário por meio do comando ls, após cd. No entanto, não localizamos o diretório, pois, na verdade, o repositório local é invisível por padrão, .m2, que possui um diretório chamado repository.

.m2/repository

Caso queiramos outro, basta usar as tags <repositories> para criá-las e usá-las em outras máquinas, por exemplo.

Vantagem de manter repositório local:
A vantagem de se manter um repositório local é que é possível realizar um cache entre vários projetos que utilizam o Maven. Dessa forma, tudo que já estiver salvo no repositório local é utilizado e compartilhado, não sendo necessário realizar novos downloads.

Vale lembrar que o repositório local fica disponível na pasta do usuário, e por esse motivo não estará disponível para diferentes usuários de um mesmo computador.
