# Maximum-Websocket-connections-in-Tomcat
Tomcat server configuration to maximize active websocket connections at a time

Following configuration changes needs to be done in Tomcat -

# 1. {CATALINA_HOME}/conf/server.xml

  NIO Connector config -
  
  Connector connectionTimeout="-1" port="8080" protocol="org.apache.coyote.http11.Http11NioProtocol" redirectPort="8443"
maxConnections="100000" acceptCount="300"


# 2.  cat /proc/sys/net/ipv4/ip_local_port_range

Check the number of ports which are available for use in the m/c where Tomcat is deployed.

Change this to from 500 till 65535.

sysctl -w net.ipv4.ip_local_port_range="500   65535"

The above configuration changes allows around ~50k live connections in a 2GB Intel Core i5 machine provided the server and client are running in different machines.
