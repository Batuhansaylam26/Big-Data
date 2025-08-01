# Installing maven

Firstly, we need to ensure **JAVA_HOME** enivronment variable exist. If it does not exist as environment variable set as permenantly as follows.  </p>

```{bash}
sudo nano /etc/profile.local
```
Then, add the environment variable **JAVA_HOME="lib/jvm/<open-jdk folder>"** then exit and save the file.</p>

After that check the environment variable.</p>
```{bash}
echo $JAVA_HOME
```