# Maven

## Generate a project using Maven

    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app
    cd my-app/
    mvn compile
    mvn test
    mvn test-compile
    mvn package
    mvn install
    mvn site
    

## Configure Eclipse with Maven

    mvn -Declipse.workspace=/home/sansari/workspace/ eclipse:add-maven-repo
    mvn eclipse:eclipse -DdownloadSources=false -DdownloadJavadocs=false
    mvn eclipse:clean
    mvn eclipse:eclipse
    
## Generate JavaDoc

Maven JavaDoc plugin <http://maven.apache.org/plugins/maven-javadoc-plugin/>
 
    mvn javadoc:javadoc # http://maven.apache.org/plugins/maven-javadoc-plugin/

## Generate PDF Documentation

Maven PDF plugin <http://maven.apache.org/plugins/maven-pdf-plugin/usage.html>

Maven APT documentation 

 * <http://maven.apache.org/doxia/references/apt-format.html>
 * <http://maven.apache.org/doxia/references/doxia-apt.html#Figure_extensions>

Maven Veolcity templating <http://velocity.apache.org/site/tools/velocity-site-doxia-renderer/index.html>

    mvn pdf:pdf         # http://maven.apache.org/plugins/maven-pdf-plugin/

## Generate Site Documentation

Site Directory Structure: <http://www.sonatype.com/books/mvnref-book/reference/site-generation-sect-dir-struct.html>

    mvn site:site
    
## Skip Tests while building site
    
    mvn -DskipTests=true -Ddependency.locations.enabled=false  site:site

## Add local dependency:

    mvn install:install-file -Dfile=lib/abcd-4.1.0.jar -DgroupId=com.abcd.java -DartifactId=abcd -Dversion=4.1.0 -Dpackaging=jar

