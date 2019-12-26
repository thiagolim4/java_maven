# Maven 01

Simpliifcação de build de projeto
Maven - ferramenta de automatização de build
Processo manual de Projeto:

public class Calculadora{
  public static void main(String[] args){
      System.out.println("5 mais 5 é "+ (5+5));
  }
}

Para compilar:

javac Calculadora.java

Se tiver cinco arquivos: javac arquivo1 arquivo2 arquivo3

Depois de compilado, o java gera o arquivo .class no mesmo local
Separar fonte (source/src, .java) do build (.class)

Criar diretório onde joga os arquivos que gera, os .class e etc
Vai cair no diretório target

javac -sourcepath src -d target src/Calculadora.java
Compile do diretorio fonte src para o diretorio target o arquivo .java

Pra usar alguma biblioteca: baixar o .jar
Add a biblioteca no src, mas pode add ela na pasta lib

E agora, como compilar o projeto com tudo isso?
javac -sourcepath src -d target -cp lib/xstream-1.4.8.jar
 src/Calculadora.java
 e quero usar um biblioteca no meu classpath (cp)
 não faz verificação da biblioteca, versão, etc

 E se tivesse arquivos de teste?
 Teria que separar no diretorio target, target/classes, src/main, src/main/Calculadora.java

maven.apache.org

- tar.gz
baixa, descompacta, mas usa pelo terminal

cd bin
ls
./ pra exectar um script dentro do diretorio
./mvn --help

pra facilitar o trampo de ter que ficar entrando no diretorio, add isso no seu path

pwd diretorio (caminho do bin)
volta pro diretorio original
cd
pwd
vi .bash_profile (vai alterar esse arquivo)
export PATH=$PATH:diretorio
o path é o path atual + diretorio
salva o bash profile no dir do usuario
abre um novo terminal

Criar projeto novo com maven:
mvn generate archetype:generate -DartifactId=produtos -DgroupId=br.com.empresa.maven -DinteractiveMode=false -DarchetypeArtifactId=maven-archetype-quickstart
artifactid é o seu projeto/nome
o penultimo parametro é tudo default
ultimo é o projeto de exemplo

mvn compile
Primeira vez que vai executar, vai baixar todos os plugins necessários para compilar e manda o arq .class pro target

mvn test
Roda primeira vez pra testar (baixa o JUnit)

Dentro de target, há uma pasta chamada surefire-reports, que abriga arquivos TXT em que o resultado do teste em cada classe é exibido

pom: modelo do projeto, configurando sua versão, grupo do projeto, nome do projeto (artifact), nome bonito é produtos, pode colocar site do projeto (url), e tem as dependências

se o jar é só pra test, usa scope 'test'

mvn clean: limpa o Projeto

Gerando relatorios

mvn clean lima o codigo de saida, deixando somente os de fonte
remove o target

usa esse plugin
mvn surefire-report:report
gera target/site com o relatorio em html

Como faço para o maven empacotar a main?
mvn package
empacota pro target, à medida que muda a version ele muda

java -cp produtos-1.0-SNAPSHOT.jar br.com.empresa.maven.App
e ele roda

Instalação do Maven no Linux

O primeiro passo é realizar o download do arquivo que contém os binários do Maven. Você poderá baixar o arquivo tar.gz, na opção "Binary tar.gz archive".

Após o download, descompacte o tar.gz no diretório de sua preferência. Vamos adicionar o diretório bin, que se encontra no diretório do Maven, na variável de ambiente PATH para que seja possível acessar o executável mvn independente de qual seja o nosso diretório atual no terminal.

Para alterar o valor da variável PATH, no Linux, em geral, editamos o arquivo .bashrc, localizado no diretório do seu usuário. É provável que já exista conteúdo nesse arquivo, portanto adicione o conteúdo no final do arquivo.

No Mac OS o arquivo a ser editado é o .bash_profile, também localizado no diretório do seu usuário. Caso o arquivo não exista, você pode criá-lo. O conteúdo que deve ser inserido nos arquivos é o seguinte:

export PATH=$PATH:/home/lucas/Dev/apache-maven-3.3.9/bin
Observação: Lembre-se de alterar o diretório para o diretório onde se encontra o seu diretório do Maven.

Para que as novas configurações sejam carregadas, abra um novo terminal.

Teste se tudo ocorreu como esperado, utilize o comando mvn -v, que deve retornar informações sobre o Maven, o JDK, e o sistema operacional.

Instalação do Maven no Windows

Comandos para criar projeto maven

Executar
mvn compile
mvn test (roda testes pra target)
mvn clean (limpa o target)

o comando test gera dois diretorios dentro do target:
test-classes (que contem os .class)
surefire-reports (resultado da execuçao dos testes)
