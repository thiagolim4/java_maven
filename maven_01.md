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
