JmxTalk Installation
========

Downloading the client
------

wget --no-check-certificate https://github.com/downloads/pambrose/JmxTalkReleases/JmxTalk-0.9.2.jar

Running the JmxTalk Client
------

Invoke the client with:

    java -jar JmxTalk-0.9.2.jar groupName sessionConfigName password url

For example:

	java -jar JmxTalk-0.9.2.jar acme config1 topsecret jmxbridge://jmxtalk.com:7003

JavaDocs
========

[[Javadocs]]

Shell objects reference: http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.2/shellobjects

MBeans reference: http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.2/mbeans

Shell variables description: http://pambrose.github.com/JmxTalkReleases/javadocs/0.9.2/shellvars

JmxTalk Syntax
========

Variable assignment
-----

    a = 4;
    b = "a string value";

Output
-----

    print(obj);
    print(vars);


Class information
-----

    describe(obj);


Constructors and method invocations
-----

    c = new String[]{"val1", "abcd".substring(2,3)};
    d = c[0].contains("va");
    print(d == true);


Operators
-----

    ++, --, +=, -=, ?:


Control flow statements
-----

    for (i = 0; i < 10; i++) System.out.println(i);
    for (i = 0; i < 10; i++) {print(i); a += i;}

    if (a < b) print(i); else print(j);
    if (a < b) print(i;
    if (a < b) {print(i); print(h);} else print(j);


Lambdas
-----

    a = #{String v1, String v2 -> print("Vals are " + v1 + " and " + v2);};
    a("Hello", "World");

    b = #System.describe;
    b(4 + 5);


Xmpp Beacons
------

    // Set up a beacon
    b = "testbeacon";
    b1 = BeaconAdmin.hasBeacon(b) ? BeaconAdmin.getBeacon(b) : BeaconAdmin.newBeacon(b, "secret");

    // Add a subscriber
    BeaconAdmin.getBeacon(b).addSubscriber("joe@foo.com", "Joe Jones");
    print(BeaconAdmin.getBeacon(b).getSubscribers());
    print(BeaconAdmin.getBeacon(b).getSubscriberCount());

    // Send a message to all beacon subscribers
    b1.sendMessage("Machine is down");

    // Set the status of a beacon
    b1.setStatus("Machine is busy");

    // Show the beacon as not available
    b1.setMode(Mode.away);

    // Delete a subscriber
    BeaconAdmin.getBeacon(b).deleteSubscriber("joe@foo.com");
    // or
    b1.deleteSubscriber(BeaconAdmin.getBeacon(b).getSubscribers()[0]);
    // or
    BeaconAdmin.deleteSubscribers();

    print(BeaconAdmin.getBeacon(b).getSubscriberCount());


Timers and TimerTasks
------

    // Create timer
    t1 = TimerAdmin.newTimer("timer1");

    // Add a task that shows % heap utilization
    task = t1.addTask("Update Mood Message", #{
        mb = MBeanServerAdmin.getServer("admin").getMBean("java.lang:type=Memory");
        mem = (double) (mb.HeapMemoryUsage.used) / (double) (mb.HeapMemoryUsage.max) * 100;
        beacon = BeaconAdmin.getBeacon("testbeacon");
        if (mem > 75)
            beacon.setMode(Mode.away);
        else
            beacon.setMode(Mode.available);
        beacon.setStatus(String.format("mem: %.2f%%", mem));
    });

    print(t1.getTasks());

    // Test the task
    task.fire();

    // Set the task's interval
    task.setIntervalSecs(10);

    // Pause and resume task
    task.pause();
    task.resume();

    // Delete a task
    t1.deleteTask(task);

    // Delete timer
    TimerAdmin.deleteTimer(t1);


MBeanServers
------

    // Create 3 MBeanServers that use client bc1
    MBeanServerAdmin.newServer("f1", "service:jmx:rmi:///jndi/rmi://remotehost1:9999/jmxrmi");
    MBeanServerAdmin.newServer("f2", "service:jmx:rmi:///jndi/rmi://remotehost2:9999/jmxrmi");
    MBeanServerAdmin.newServer("f3", "service:jmx:rmi:///jndi/rmi://remotehost3:9999/jmxrmi");

    // Verify the servers are present
    print(MBeanServerAdmin.getServers());
	// or
	print(mbeanServers);

    // Referencing the servers
    f1 = MBeanServerAdmin.getServers()[0];
    f2 = MBeanServerAdmin.getServer("f2");
 	f3 = mbeanServers[2];

MBeanServerGroups
------

    // Create a new group called g1
    g1 = MBeanServerGroupAdmin.newGroup("g1");

    // Add 3 servers to it
    g1.addServer(MBeanServerAdmin.getServer("f1"));
    g1.addServer("f2");
    g1.addServer(f3);

    // Verify servers were added
    print(g1.getServers());

    // Get MBeanCount for all servers in group
    print(a.getMBeanCount());

MBeans
------

    print(MBeanServerAdmin.getServers()[0].getMBeans());
    mb1 = f1.getMBeans()[4];
    mb1 = f1.getMBean("java.lang:type=Runtime");
    describe(mb1);
    print(mb1);

    // MBean attributes and methods are referenced like pojos
    print(mb1.attrib);
    print(mb1.getValue());
    mb1.setValue(44);


MBean queries using JmxQL
------

    print(f1.getMBeans("*:*"));
    print(f1.getMBeans("*:*", "not instanceof 'com.foo.JmxTest'"));
    print(f1.getMBeans("com.foo:*", "Val2 > 4 AND Val5 > 9"));
    print(f1.getMBeans("com.foo:*", "Val2 IN (2, 4)"));
    print(f1.getMBeans("com.foo:*", "Val2 not IN (2, 4)"));
    print(f1.getMBeans("com.foo:*", "com.foo.JmxTest.Val2 between 2 AND 4"));
    print(f1.getMBeans("com.foo:*", "Val2 between 2 AND 4")
    print(f1.getMBeans("com.foo:*", "Val2 not between 2 AND 4 OR not (Val3 between 2 AND 4)"));
    print(f1.getMBeans("com.foo:*", "Val1 like '*'"));
    print(f1.getMBeans("com.foo:*", "Val1 not like '*'"));
    print(f1.getMBeans("com.foo:*", "Val1 like '*2'"));
    print(f1.getMBeans("com.foo:*", "not (Val1 like '*2')"));
    print(f1.getMBeans("com.foo:*", "Val1 begins with 'v'"));
    print(f1.getMBeans("com.foo:*", "Val1 not begins with 'v'"));
    print(f1.getMBeans("com.foo:*", "Val1 ends with 'f'"));
    print(f1.getMBeans("com.foo:*", "Val1 not ends with 'f'"));
    print(f1.getMBeans("com.foo:*", "Val1 contains 'g'"));
    print(f1.getMBeans("com.foo:*", "Val1 not contains 'k'"));
    print(f1.getMBeans("*:*", "like '*Jmx*'"));
    print(f1.getMBeans("*:*", "not like '*Jmx*'"));
    print(f1.getMBeans("*:*", "not (like '*Jmx*')"));
    print(f1.getMBeans("*:*", "begins with 'com'"));
    print(f1.getMBeans("*:*", "not begins with 'com'"));
    print(f1.getMBeans("*:*", "ends with 'est'"));
    print(f1.getMBeans("*:*", "not ends with 'est'"));
    print(f1.getMBeans("*:*", "contains 'jmxtalk'"));
    print(f1.getMBeans("*:*", "not contains 'memset'"));
    print(f1.getMBeans("*:*", "begins with 'com'")[0]);

JmxQL is described here: <http://weblogs.java.net/blog/emcmanus/archive/2008/04/a_query_languag.html>

MBean Notifications
------

    // Create a notification listener
    nl = NotificationAdmin.newListener("nl1", #{Notification notification, MBean mbean -> Log.info("red flag");}, mbean1);

    // Change the listener action
    nl.setAction(#{Notification notification, MBean mbean -> Log.info("blue flag");});

    // Filter the notifications
    nl.setFilterAction(#{Notification notification, String objectName -> return !objectName.contains("foo");});

    // Pause and resume the listener
    nl.pause();
    nl.resume();

    // Delete the listener
    NotificationAdmin.removeListener("nl1");

