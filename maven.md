# 执行maven 命令报错
*  Non-resolvable parent POM for com.xxx.yyy.zzz.app:x-app-service:[unknown-version]: Failure to find com.xxx.yyy.zzz.app:sandbox-app-x-app:pom:1.0.0-SNAPSHOT 
  in ${resposity_url} was cached in the local repository, resolution will not be reattempted until the update interval of tbmirror-snapshots has elapsed or 
  updates are forced and 'parent.relativePath' points at wrong local POM @ line 5, column 11 -> [Help 2]
  
   * 关键parent pom. parent pom和 子项目中依赖的parent 应该有不一致的地方. 
   * **不要猜测, 反复盲目实验, 这是科学, 不是玄学...**
   * Following the upward warings and errors, you can find the answer. 
   * In this case, groupId spells error.  an extra 'e'. 
      com.xxx.yyy.zzz.**appe**:sandbox-app-x-app instead of com.xxx.yyy.zzz.**app**
    
    ```text
    [INFO] Scanning for projects...
    [ERROR] [ERROR] Some problems were encountered while processing the POMs:
    [WARNING] 'parent.relativePath' of POM com.xxx.yyy.zzz.app:x-app-app:[unknown-version] (/Users/xxxx/xxx/sandbox-app-x-app/x-app-app/pom.xml) points 
    at com.xxx.yyy.zzz.appe:sandbox-app-x-app instead of com.xxx.yyy.zzz.app:sandbox-app-x-app, please verify your project structure @ line 5, column 13
    [FATAL] Non-resolvable parent POM for com.xxx.yyy.zzz.app:x-app-app:[unknown-version]: Failure to find com.xxx.yyy.zzz.app:sandbox-app-x-app:pom:1.0.0-SNAPSHOT in   was cached in the local repository, resolution will not be reattempted until the update interval of tbmirror-snapshots has elapsed or updates are forced and 'parent.relativePath' points at wrong local POM @ line 5, column 13

    ```
   
   
# maven插件
## maven-antrun-plugin
* run ant tasks. 
* example
    ```text
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.8</version>
                <executions>
                    <execution>
                        <phase>prepare-package</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <target>
                                <taskdef name="classModel" classpathref="maven.compile.classpath"
                                         classname="com.xxx.yyy.zzz.ClassModelMetaDataAntTask">
                                </taskdef>
                                <classModel/>
                            </target>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```
  
