---
layout: post
title:  Space JMX Management
categories: XAP97
parent: managing-and-monitoring-a-running-system.html
weight: 500
---

{% summary %}Controlling space attributes and operations using the JMX console. {% endsummary %}

# Overview

The Java Management Extensions (JMX specification) describe an architecture, design patterns, API's, and services for application and network management in the Java programming language. JMX functions beyond a simple API since it can specify the architecture as to how that API is used. It provides the means to construct Java code, create smart Java agents, implement distributed management middleware and managers, and integrate these solutions smoothly into existing management systems. You can integrate such solutions with either HTML or industry standards such as SNMP and WBEM. JMX is dynamic, allowing the monitoring and management of resources in real time while they are created, installed, and implemented. The JMX also works along with JVM, the Java Virtual Machine.

{% refer %}For more details about JMX, refer to: [http://java.sun.com/products/JavaManagement/](http://java.sun.com/products/JavaManagement/).{% endrefer %}

## Manageable Resource

A JMX manageable resource can be an application, an implementation of a service, a device, a user, etc. It is developed in Java, or at least offers a Java wrapper, and must also be implemented by a Java object called a managed bean (MBeans), according to JMX specifications.

# Opening JMX

1. The easiest way to open JConsole for a specific service is through the GigaSpaces Management Center:
    - In the Deployments tab, right-click the GSC, GSM, or LookupService tree node, or
    - In the Space Browser tab:
        - In the Grid Tree, right-click the relevant [space container node](./gigaspaces-browser-tree-panel-and-configuration-panel.html#Container Node), or {% wbr %} ![space_JMX_1_GMC_space_LaunchingJConsoleFromContainerNode_6.5.jpg](/attachment_files/space_JMX_1_GMC_space_LaunchingJConsoleFromContainerNode_6.5.jpg)
        - Right-click the relevant [space node](./gigaspaces-browser-tree-panel-and-configuration-panel.html#Space Node) or clustered space node, or {% wbr %}![space_JMX_2_GMC_space_LaunchingJConsoleFromSpaceNode_6.5.jpg](/attachment_files/space_JMX_2_GMC_space_LaunchingJConsoleFromSpaceNode_6.5.jpg)
        - Right-click the relevant space from the [space network view](./gigaspaces-browser-tree-panel-and-configuration-panel.html#Spaces Network View):{% wbr %}![space_JMX_3_GMC_space_network_LaunchingJconsole_6.5.jpg](/attachment_files/space_JMX_3_GMC_space_network_LaunchingJconsole_6.5.jpg)

1. Click **Launch JConsole**.
1. This opens the JConsole (only if you are running JDK 1.5 and above) of the selected process.
1. You can browse the various MBeans.
1. Make sure you have a deployed space.
1. Open a console and type the following command:{% wbr %}`jconsole`{% wbr %}{% infosign %} By default, operations in the MBeans **Operations** tab which have GigaSpaces classes as their type are disabled. To enable these, type{% wbr %}`jconsole -J-Djava.class.path=%JAVA_HOME%\lib\jconsole.jar;GS_HOME\lib\JSpaces.jar`{% wbr %}in your console. Instead of `GS_HOME`, type the directory in which GigaSpaces is installed on your computer.

1. Connect to the MBean server (choose one of the following options):
    - Using the **Advanced** tab:
        1. The JConsole: Connect to Agent window appears. Select the **Advanced** tab.
        1. In the **JMX URL** text box, copy the URL in the log message displayed in your GigaSpaces Server, for example:{% wbr %}INFO:{% wbr %}`New JMXConnectionServer was successfully registered into the MBeanServer using service url:{% wbr %}service:jmx:rmi:///jndi/rmi://localhost:10098/jmxrmi`{% wbr %}
            ![space_JMX_4_space_JMX_IMG992.gif](/attachment_files/space_JMX_4_space_JMX_IMG992.gif)
        1. Press **Connect**.
    - Using the **Remote** tab:
        1. The JConsole: Connect to Agent window appears. Select the **Remote** tab.
        1. In the **Host or IP** text box, copy the host name/IP address from JNDI URL text field in the container configuration.
        1. In the **Port** text box, copy the port value from the same JNDI URL text field in the container configuration.{% wbr %}
            ![space_JMX_5_GMC_space_containerNodeSelected_directoy_services_tab_6.1.jpg](/attachment_files/space_JMX_5_GMC_space_containerNodeSelected_directoy_services_tab_6.1.jpg){% wbr %}
            ![space_JMX_6_jconsole_connect.jpg](/attachment_files/space_JMX_6_jconsole_connect.jpg)
        1. Press **Connect**.{% wbr %}Here is a code example of implementing such an approach:{% wbr %}
            `IJSpace spaceProxy = ( IJSpace )SpaceFinder.find( "jini://mySpace_container/mySpace");`{% wbr %}
            `System.out.println( "Space found: " + spaceProxy.toString() );`{% wbr %}
            `ContainerConfig containerConfig = ( ( IJSpaceContainerAdmin )spaceProxy.getContainer() ).getConfig();`{% wbr %}
            `String jndiURL = containerConfig.jndiUrl;`{% wbr %}
            `Runtime.getRuntime().exec( "jconsole " + jndiURL );`{% wbr %}

{% include /COM/jconsolejmapwarning.markdown %}

# Remote JConsole connection

In order to enable monitoring and management from remote systems using JMX jconsole set the following system properties or use the setenv shell variable **REMOTE_JMX**

    REMOTE_JMX=-Dcom.sun.management.jmxremote.port=5001 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false

# Viewing Thread CPU Usage with JDK 1.6

JConsole includes a [new tab](http://blog.luminis.nl/luminis/entry/top_threads_plugin_for_jconsole) that displays CPU usage for each JVM thread. This tab is displayed using the [-pluginpath](http://java.sun.com/javase/6/docs/technotes/guides/management/jconsole.html) JConsole parameter (already implemented in GigaSpaces).

**To view this tab in your JConsole**:

- Install **[JDK 1.6](http://java.sun.com/javase/downloads/index.jsp)** -- download **JDK 6 Update 2** as seen below:

{% indent %}
![space_JMX_7_JDK6.jpg](/attachment_files/space_JMX_7_JDK6.jpg)
{% endindent %}

- **[Download the topthreads.jar file](http://blog.luminis.nl/luminis/resource/peter/topthreads.jar)** and add it to your `<GigaSpaces Root>\lib\ui` folder.

{% infosign %} `topthreads.jar` is used by default. If `topthreads.jar` isn't found, the `JTop.jar` file (which is part of the JDK) is used instead.

Below are some example screenshots:

## topthread.jar

{% indent %}
![space_JMX_8_top_threads.jpg](/attachment_files/space_JMX_8_top_threads.jpg)
{% endindent %}

## JTop.jar

{% indent %}
![space_JMX_9_j_top.jpg](/attachment_files/space_JMX_9_j_top.jpg)
{% endindent %}

# MBeans View

The jconsole utility (part of Sun J2SE 5.0 JDK and above) includes a **MBeans** view, which allows you to perform space administration operations, and to view and control space attributes. These operations are defined in the [JavaSpaceMBeanDescriptors.xml](http://www.gigaspaces.com/wiki/download/attachments/15078/JavaSpaceMBeanDescriptors.xml) file, which exists in the `JSpaces.jar` file. If you do not want a certain operation or attribute to be exposed in the JMX **MBeans** tab, simply comment or remove the operation from the XML file.

## Space Container MBean

The container MBean exposes the space container's attributes and operations. The space container manages the space life cycle.

### Attributes Tab

The container **Attributes** tab displays a list of container attributes. Attribute values appearing in blue can be controlled, while values in black can not be changed. Red values are unavailable.

{% indent %}
![space_JMX_10_IMG994.gif](/attachment_files/space_JMX_10_IMG994.gif)
{% endindent %}

### Operations Tab

The container **Operations** tab allows you to perform different space container operations:

- **shutdown** -- shuts down this container.
- **restart** -- restarts this container.
- **destroySpace** -- destroys a space in this container (type the space's name in the **spaceName** text box).
- **createSpace (spaceName, schemaName, clusterConfigURL)** -- creates a space with a unique name in this container and writes the created space to the appropriate Storage Adapter. (Type the name of the space, the name of the schema, and the cluster configuration URL\*\*\* in the relevant text boxes).
- **createSpace (spaceName, schemaName)** -- creates a space with a unique name in this container.
- **getRuntimeConfigReport** -- displays a runtime configuration report. For more details, refer to the [Runtime Configuration Report](./space-container-configuration-general-tab---gigaspaces-browser.html#Runtime Configuration Report) section.

{% indent %}
![space_JMX_11_IMG995.gif](/attachment_files/space_JMX_11_IMG995.gif)
{% endindent %}

### Info Tab

The container **Info** tab displays the MBean name and its Java class.

{% indent %}
![space_JMX_12_IMG996.gif](/attachment_files/space_JMX_12_IMG996.gif)
{% endindent %}

## Space MBean

The Space MBean exposes space attributes and operations. You can get the basic space operational settings using this MBean.

### Attributes Tab

The space **Attributes** tab displays a list of space attributes/elements by XPath, in the selected space. Attribute values appearing in blue can be controlled, while values in black can not be changed. Red values are unavailable.

{% refer %}For details on specific configuration file elements, refer to the Configuration Files Element List\*** section.{% endrefer %}

{% indent %}
![space_JMX_13_IMG993.gif](/attachment_files/space_JMX_13_IMG993.gif)
{% endindent %}

{% anchor 1 %}

### Operations Tab

The space **Operations** tab allows you to perform different space operations:

- **getSpace** -- returns the space proxy that this manageable bean governs.
- **getStatistics** -- returns a `StatisticsContext` according to the operation code you type in the **operationCode** text box -- each operation has a constant representing it.

{% refer %}For a list of operation codes, see [Javadoc](http://www.gigaspaces.com/docs/JavaDoc{% currentversion %}/index.html?com/j_spaces/core/filters/FilterOperationCodes.html) and the [statistics filter operation codes list](http://www.gigaspaces.com/docs/JavaDoc/constant-values.html#com.j_spaces.core.filters.FilterOperationCodes.AFTER_ALL_NOTIFY_TRIGGER).{% endrefer %}

{% refer %}For more details, see [com.j_spaces.core.admin.StatisticsAdmin](http://www.gigaspaces.com/docs/JavaDoc{% currentversion %}/index.html?com/j_spaces/core/admin/StatisticsAdmin.html) or [com.j_spaces.core.filters.StatisticsContext](http://www.gigaspaces.com/docs/JavaDoc{% currentversion %}/index.html?com/j_spaces/core/filters/StatisticsContext.html).{% endrefer %}

- **clean** -- cleans the selected space.
- **count** -- when entering a specific class name in the **className** textbox, displays the number of Entries in this class.
- **clear** -- when entering a specific class name in the **className** textbox, removes the Entries that match this template from the space.
- **stop** -- attempts to stop the selected space.
- **start** -- attempts to start the selected space.
- **ping** -- checks whether the space is alive and accessible.
- **restart** -- restarts the space.
- **getClusterPolicy** -- displays a cluster policy instance.
- **getRuntimeInfo** -- returns a RuntimeInfo instance.
{% refer %}For more details, see [Javadoc](http://www.gigaspaces.com/docs/JavaDoc{% currentversion %}/index.html?com/j_spaces/core/admin/SpaceRuntimeInfo.html).{% endrefer %}

- **getURL** -- displays the `spaceURL` instance which was used to initialize the space.

{% indent %}
![space_JMX_14_IMG997.gif](/attachment_files/space_JMX_14_IMG997.gif)
{% endindent %}

### Info Tab

The space **Info** tab displays the MBean name and its Java class.

{% indent %}
![space_JMX_15_IMG998.gif](/attachment_files/space_JMX_15_IMG998.gif)
{% endindent %}

## Space MBean Extension

The Space MBean Extension exposes advanced space attributes -- this includes memory management, persistency and communication settings.

### Attributes Tab

The space extensions **Attributes** tab displays a list of advanced space attributes/elements by XPath, in the selected space. Attribute values appearing in blue can be controlled, while values in black can not be changed. Red values are unavailable.

{% refer %}For details on specific configuration file elements, refer to the Configuration Files Element List\*** section. {% endrefer %}

{% indent %}
![space_JMX_16_IMG999.gif](/attachment_files/space_JMX_16_IMG999.gif)
{% endindent %}

### Info Tab

The space extensions **Info** tab displays the MBean name and its Java class.

{% indent %}
![space_JMX_17_IMG200.gif](/attachment_files/space_JMX_17_IMG200.gif)
{% endindent %}

# Restricting and Modifying MBeans

There is an option to restrict the access to space and space container operations or attributes; for example, you can decide to hide some of the attributes and configuration, and disable execution of operations.

{% infosign %} This way, you can view, restrict or modify most of the space and space container **configuration** (as set in the space/container schema files), or the basic **admin operations**, which were discussed in the above sections.

To do this, modify the following space and space container **MBean Descriptors**, which are located inside the `<GigaSpaces Root>\lib\JSpaces.jar` file:

- `ContainerMBeanDescriptors.xml`
- `JavaSpaceExtMBeanDescriptors.xml`
- `JavaSpaceMBeanDescriptors.xml`

## Settings to Modify

Following are some space/space container MBeans **Attributes** settings you can modify:

- **Attribute** -- required, otherwise is optional.
- **name** -- the name of the attribute.
- **type** - The type or class name of the attribute.
- **description** -- a description of the attribute.
- **isReadable** -- true if the attribute has a getter method, false otherwise.
- **isWritable** -- true if the attribute has a setter method, false otherwise.

Following are some space/space container MBeans **Operations** settings you can modify:

- **Operation** -- required, otherwise optional.
- **name** -- the name of the method.
- **type** -- the type of the method's return value.
- **impact** -- the impact of the method, one of `INFO`, `ACTION`, `ACTION_INFO`, `UNKNOWN`.
- **description** -- a description of the operation.
- **signature** -- `MBeanParameterInfo` objects describing the parameters (arguments) of the method.
- **Signature** -- the list of parameters info.
    - **Parameter** -- required, otherwise optional.
    - **name** -- the name of the data.
    - **type** - the type or class name of the data.

# Getting Space Statistics using the JMX API

See [example of JMX API usage](/sbp/jmx-space-statistics.html).


