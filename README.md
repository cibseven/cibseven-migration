# cibseven-migration

a) add this to your maven pom.xml:
```xml
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.openrewrite.maven</groupId>
          <artifactId>rewrite-maven-plugin</artifactId>
          <version>5.44.0</version>
          <configuration>
            <configLocation>${project.basedir}/replace-camunda-with-cibseven.yml</configLocation>
            <activeRecipes>
              <recipe>org.cibseven.ReplaceCamundaWithCIBSeven</recipe>
            </activeRecipes>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
```

b) put [replace-camunda-with-cibseven.yml](replace-camunda-with-cibseven.yml) into root dir of your project

c) run
```bash
mvn rewrite:run
```
