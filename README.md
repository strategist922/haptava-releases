## Introduction

## Features

## Getting Started

### Download

	$ wget --no-check-certificate https://github.com/downloads/pambrose/JmxTalkReleases/JmxTalk-0.9.4.jar

### Xmpp Shell Access 

Using your favorite Xmpp client, login to jmxtalk.com with your username and add jmxtalk as a contact.

### Command Line Shell Access

	Usage: java com.jmxtalk.RemoteShell [-options]
	where options include:
		--usage                    print this message
		-v,--version               print version info and exit
		-u,--username  <value>     username value
		-p,--password  <value>     password value
		-s,--server    <url>       jmxtalk server url
		-f,--file      <filename>  script file name

Example:

    $ java -cp ./JmxTalk-0.9.4.jar com.jmxtalk.RemoteShell -u user1 -p topsecret -s jmxbridge://jmxtalk.com:7003

### Running the JmxTalk client for MBeanServers and JMX Proxies:

	Usage: java -jar JmxTalk-0.9.4.jar [-options]
	where options include:
		--usage                 print this message
		-v,--version            print version info and exit
		-p,--prop    <filename> properties file name
		-g,--group   <value>    group name value
		-c,--config  <value>    config name value
		-a,--auth    <value>    authorization token
		-s,--server  <url>      server url

Example:

    $ java -jar JmxTalk-0.9.4.jar -g devgroup -c prodserver -a extrasecret -s jmxbridge://jmxtalk.com:7003

### [Simple walk through] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/shellobjects)

## JavaDocs 
* [JmxTalk Shell Objects Reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/shellobjects)
* [JmxTalk Shell Variables Reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/shellvars)
* [JmxTalk MBeans Reference] (http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.4/mbeans)

## Shells
* [JmxTalk Shell](https://github.com/pambrose/JmxTalkReleases/wiki/JmxTalk-Shell)
* [MBean Shell](https://github.com/pambrose/JmxTalkReleases/wiki/MBean-Shell)

## [JmxQL](https://github.com/pambrose/JmxTalkReleases/wiki/JmxQL)

## Examples

* [MBeanServers](https://github.com/pambrose/JmxTalkReleases/wiki/MBeanServers)
* [MBeans](https://github.com/pambrose/JmxTalkReleases/wiki/MBeans)
* [Xmpp Beacons](https://github.com/pambrose/JmxTalkReleases/wiki/Beacons)
* [Timers and TimerTasks](https://github.com/pambrose/JmxTalkReleases/wiki/Timers)
* [MBean Notifications](https://github.com/pambrose/JmxTalkReleases/wiki/Notifications)


