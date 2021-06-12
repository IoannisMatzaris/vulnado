# Vulnado - Intentionally Vulnerable Java Application

This application and exercises will take you through some of the OWASP top 10 Vulnerabilities and how to prevent them.

## Up and running

1. Install Docker for [MacOS](https://hub.docker.com/editions/community/docker-ce-desktop-mac) or [Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows). You'll need to create a Docker account if you don't already have one.
2. `git clone git://github.com/ScaleSec/vulnado`
3. `cd vulnado`
4. `docker-compose up`
5. Open a browser and navigate to the client to make sure it's working: [http://localhost:1337](http://localhost:1337)
6. Then back in your terminal verify you have connection to your API server: `nc -vz localhost 8081`

## Architecture

The docker network created by `docker-compose` maps pretty well to a multi-tier architecture where a web server is publicly available and there are other network resources like a database and internal site that are not publicly available.

![](exercises/assets/arch.png)

## Exercises

* [SQL Injection](exercises/01-sql-injection.md)
* [XSS - Cross Site Scripting](exercises/02-xss.md)
* [SSRF - Server Side Request Forgery](exercises/03-ssrf.md)
* [RCE - Remote Code Execution & Reverse Shell](exercises/04-rce-reverse-shell.md)

## Remote Debugging - jdb
In case you would like to try some remote debugging with jdb, you may
1. `docker-compose up --build -d`
2. `docker cp vulnado_vulnado_1:/vulnado-0.0.1-SNAPSHOT.jar .`
3. Use JD-GUI [https://github.com/java-decompiler/jd-gui] to decompile the jar
4. Change the file structure, so that the remote debugging can be successfully done
5. `jdb -sourcepath ./ -connect com.sun.jdi.SocketAttach:hostname=localhost,port=5005`
6. Set breakpoints using jdb `stop in com.scalesec.vulnado.LoginController:20`