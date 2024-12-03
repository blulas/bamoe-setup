# Maven Repository

With `IBM Business Automation Manager Open Editions v9.1` aligning with its previous version BAMOE v8 in the downstream build model, the artifacts are no longer available in Maven Central. The artifacts are shipped as part of the product as a Container Image and Maven Repository inside the compressed file in a consumable format.

If you have a Maven Repository Manager tool like Artifactory or Nexus, you can import the compressed BAMOE Maven repository content into Maven Repository Manager. For companies without such infrastructure, it is highly recommended to use the container image and make it available within the company for all developers and the continuous integration (CI) system. For companies that already use a Maven Repository Manager tool, developers and the CI system are typically configured to connect with it. If you are using the container image, ensure that it is made available and provide the URL that developers and the CI system need to specify in their `settings.xml` file.

There are two ways to do this:

- Set up a maven repository with a container image
- Configure your local maven repository

## Configuring Maven with the Container Image on Docker (locally)
1.  Start by loading the `tar.gz` file or pulling the image from quay.io:

- **_Using the file_**:  bamoe-9.1.1-maven-repository-image.tar.gz

    ~~~shell
    docker image load --input bamoe-9.1.x-maven-repository-image.tar.gz
    ~~~

- **_Pulling the image_**:  quay.io/bamoe/maven-repository:9.1.1-ibm-0003

    ~~~shell
    docker pull quay.io/bamoe/maven-repository:9.1.1-ibm-0003
    ~~~

2.  Run the image, mapping its port:

~~~shell
docker run -d -p 9000:8080 quay.io/bamoe/maven-repository:9.1.1-ibm-0003
~~~

You can verify the repository is running by accessing the repository in your browser at http://localhost:<PORT>/com/ibm/bamoe.

3.  Open the Maven ~/.m2/settings.xml file in a text editor or integrated development environment (IDE).

    > **_NOTE:_**  If there is no settings.xml file in the ~/.m2/ directory, copy the settings.xml file from the $MAVEN_HOME/.m2/conf/ directory into the ~/.m2/ directory.

4. Add the following lines to the <profiles> element of the settings.xml file:

    ```xml
    <profile>
    <id>ibm-bamoe-enterprise-maven-repository</id>
    <repositories>
        <repository>
        <id>ibm-bamoe-enterprise-maven-repository</id>
        <url>http://localhost:9000</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
        <id>ibm-bamoe-enterprise-maven-repository</id>
        <url>http://localhost:9000</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
        </pluginRepository>
    </pluginRepositories>
    </profile>
    ```

5.  Add the following lines to the <activeProfiles> element of the settings.xml file and save the file:

```xml
<activeProfile>ibm-bamoe-enterprise-maven-repository</activeProfile>
```

## Configuring a local Maven Repository 
If you prefer not to use containers, you can download and configure the BAMOE Maven repository from the compressed file. The BAMOE Maven repository contains the libraries that Java developers need to build BAMOE applications.  To configure the BAMOE Maven repository locally follow these steps:

1.  Download the BAMOE v9.1.x Maven Repository (bamoe-9.1.x-maven-repository.zip).
2.  Extract the downloaded archive.
3.  Go to the `~/.m2/` directory and open the Maven settings.xml file in a text editor or IDE.
4.  Add the following lines to the <profiles> element of the Maven settings.xml file, where <MAVEN_REPOSITORY> is the path of the Maven repository that you downloaded. The format of <MAVEN_REPOSITORY> must be file://$PATH. For example, file:///home/userX/bamoe-9.1.x-maven-repository/:.

```xml
<profile>
  <id>ibm-bamoe-enterprise-maven-repository</id>
  <repositories>
    <repository>
      <id>ibm-bamoe-enterprise-maven-repository</id>
      <url><MAVEN_REPOSITORY></url>
      <releases>
        <enabled>true</enabled>
      </releases>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </repository>
  </repositories>
  <pluginRepositories>
    <pluginRepository>
      <id>ibm-bamoe-enterprise-maven-repository</id>
      <url><MAVEN_REPOSITORY></url>
      <releases>
        <enabled>true</enabled>
      </releases>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </pluginRepository>
  </pluginRepositories>
</profile>
```

5.  Add the following lines to the <activeProfiles> element of the Maven settings.xml file and save the file:

```xml
<activeProfile>ibm-bamoe-enterprise-maven-repository</activeProfile>
```

If your Maven repository contains outdated artifacts, you might encounter Maven error messages when you build or deploy the project, such as:

-  Missing artifact <PROJECT_NAME>
- [ERROR] Failed to execute goal on project <ARTIFACT_NAME>; Could not resolve dependencies for <PROJECT_NAME>

To resolve these issues, delete the cached version of your local repository that is located in the ~/.m2/repository directory to force a download of the latest Maven artifacts.

Your Maven repository is now properly configured and ready to build BAMOE based projects using a standard Maven workflow.



