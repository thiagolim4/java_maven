# Ciclo de Vida do Maven

- O processo de construção do projeto passa pelo chamado *Ciclo de Vida*, que possui as fases:

1. **Validação:** verificamos se projeto possui todas as informações necessárias

2. **Compilação:** compilar os conteúdos

3. **Teste:** realizar testes diferentes no projeto

4. **Pacote:** geração de um pacote do projeto

5. **Teste de integração:** realizar testes de integração

6. **Verificação:** checagem do pacote gerado

7. **Instalação:** realizar a instalação do pacote no repositório local

8. **Implantação:** realizar a implantação no ambiente adequado

- Cada fase posterior executa todas as anteriores
- Podemos forçar a ordem de etapas com opções da linha de comando, como não gerar testes, por meio do comando:
```
mvn -DskipTests=true package
```

## Incluindo plugins

- **maven pmd**: analisa o código fonte e detecta possíveis margens de bug no código
- Executa o plugin, baixando as dependências necessárias e executando o relatório:
```
mvn pmd:pmd
```
- Será gerado um arquivo pmd.html, armazenado no diretório "> target > site"
- Comando realiza uma varredura no build à procura de erros, inclusive interrompendo o projeto caso as regras definidas para o código não sejam cumpridas:
```
mvn pmd:check
```
- Para não ter que executar várias vezes o comando, pode-se realizar configurações que permitam a execução automática do PMD durante o build do projeto:
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-pmd-plugin</artifactId>
      <version>3.6</version>
    </plugin>
  </plugins>
    </plugins>
</build>
```
- No terminal:
```
mvn verify
```
- Além de mencionar o plugin, deve-se indicar que ele alterará o clico de vida do projeto, adicionando a tag <executions> para indicar quando o plugin deverá ser executado
- No caso, uma execução na fase de verificação, cujo objetivo (goals/opção) é check:
```xml
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
```
## Plugin de cobertura de testes

- Instalar o plugin jacoco
- É possível verificar os goals (opções) para execução do plugin
- Não é bom deixar a versão de um plugin em aberto pois o Maven sempre busca a mais recente (e se ficar em aberto isso vai sendo sempre modificando, podendo causar problemas no projeto)
```
mvn jacoco:help
```
- Rodar duas fases: prepare-agent e report
```xml
<executions>
<plugin>
  <groupId>org.jacoco</groupId>
  <artifactId>jacoco-maven-plugin</artifactId>
  <version>0.7.5.201505241946</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
                <goal>report</goal>
            </goals>
        </execution>
</plugin>
</executions>
```
- Relatório vai pra target

## Atualizando dependências do projeto
- Exibe as dependências com novas versões mas sem atualizar:
```
mvn versions:display-dependency-updates
```
- Atualiza com novas versões:
```
mvn versions:use-latest-versions
```
- Ambos fazem parte do plugin Versions

## Testes unitários
- Para cada método, só criar:
```java
@Test
public void metodoTest(){
  //...
}
```
- É possível rodar direto pelo Eclipse:
 - Run As > Maven Build
 - Goals > Verify
- Ou:
```
mvn verifiy
```
