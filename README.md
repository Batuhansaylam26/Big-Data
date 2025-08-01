# Installing maven

Firstly, we need to ensure **JAVA_HOME** enivronment variable exist. If it does not exist as environment variable set as permenantly as follows.  </p>

```{bash}
nano ~/.bashrc
```
Then, add the following code block to *.bashrc* then exit and save the file.</p>

``` {bash}
JAVA_HOME="lib/jvm/openjdk-21"
PATH= "$JAVA_HOME/bin:$PATH"
export PATH
```
After that run the following on terminal.
```{bash}
source ~/.bashrc
```
After that check the environment variable.</p>
```{bash}
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

```{bash}
unzip apache-maven-3.9.11-bin.zip
```

or

```{bash}
tar xzvf apache-maven-3.9.11-bin.tar.gz
```

Then copy or move the extracted folder to */opt/*

```{bash}
sudo cp -rf  apache-maven-3.9.11 /opt/
```

or 

```{bash}
sudo mv -rf  apache-maven-3.9.11 /opt/
```
Again open the .bashrc.
```{bash}
nano ~/.bashrc
```
add the following block to *.bashrc*.
```{bash}
M2_HOME="/opt/apache-maven-3.9.11"
PATH="$M2_HOME/bin:$PATH"
export PATH
```
The command source ~/.bashrc is used to apply the changes made in the ~/.bashrc file immediately to the current Bash session.
```{bash}
source ~/.bashrc
```

Check the maven by the code:
```{bash}
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