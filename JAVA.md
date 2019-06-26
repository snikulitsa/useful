# JAVA
Installation
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
Run spring boot app with profile:  
```bash
sudo java -jar -Dspring.profiles.active=profile_name app.jar
```

Run app with remote `JMX` access:  
```bash
sudo java -jar -Dcom.sun.management.jmxremote.port=6666 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false app.jar
```

Run app with remote **Debug** availability:  
```bash
sudo java -Xdebug -Xrunjdwp:transport=dt_socket,address=7777,server=y,suspend=y -jar app.jar
```
Command | Semantic
------- | --------
`suspend=y` | don't start app until remote debug connected
`suspend=n` | run the app immediately