# Maven 01

## O que é o Maven
- Ferramenta de automatização de build (construção) de projeto
- Organiza o projeto, separando código executável de entregável (cliente), além de separar os testes, recursos, etc

## Processo de Build sem Maven
- Exemplo de processo manual de build de projeto:

```java
public class Calculadora{
  public static void main(String[] args){
      System.out.println("5 mais 5 é "+ (5+5));
  }
}
```

### Compilar
- Projeto com um arquivo:
```
javac Calculadora.java
```
- Se tiver mais arquivos:
```
javac arquivo1 arquivo2 arquivo3
```
- Depois de compilado, o Java gera o arquivo .class no mesmo local, sem separação de código fonte (source/src, .java) do build (.class)

### Compilar e separar
- O melhor seria criar um diretório para ter onde jogar os arquivos gerados (.class) e etc.
- Compilar do diretório fonte (src) para o diretório alvo (target) a classe Calculadora.java:
```
javac -sourcepath src -d target src/Calculadora.java
```
- Para usar alguma biblioteca no projeto, deve-se baixar o .jar correspondente e adicionar no src do mesmo (ou lib)

### Compilar e separar com biblioteca
- Compilar o projeto com todas as adições, usando a biblioteca no classpath (cp):
```
javac -sourcepath src -d target -cp lib/xstream-1.4.8.jar src/Calculadora.java
```
- Problemas: não faz verificação de biblioteca, versão, etc
- Se tivesse arquivos de teste: teria que separar no diretório target, além das separações de target/classes, target/test, e outros diretórios em src/main, src/main/Calculadora.java

## Baixando Maven
- Site do maven.apache.org
- Download tar.gz
 - Baixa, descompacta, executa pelo terminal
 - Dentro de /bin
```
./mvn --help
```

## Criar Projeto Novo com Maven:
- Novo projeto usando archetype:
```
mvn generate archetype:generate -DartifactId=produtos -DgroupId=br.com.empresa.maven -DinteractiveMode=false -DarchetypeArtifactId=maven-archetype-quickstart
```
- ArtifactId é o seu projeto/nome (identificação, geralmente igual ao nome)
- archetypeArtifcactId: projeto que vai usar como arquétipo/exemplo para construção, em geral usa-se o quickstart (iniciante, com configurações básicas)

- Primeira execução do projeto no terminal, Maven baixa todos os plugins necessários e manda os arquivos .class para o diretório target
```
mvn compile
```
- Executa para fim de teste (baixa JUnit)
```
mvn test
```
- Dentro de target, há uma pasta chamada surefire-reports, que abriga arquivos TXT em que o resultado do teste em cada classe é exibido
- **pom.xml**: arquivo que contém o modelo do projeto, configurando sua versão, grupo do projeto, nome do projeto (artifact), nome, site (url), dependências e plugins.

## Gerando relatórios
- Limpa o projeto, limpa o código de saída deixando somente os de fonte removendo tudo do target:
```
mvn clean
```
- Plugin Surefire-Report, gera target/site com relatório em html:
```
mvn surefire-report:report
```
- Para empacotar a main em .jar, deixando no target (à medidade que a version muda ele também muda):
```
mvn package
```
- Executar o package:
```
java -cp produtos-1.0-SNAPSHOT.jar br.com.empresa.maven.App
```

## Instalação
- Instalação do Maven no Linux (link)
- Instalação do Maven no Windows (link)

## Resumo
- Criando projeto:
```
mvn compile
mvn test
mvn clean
```
- Comando test gera dois diretórios dentro do target:
 - test-classes (que contem os .class)
 - surefire-reports (resultado da execuçao dos testes)
