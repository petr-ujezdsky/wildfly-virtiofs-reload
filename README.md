# Wildfly redeploying under VirtioFS - reproduction

This repo reproduces the issue with Wildfly constantly redeploying applications inside Docker for Desktop with VirtioFS enabled.

The example war is from [here](https://github.com/efsavage/hello-world-war/raw/master/dist/hello-world.war).

## Steps to reproduce:
1. Enable VirtioFS in Docker for Desktop
2. Start the app using `start.sh`
3. Observe console logs

## Expected result:
The war deploys once and stays deployed.
```
$ ./start.sh
=========================================================================

  JBoss Bootstrap Environment

  JBOSS_HOME: /opt/jboss/wildfly

  JAVA: /usr/lib/jvm/java/bin/java

  JAVA_OPTS:  -server -Xms64m -Xmx512m -XX:MetaspaceSize=96M -XX:MaxMetaspaceSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=org.jboss.byteman -Djava.awt.headless=true  --add-exports=java.desktop/sun.awt=ALL-UNNAMED --add-exports=java.naming/com.sun.jndi.ldap=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.lang.invoke=ALL-UNNAMED --add-opens=java.base/java.lang.reflect=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.security=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.management/javax.management=ALL-UNNAMED --add-opens=java.naming/javax.naming=ALL-UNNAMED

=========================================================================

10:11:58,138 INFO  [org.jboss.modules] (main) JBoss Modules version 2.0.0.Final
10:11:58,745 INFO  [org.jboss.msc] (main) JBoss MSC version 1.4.13.Final
10:11:58,755 INFO  [org.jboss.threads] (main) JBoss Threads version 2.4.0.Final
10:11:58,919 INFO  [org.jboss.as] (MSC service thread 1-2) WFLYSRV0049: WildFly Full 26.0.1.Final (WildFly Core 18.0.4.Final) starting
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.wildfly.extension.elytron.SSLDefinitions (jar:file:/opt/jboss/wildfly/modules/system/layers/base/org/wildfly/extension/elytron/main/wildfly-elytron-integration-18.0.4.Final.jar!/) to method com.sun.net.ssl.internal.ssl.Provider.isFIPS()
WARNING: Please consider reporting this to the maintainers of org.wildfly.extension.elytron.SSLDefinitions
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
10:11:59,780 INFO  [org.wildfly.security] (ServerService Thread Pool -- 26) ELY00001: WildFly Elytron version 1.18.3.Final
10:12:00,406 INFO  [org.jboss.as.repository] (ServerService Thread Pool -- 37) WFLYDR0001: Content added at location /opt/jboss/wildfly/standalone/data/content/47/9d6ceb6ebe7b2e5dcf8c36e0b177813526181c/content
10:12:00,467 INFO  [org.jboss.as.server] (Controller Boot Thread) WFLYSRV0039: Creating http management service using socket-binding (management-http)
10:12:00,487 INFO  [org.xnio] (MSC service thread 1-8) XNIO version 3.8.5.Final
10:12:00,496 INFO  [org.xnio.nio] (MSC service thread 1-8) XNIO NIO Implementation Version 3.8.5.Final
10:12:00,563 INFO  [org.wildfly.extension.elytron.oidc._private] (ServerService Thread Pool -- 52) WFLYOIDC0001: Activating WildFly Elytron OIDC Subsystem
10:12:00,566 INFO  [org.jboss.as.clustering.infinispan] (ServerService Thread Pool -- 54) WFLYCLINF0001: Activating Infinispan subsystem.
10:12:00,566 INFO  [org.wildfly.extension.health] (ServerService Thread Pool -- 53) WFLYHEALTH0001: Activating Base Health Subsystem
10:12:00,568 INFO  [org.jboss.as.jaxrs] (ServerService Thread Pool -- 56) WFLYRS0016: RESTEasy version 4.7.4.Final
10:12:00,570 INFO  [org.wildfly.extension.io] (ServerService Thread Pool -- 55) WFLYIO001: Worker 'default' has auto-configured to 16 IO threads with 128 max task threads based on your 8 available processors
10:12:00,584 INFO  [org.jboss.as.connector.subsystems.datasources] (ServerService Thread Pool -- 44) WFLYJCA0004: Deploying JDBC-compliant driver class org.h2.Driver (version 1.4)
10:12:00,584 INFO  [org.jboss.as.connector] (MSC service thread 1-4) WFLYJCA0009: Starting Jakarta Connectors Subsystem (WildFly/IronJacamar 1.5.3.Final)
10:12:00,601 WARN  [org.jboss.as.txn] (ServerService Thread Pool -- 74) WFLYTX0013: The node-identifier attribute on the /subsystem=transactions is set to the default value. This is a danger for environments running multiple servers. Please make sure the attribute value is unique.
10:12:00,608 INFO  [org.jboss.as.connector.deployers.jdbc] (MSC service thread 1-4) WFLYJCA0018: Started Driver service with driver-name = h2
10:12:00,614 INFO  [org.wildfly.extension.microprofile.jwt.smallrye] (ServerService Thread Pool -- 65) WFLYJWT0001: Activating MicroProfile JWT Subsystem
10:12:00,626 INFO  [org.wildfly.extension.microprofile.opentracing] (ServerService Thread Pool -- 66) WFLYTRACEXT0001: Activating MicroProfile OpenTracing Subsystem
10:12:00,626 INFO  [org.wildfly.extension.metrics] (ServerService Thread Pool -- 63) WFLYMETRICS0001: Activating Base Metrics Subsystem
10:12:00,652 INFO  [org.jboss.remoting] (MSC service thread 1-8) JBoss Remoting version 5.0.23.Final
10:12:00,662 INFO  [org.wildfly.extension.microprofile.config.smallrye] (ServerService Thread Pool -- 64) WFLYCONF0001: Activating MicroProfile Config Subsystem
10:12:00,679 INFO  [org.jboss.as.webservices] (ServerService Thread Pool -- 76) WFLYWS0002: Activating WebServices Extension
10:12:00,680 INFO  [org.jboss.as.naming] (ServerService Thread Pool -- 67) WFLYNAM0001: Activating Naming Subsystem
10:12:00,698 INFO  [org.jboss.as.jsf] (ServerService Thread Pool -- 61) WFLYJSF0007: Activated the following Jakarta Server Faces Implementations: [main]
10:12:00,813 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) WFLYUT0003: Undertow 2.2.14.Final starting
10:12:00,827 WARN  [org.wildfly.extension.elytron] (MSC service thread 1-2) WFLYELY00023: KeyStore file '/opt/jboss/wildfly/standalone/configuration/application.keystore' does not exist. Used blank.
10:12:00,823 INFO  [org.jboss.as.naming] (MSC service thread 1-3) WFLYNAM0003: Starting Naming Service
10:12:00,834 INFO  [org.jboss.as.mail.extension] (MSC service thread 1-3) WFLYMAIL0001: Bound mail session [java:jboss/mail/Default]
10:12:00,880 WARN  [org.wildfly.extension.elytron] (MSC service thread 1-8) WFLYELY01084: KeyStore /opt/jboss/wildfly/standalone/configuration/application.keystore not found, it will be auto generated on first use with a self-signed certificate for host localhost
10:12:00,997 INFO  [org.jboss.as.ejb3] (MSC service thread 1-5) WFLYEJB0482: Strict pool mdb-strict-max-pool is using a max instance size of 32 (per class), which is derived from the number of CPUs on this host.
10:12:00,997 INFO  [org.jboss.as.ejb3] (MSC service thread 1-6) WFLYEJB0481: Strict pool slsb-strict-max-pool is using a max instance size of 128 (per class), which is derived from thread worker pool sizing.
10:12:01,012 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 75) WFLYUT0014: Creating file handler for path '/opt/jboss/wildfly/welcome-content' with options [directory-listing: 'false', follow-symlink: 'false', case-sensitive: 'true', safe-symlink-paths: '[]']
10:12:01,046 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-5) WFLYUT0012: Started server default-server.
10:12:01,054 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) Queuing requests.
10:12:01,056 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) WFLYUT0018: Host default-host starting
10:12:01,134 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-2) WFLYUT0006: Undertow HTTP listener default listening on 0.0.0.0:8080
10:12:01,223 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-6) WFLYUT0006: Undertow HTTPS listener https listening on 0.0.0.0:8443
10:12:01,273 INFO  [org.jboss.as.ejb3] (MSC service thread 1-2) WFLYEJB0493: Jakarta Enterprise Beans subsystem suspension complete
10:12:01,346 INFO  [org.jboss.as.connector.subsystems.datasources] (MSC service thread 1-2) WFLYJCA0001: Bound data source [java:jboss/datasources/ExampleDS]
10:12:01,555 INFO  [org.jboss.as.patching] (MSC service thread 1-6) WFLYPAT0050: WildFly Full cumulative patch ID is: base, one-off patches include: none
10:12:01,562 INFO  [org.jboss.as.server.deployment.scanner] (MSC service thread 1-2) WFLYDS0013: Started FileSystemDeploymentService for directory /opt/jboss/wildfly/standalone/deployments
10:12:01,569 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-6) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:12:01,641 INFO  [org.jboss.ws.common.management] (MSC service thread 1-4) JBWS022052: Starting JBossWS 5.4.4.Final (Apache CXF 3.4.5)
10:12:02,472 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000128: Infinispan version: Infinispan 'Taedonggang' 12.1.7.Final
10:12:02,536 INFO  [org.infinispan.CONFIG] (MSC service thread 1-6) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
10:12:02,538 INFO  [org.infinispan.CONFIG] (MSC service thread 1-6) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
10:12:02,592 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000556: Starting user marshaller 'org.wildfly.clustering.infinispan.spi.marshalling.InfinispanProtoStreamMarshaller'
10:12:02,690 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000025: wakeUpInterval is <= 0, not starting expired purge thread
10:12:02,716 INFO  [org.jboss.as.clustering.infinispan] (ServerService Thread Pool -- 78) WFLYCLINF0002: Started http-remoting-connector cache from ejb container
10:12:02,847 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:12:02,913 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 45) WFLYSRV0010: Deployed "hello-world.war" (runtime-name : "hello-world.war")
10:12:02,969 INFO  [org.jboss.as.server] (Controller Boot Thread) WFLYSRV0212: Resuming server
10:12:02,976 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0025: WildFly Full 26.0.1.Final (WildFly Core 18.0.4.Final) started in 5227ms - Started 399 of 601 services (341 services are lazy, passive or on-demand)
10:12:02,979 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0060: Http management interface listening on http://127.0.0.1:9990/management
10:12:02,979 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0051: Admin console listening on http://127.0.0.1:9990
```

## Actual result
The war deploys, undeploys and deploys again every 5 seconds.

The 5000 miliseconds is the default value for `scan-interval` in `deployment-scanner` in Wildfly which looks for deployment changes and redeploys apps if changed.

```
$ ./start.sh
=========================================================================

  JBoss Bootstrap Environment

  JBOSS_HOME: /opt/jboss/wildfly

  JAVA: /usr/lib/jvm/java/bin/java

  JAVA_OPTS:  -server -Xms64m -Xmx512m -XX:MetaspaceSize=96M -XX:MaxMetaspaceSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=org.jboss.byteman -Djava.awt.headless=true  --add-exports=java.desktop/sun.awt=ALL-UNNAMED --add-exports=java.naming/com.sun.jndi.ldap=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.lang.invoke=ALL-UNNAMED --add-opens=java.base/java.lang.reflect=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.security=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.management/javax.management=ALL-UNNAMED --add-opens=java.naming/javax.naming=ALL-UNNAMED

=========================================================================

10:08:54,209 INFO  [org.jboss.modules] (main) JBoss Modules version 2.0.0.Final
10:08:54,576 INFO  [org.jboss.msc] (main) JBoss MSC version 1.4.13.Final
10:08:54,584 INFO  [org.jboss.threads] (main) JBoss Threads version 2.4.0.Final
10:08:54,711 INFO  [org.jboss.as] (MSC service thread 1-2) WFLYSRV0049: WildFly Full 26.0.1.Final (WildFly Core 18.0.4.Final) starting
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.wildfly.extension.elytron.SSLDefinitions (jar:file:/opt/jboss/wildfly/modules/system/layers/base/org/wildfly/extension/elytron/main/wildfly-elytron-integration-18.0.4.Final.jar!/) to method com.sun.net.ssl.internal.ssl.Provider.isFIPS()
WARNING: Please consider reporting this to the maintainers of org.wildfly.extension.elytron.SSLDefinitions
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future rel[.gitignore](.gitignore)ease
10:08:55,484 INFO  [org.wildfly.security] (ServerService Thread Pool -- 27) ELY00001: WildFly Elytron version 1.18.3.Final
10:08:56,052 INFO  [org.jboss.as.repository] (ServerService Thread Pool -- 2) WFLYDR0001: Content added at location /opt/jboss/wildfly/standalone/data/content/47/9d6ceb6ebe7b2e5dcf8c36e0b177813526181c/content
10:08:56,137 INFO  [org.jboss.as.server] (Controller Boot Thread) WFLYSRV0039: Creating http management service using socket-binding (management-http)
10:08:56,155 INFO  [org.xnio] (MSC service thread 1-3) XNIO version 3.8.5.Final
10:08:56,165 INFO  [org.xnio.nio] (MSC service thread 1-3) XNIO NIO Implementation Version 3.8.5.Final
10:08:56,226 INFO  [org.wildfly.extension.health] (ServerService Thread Pool -- 53) WFLYHEALTH0001: Activating Base Health Subsystem
10:08:56,228 INFO  [org.wildfly.extension.elytron.oidc._private] (ServerService Thread Pool -- 52) WFLYOIDC0001: Activating WildFly Elytron OIDC Subsystem
10:08:56,233 INFO  [org.jboss.as.clustering.infinispan] (ServerService Thread Pool -- 54) WFLYCLINF0001: Activating Infinispan subsystem.
10:08:56,235 INFO  [org.jboss.as.jaxrs] (ServerService Thread Pool -- 56) WFLYRS0016: RESTEasy version 4.7.4.Final
10:08:56,246 INFO  [org.wildfly.extension.microprofile.jwt.smallrye] (ServerService Thread Pool -- 65) WFLYJWT0001: Activating MicroProfile JWT Subsystem
10:08:56,266 INFO  [org.jboss.remoting] (MSC service thread 1-8) JBoss Remoting version 5.0.23.Final
10:08:56,266 INFO  [org.wildfly.extension.microprofile.opentracing] (ServerService Thread Pool -- 66) WFLYTRACEXT0001: Activating MicroProfile OpenTracing Subsystem
10:08:56,271 INFO  [org.jboss.as.connector.subsystems.datasources] (ServerService Thread Pool -- 44) WFLYJCA0004: Deploying JDBC-compliant driver class org.h2.Driver (version 1.4)
10:08:56,288 WARN  [org.jboss.as.txn] (ServerService Thread Pool -- 74) WFLYTX0013: The node-identifier attribute on the /subsystem=transactions is set to the default value. This is a danger for environments running multiple servers. Please make sure the attribute value is unique.
10:08:56,290 INFO  [org.wildfly.extension.io] (ServerService Thread Pool -- 55) WFLYIO001: Worker 'default' has auto-configured to 16 IO threads with 128 max task threads based on your 8 available processors
10:08:56,297 INFO  [org.wildfly.extension.microprofile.config.smallrye] (ServerService Thread Pool -- 64) WFLYCONF0001: Activating MicroProfile Config Subsystem
10:08:56,307 INFO  [org.jboss.as.connector] (MSC service thread 1-2) WFLYJCA0009: Starting Jakarta Connectors Subsystem (WildFly/IronJacamar 1.5.3.Final)
10:08:56,307 INFO  [org.jboss.as.webservices] (ServerService Thread Pool -- 76) WFLYWS0002: Activating WebServices Extension
10:08:56,330 INFO  [org.wildfly.extension.metrics] (ServerService Thread Pool -- 63) WFLYMETRICS0001: Activating Base Metrics Subsystem
10:08:56,337 INFO  [org.jboss.as.naming] (ServerService Thread Pool -- 67) WFLYNAM0001: Activating Naming Subsystem
10:08:56,326 INFO  [org.jboss.as.jsf] (ServerService Thread Pool -- 61) WFLYJSF0007: Activated the following Jakarta Server Faces Implementations: [main]
10:08:56,328 INFO  [org.jboss.as.connector.deployers.jdbc] (MSC service thread 1-5) WFLYJCA0018: Started Driver service with driver-name = h2
10:08:56,431 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-7) WFLYUT0003: Undertow 2.2.14.Final starting
10:08:56,504 WARN  [org.wildfly.extension.elytron] (MSC service thread 1-1) WFLYELY00023: KeyStore file '/opt/jboss/wildfly/standalone/configuration/application.keystore' does not exist. Used blank.
10:08:56,512 INFO  [org.jboss.as.naming] (MSC service thread 1-8) WFLYNAM0003: Starting Naming Service
10:08:56,516 INFO  [org.jboss.as.mail.extension] (MSC service thread 1-4) WFLYMAIL0001: Bound mail session [java:jboss/mail/Default]
10:08:56,541 WARN  [org.wildfly.extension.elytron] (MSC service thread 1-3) WFLYELY01084: KeyStore /opt/jboss/wildfly/standalone/configuration/application.keystore not found, it will be auto generated on first use with a self-signed certificate for host localhost
10:08:56,612 INFO  [org.jboss.as.ejb3] (MSC service thread 1-2) WFLYEJB0482: Strict pool mdb-strict-max-pool is using a max instance size of 32 (per class), which is derived from the number of CPUs on this host.
10:08:56,614 INFO  [org.jboss.as.ejb3] (MSC service thread 1-8) WFLYEJB0481: Strict pool slsb-strict-max-pool is using a max instance size of 128 (per class), which is derived from thread worker pool sizing.
10:08:56,625 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 75) WFLYUT0014: Creating file handler for path '/opt/jboss/wildfly/welcome-content' with options [directory-listing: 'false', follow-symlink: 'false', case-sensitive: 'true', safe-symlink-paths: '[]']
10:08:56,673 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-5) WFLYUT0012: Started server default-server.
10:08:56,677 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-5) Queuing requests.
10:08:56,682 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-5) WFLYUT0018: Host default-host starting
10:08:56,759 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-6) WFLYUT0006: Undertow HTTP listener default listening on 0.0.0.0:8080
10:08:56,879 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-4) WFLYUT0006: Undertow HTTPS listener https listening on 0.0.0.0:8443
10:08:56,945 INFO  [org.jboss.as.ejb3] (MSC service thread 1-3) WFLYEJB0493: Jakarta Enterprise Beans subsystem suspension complete
10:08:57,000 INFO  [org.jboss.as.connector.subsystems.datasources] (MSC service thread 1-2) WFLYJCA0001: Bound data source [java:jboss/datasources/ExampleDS]
10:08:57,084 INFO  [org.jboss.as.patching] (MSC service thread 1-4) WFLYPAT0050: WildFly Full cumulative patch ID is: base, one-off patches include: none
10:08:57,091 INFO  [org.jboss.as.server.deployment.scanner] (MSC service thread 1-2) WFLYDS0013: Started FileSystemDeploymentService for directory /opt/jboss/wildfly/standalone/deployments
10:08:57,121 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-5) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:08:57,208 INFO  [org.jboss.ws.common.management] (MSC service thread 1-1) JBWS022052: Starting JBossWS 5.4.4.Final (Apache CXF 3.4.5)
10:08:57,950 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000128: Infinispan version: Infinispan 'Taedonggang' 12.1.7.Final
10:08:58,018 INFO  [org.infinispan.CONFIG] (MSC service thread 1-5) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
10:08:58,022 INFO  [org.infinispan.CONFIG] (MSC service thread 1-5) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
10:08:58,078 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000556: Starting user marshaller 'org.wildfly.clustering.infinispan.spi.marshalling.InfinispanProtoStreamMarshaller'
10:08:58,185 INFO  [org.infinispan.CONTAINER] (ServerService Thread Pool -- 78) ISPN000025: wakeUpInterval is <= 0, not starting expired purge thread
10:08:58,215 INFO  [org.jboss.as.clustering.infinispan] (ServerService Thread Pool -- 78) WFLYCLINF0002: Started http-remoting-connector cache from ejb container
10:08:58,321 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:08:58,384 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 45) WFLYSRV0010: Deployed "hello-world.war" (runtime-name : "hello-world.war")
10:08:58,433 INFO  [org.jboss.as.server] (Controller Boot Thread) WFLYSRV0212: Resuming server
10:08:58,439 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0025: WildFly Full 26.0.1.Final (WildFly Core 18.0.4.Final) started in 4560ms - Started 399 of 601 services (341 services are lazy, passive or on-demand)
10:08:58,444 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0060: Http management interface listening on http://127.0.0.1:9990/management
10:08:58,445 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0051: Admin console listening on http://127.0.0.1:9990

10:08:58,453 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0022: Unregistered web context: '/hello-world' from server 'default-server'
10:08:58,488 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-1) WFLYSRV0028: Stopped deployment hello-world.war (runtime-name: hello-world.war) in 46ms
10:08:58,494 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-6) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:08:58,657 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:08:58,720 INFO  [org.jboss.as.server] (DeploymentScanner-threads - 1) WFLYSRV0013: Redeployed "hello-world.war"

10:09:03,751 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 2) WFLYUT0022: Unregistered web context: '/hello-world' from server 'default-server'
10:09:03,778 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-3) WFLYSRV0028: Stopped deployment hello-world.war (runtime-name: hello-world.war) in 29ms
10:09:03,780 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-2) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:09:03,904 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 2) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:09:03,917 INFO  [org.jboss.as.server] (DeploymentScanner-threads - 1) WFLYSRV0016: Replaced deployment "hello-world.war" with deployment "hello-world.war"

10:09:08,936 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0022: Unregistered web context: '/hello-world' from server 'default-server'
10:09:08,965 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-6) WFLYSRV0028: Stopped deployment hello-world.war (runtime-name: hello-world.war) in 31ms
10:09:08,968 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-5) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:09:09,118 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 2) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:09:09,142 INFO  [org.jboss.as.server] (DeploymentScanner-threads - 1) WFLYSRV0013: Redeployed "hello-world.war"

10:09:14,160 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0022: Unregistered web context: '/hello-world' from server 'default-server'
10:09:14,193 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-1) WFLYSRV0028: Stopped deployment hello-world.war (runtime-name: hello-world.war) in 35ms
10:09:14,196 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-2) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:09:14,361 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:09:14,395 INFO  [org.jboss.as.server] (DeploymentScanner-threads - 1) WFLYSRV0016: Replaced deployment "hello-world.war" with deployment "hello-world.war"

10:09:19,412 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 2) WFLYUT0022: Unregistered web context: '/hello-world' from server 'default-server'
10:09:19,441 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-4) WFLYSRV0028: Stopped deployment hello-world.war (runtime-name: hello-world.war) in 31ms
10:09:19,444 INFO  [org.jboss.as.server.deployment] (MSC service thread 1-4) WFLYSRV0027: Starting deployment of "hello-world.war" (runtime-name: "hello-world.war")
10:09:19,547 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 79) WFLYUT0021: Registered web context: '/hello-world' for server 'default-server'
10:09:19,565 INFO  [org.jboss.as.server] (DeploymentScanner-threads - 1) WFLYSRV0013: Redeployed "hello-world.war"
...
```
