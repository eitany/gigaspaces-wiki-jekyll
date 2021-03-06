---
layout: post
title:  Connections View - GigaSpaces Browser
categories: XAP97
parent: gigaspaces-browser-tree-panel-and-configuration-panel.html
weight: 100
---

{% summary page|60 %}Displays information regarding all connected and disconnected proxies.{% endsummary %}

# Overview

The Connections view exposes information regarding all connected and disconnected space proxies.

{% lampon %} It is also possible to retrieve space connections using the **[space connections](./space-connections---gigaspaces-cli.html)** command

The following properties are exposed:

- Server IP address and port
- Client IP address and port
- Start connection time
- Connection status
- Disconnection time

The Connections view is accessible for each space node. The red highlighted rows in the screenshot below are disconnected connections.

{% indent %}
![Connections View1.gif](/attachment_files/Connections View1.gif)
{% endindent %}

You can clean the displayed disconnections and view only live connections by clicking the **Clean disconnections** button on the top right.

# Refresh Options

You can choose to refresh the Connection view periodically. Select the desired refresh rate from the drop-down menu. To stop automatically refreshing the Connections view, click the **Stop* button. The refresh activity impacts server performance, so when running benchmarks you might want to stop auto-refresh activity (by clicking the *Stop** button). When auto-refresh is running, a green blinking dot is displayed on the right side of the screen.

{% indent %}
![GMC_space_x_RefreshRate_area_TopRight_6.0.gif](/attachment_files/GMC_space_x_RefreshRate_area_TopRight_6.0.gif)
{% endindent %}

# Considerations

- {% infosign %} Connections are created for a space **only when a space operation (eg. ping, write, etc.) is invoked**.
- Information relates only to physical (live) connections. Logical connections will be shown in the future.
- Disconnected connections are calculated and displayed only on the client side and are not supplied by MBean methods.

