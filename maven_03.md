# Ciclo de Vida do Maven

Na documentação do Maven encontraremos as fases que um ciclo de vida build apresenta:

1. Validação: verificamos se projeto possui todas as informações necessárias

2. Compilação: compilar os conteúdos

3. Teste: realizar testes diferentes no projeto

4. Pacote: geração de um pacote do projeto

5. Teste de integração: realizar testes de integração

6. Verificação: checagem do pacote gerado

7. Instalação: realizar a instalação do pacote no repositório local

8. Implantação: realizar a implantação no ambiente adequado

Podemos forçar a ordem de etapas com opções da linha de comando, como não gerar testes, por meio do comando -DskipTests=true:

mvn -DskipTests=true package

# Incluindo plugins

maven pmd: analisa o codigo fonte e detecta possiveis margens de bug no codigo
mvn pmd:pmd
Procura na internet pra baixar junto com as dependencias e executa o relatorio

Como o relatório PMD segue o padrão do Maven, o .jar desse plugin é encontrado automaticamente, ou seja, não precisamos efetivar nenhum tipo de configuração, já que o download dos conteúdos é realizado sem problemas. Ao final, será gerado um arquivo pmd.html, armazenado no diretório "produtos > target > site". Vejamos o conteúdo do relatório:

no site do Apache tem usos do pmd e como analisar códigos de JavaScript, etc

Com o comando pmd:pmd conseguimos gerar relatórios, mas de que forma verificamos a qualidade do nosso projeto? Lembrando que a verificação é uma fase do ciclo de vida do build.

Se simplesmente utilizarmos o comando mvn verify no terminal, não teremos uma verificação efetiva, afinal não configuramos o PMD para ser utilizado no momento da verificação. Para isso, utilizaremos o comando pmd:check, que realiza uma varredura no build à procura de erros, inclusive interrompendo o projeto caso as regras definidas para o código não sejam cumpridas.

Ao executarmos pmd:check, receberemos uma mensagem de erro no terminal (BUILD FAILURE), e a alegação é de que temos uma violação (You have 1 PMD violation). Estamos utilizando o PMD padrão, que possui diversas regras. Para customizá-lo precisamos ir ao Rules Set e aplicar nossas preferências.

Temos uma questão: todas as vezes em que quisermos executar o PMD precisamos utilizar pmd:check no terminal, o que pode se tornar cansativo ao longo do desenvolvimento do programa. No arquivo pom.xml, podemos realizar configurações que permitam a execução automática do PDM durante o build do projeto. Começaremos criando a tag <build>, em que adicionaremos <plugins>.

<build>
    <plugins>
    <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-pmd-plugin</artifactId>
      <version>3.6</version>
    </plugin>
  </plugins>
    </plugins>
</build>

No terminal, executaremos o comando mvn verify. Embora tenhamos um erro propositalmente colocado em nosso projeto, a verificação não consegue detectá-lo. Isso porque o PMD não é executado.

Isto indica que não basta mencionarmos o uso do plugin; devemos indicar que ele alterará o ciclo de vida do projeto. No arquivo pom.xml, adicionaremos a tag <executions> para especificarmos quando o plugin deverá ser executado, afinal podem haver múltiplas execuções ao longo do build. Em nosso caso, será apenas uma execução na fase (<phase>) de verificação (verify), cujo objetivo (<goals>) é check.

<project>
  <!-- ... -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-pmd-plugin</artifactId>
        <version>3.10.0</version>
        <executions>
            <execution>
                <phase>verify</phase>
                    <goals>
                        <goal>check</goal>
                    </goals>
            </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
  <!-- ... -->
</project>
