## Introduction

## Features

## Getting Started

### Download the client

	wget --no-check-certificate https://github.com/downloads/pambrose/JmxTalkReleases/JmxTalk-0.9.4.jar

### Using a Xmpp client
Using your favorite Xmpp client, login to jmxtalk.com with your username and add jmxtalk as a contact.

### Running the Remote Shell
Invoke the client with:

    java -cp ./JmxTalk-0.9.4.jar -u username -p password -s url

Example:

    $ java -cp ./JmxTalk-0.9.4.jar -u user1 -p topsecret -s jmxbridge://jmxtalk.com:7003

### Running the JMX Proxy:

Invoke the JMX proxy with:

    java -jar JmxTalk-0.9.4.jar -g groupName -c configName -a authenticationToken -s url

Example:

    $ java -jar JmxTalk-0.9.4.jar -g acme -c config1 -a extrasecret -s jmxbridge://jmxtalk.com:7003

## JavaDocs 
* [Shell objects reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/shellobjects)
* [MBeans reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/mbeans)
* [Shell variables reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/shellvars)

## Shells
* [JmxTalk Shell](https://github.com/pambrose/JmxTalkReleases/wiki/JmxTalk-Shell)
* [MBean Shell](https://github.com/pambrose/JmxTalkReleases/wiki/MBean-Shell)

## [JmxQL](https://github.com/pambrose/JmxTalkReleases/wiki/JmxQL)

## Examples

* [Xmpp Beacons](https://github.com/pambrose/JmxTalkReleases/wiki/Beacons)
* [Timers and TimerTasks](https://github.com/pambrose/JmxTalkReleases/wiki/Timers)
* [MBeanServers](https://github.com/pambrose/JmxTalkReleases/wiki/MBeanServers)
* [MBeans](https://github.com/pambrose/JmxTalkReleases/wiki/MBeans)
* [MBean Notifications](https://github.com/pambrose/JmxTalkReleases/wiki/Notifications)

