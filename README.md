# Apache Maven

Maven is a powerful build automation tool used primarily for Java projects, enabling the creation, management, and automation of your project.

In short, Maven's core functions are as follows:

## 1. Dependency Management

This is Maven's most important feature. When developing a project, we need external libraries (for example: Spring Framework, Hibernate, JUnit). Maven allows you to write the names and versions of these libraries (artifacts) in your project's main configuration file, pom.xml.

When you issue the command, Maven automatically downloads these libraries from a central repository (Maven Central), stores them in your local repository, and adds them to your project. This eliminates the hassle of manually downloading and adding libraries to your project.

## 2. Project Structure and Standardization

Maven defines a standard directory structure (folder layout) for projects. For example, source code is placed in the src/main/java folder, and test code in the src/test/java folder. This standardization allows developers working on different projects to easily understand the project's location and collaborate.

## 3. Automated Build Process

Maven automates the project's build process. It takes the project through a series of stages and defines a goal for each stage. These stages are:

Compile: Converts Java code into .class files.

Test: Runs tests on your project using tools like JUnit.

Package: Combines the compiled code and resources to create a .jar or .war file.

Install: Saves the built package to your local Maven repository for use by other projects.

All of these processes can be run automatically with a single command (such as mvn install).

## 4. Reporting and Documentation

Maven can generate various reports and documentation about your project. It simplifies project management by automatically reporting information such as the project's dependency list, test results, and code quality analysis.

In short, Maven simplifies the developer's work by consolidating a project's lifecycle (building, managing dependencies, compiling, testing, packaging, and deploying) under a single framework. This allows developers to focus directly on writing code rather than on the project's infrastructure.

# Installing maven

Firstly, we need to ensure **JAVA_HOME** enivronment variable exist. If it does not exist as environment variable set as permenantly as follows.  </p>

```bash
nano ~/.bashrc
```
Then, add the following code block to *.bashrc* then exit and save the file.</p>

``` bash
JAVA_HOME="lib/jvm/openjdk-21"
PATH= "$JAVA_HOME/bin:$PATH"
export PATH
```
After that run the following on terminal.
```bash
source ~/.bashrc
```
After that check the environment variable.</p>
```bash
echo $JAVA_HOME
java -version
```
Output: 
```
openjdk version "21.0.8" 2025-07-15
OpenJDK Runtime Environment (build 21.0.8+9-Ubuntu-0ubuntu124.04.1)
OpenJDK 64-Bit Server VM (build 21.0.8+9-Ubuntu-0ubuntu124.04.1, mixed mode, sharing)
```
Download Apache maven on the URL https://maven.apache.org/download.cgi </br>

Unzip the package by using following commands. </br>

```bash
unzip apache-maven-3.9.11-bin.zip
```

or

```bash
tar xzvf apache-maven-3.9.11-bin.tar.gz
```

Then copy or move the extracted folder to */opt/*

```bash
sudo cp -rf  apache-maven-3.9.11 /opt/
```

or 

```bash
sudo mv -rf  apache-maven-3.9.11 /opt/
```
Again open the .bashrc.
```bash
nano ~/.bashrc
```
add the following block to *.bashrc*.
```bash
M2_HOME="/opt/apache-maven-3.9.11"
PATH="$M2_HOME/bin:$PATH"
export PATH
```
The command source ~/.bashrc is used to apply the changes made in the ~/.bashrc file immediately to the current Bash session.
```bash
source ~/.bashrc
```

Check the maven by the code:
```bash
mvn -v
```
Output:
```
Apache Maven 3.9.11 (3e54c93a704957b63ee3494413a2b544fd3d825b)
Maven home: /opt/apache-maven-3.9.11
Java version: 21.0.8, vendor: Ubuntu, runtime: /usr/lib/jvm/java-21-openjdk-amd64
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "6.14.0-24-generic", arch: "amd64", family: "unix"
```

# Create first project

```bash
mvn archetype:generate -DgroupId=com.first.example -DartifactId=jcg-example -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```
By using the *mvn archetype:generate* command above, the first project has been initialized. </br>
-  **-DgroupID** declares the group id of project.
- **-DartifactId** declares the artifact id of project.
- **-DarchetypeArtifactId=maven-archetype-quickstart** this archetype will create for us a basic java project with maven directories conventions that will be packaged as a jar file.
- **-DinteractiveMode=false** This parameter prevents Maven from prompting the user for project details (Group ID, Artifact ID, etc.) and allows the user to use the values specified in the command directly. This allows the command to be run non-interactively.


The generate command will take a few seconds to complete if you are using Maven for the first time since it needs to download all necessary plugins and artifacts before it can begin the generation operation.
 As you can see, the chosen directory now has a new directory with the same name as the artifactId.  The updated directory structure is shown below.</br>

 ```
/jcg-example
    |
    ---- /src
            |
            ----/main/java/com/first/example
                    |
                    -----App.java
            |
            ----/test/java/com/first/example
                    |
                    -----AppTest.java
    |
    ----pom.xml
 ```

 To build your project, you can configure all project features, dependencies, repositories, plugins, etc. in a file called pom.xml (Project Object Model), which is defined by Maven.</p>

 Finally, by using Eclipse, the java project of this artifact is created and configurated as Maven project.

 # Hadoop

 ## The First "Hello-wrold"  Example

The following dependency block can be added into pom.xml (Project Object Managment) to use Hadoop.</br>

Firstly, we add the following block to pom.xml for hadoop dependency.

```
<dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-core</artifactId>
        <version>1.2.1</version>
</dependency>
```

### Mapper Code

*The MapClass.java* is added to **/jcg-example/src/main/java** folder.</br> 
The mapper task is responsible for tokenizing the input text based on space and create a list of words, then traverse over all the
tokens and emit a key-value pair of each word with a count of one, for example, <Hello, 1>. [1]</br>

Firstly, the code block will be explained line by line.</br>

```java
package com.first.example;
```
This code suggests us the MapClass is located in the **com.first.example** package.</br>


```java
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;
```
This code block shows us that the other java and hadoop packages are imported.</br>

```java
public class MapClass extends Mapper<LongWritable, Text, Text, IntWritable>
```
This declares a class named as **MapClass**</br>
- **extends Mapper** shows us the class is inherited from **Mapper** class.</br>
- <LongWritable, Text, Text, IntWritable>: This parameters  define the types of inputs and outputs of the **Mapper** class.</br>
  - **LongWritable**: The type of the key of the input.</br>
  - **Text**: The type of the value of the input.</br>
  - **Text**: The type of the key of the output.</br>
  - **IntWritable**: The type of the value of the output.</br>

```java
private final static IntWritable one = new IntWritable(1);
private Text word = new Text();
```
The code block firstly makes a **IntWritable** object which represents **1** for each words and the object is shared by all words since **static** and created only ones since it is **final**. </p>

Also, the **Text** object is created to store the each word.</br>


```java
@Override
    protected void map(LongWritable  key,
            Text value,
            Context context) throws IOException, InterruptedException 
```


- **@Override protected void map(...)** : This is the main method of the Mapper class. Hadoop calls this method once for each input line.

- key: Byte position of the input line.

- value: The line of text read.

- context: An object used to communicate with the Hadoop framework. We write the output of the Map stage with this object.

```java
String line = value.toString();
StringTokenizer st = new StringTokenizer(line, " ");
while(st.hasMoreTokens()) {
        word.set(st.nextToken());
        context.write(word, one);
}
```

- **String line = value.toString();** :Converts the incoming Text object to a standard Java String.

- **StringTokenizer st = new StringTokenizer(line, " ");**: Creates a StringTokenizer object to separate the text line in the line variable by the space (" ").

- **while(st.hasMoreTokens()) { ... }** : This loop runs as long as there are more words to parse in the line.

- **word.set(st.nextToken());** : Retrieves the next word from the StringTokenizer and sets the value of the word object to that word.

- **context.write(word, one);**: This is the most important output of the Mapper.

- word (word) is written to the context as the key, and one (1) is written to the context as the value.

For example, for the text "Hello World," this line runs twice: first it outputs (Hello, 1), and then it outputs (World, 1).</p>

The full code blow is below:</br>
```java
package com.first.example;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;
public class MapClass extends Mapper<LongWritable, Text, Text, IntWritable>{
	private final static IntWritable one = new IntWritable(1);
	private Text word = new Text();
	
	@Override
	protected void map(LongWritable  key,
			Text value,
			Context context) throws IOException, InterruptedException {
		String line = value.toString();
		StringTokenizer st = new StringTokenizer(line, " ");
		while(st.hasMoreTokens()) {
			word.set(st.nextToken());
			context.write(word, one);
		}
	}

}

```























# References

[1] https://www.javacodegeeks.com/wp-content/uploads/2016/05/Apache-Hadoop-Cookbook.pdf
