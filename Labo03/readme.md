# Labo03 - Run a first container

## Pedagogical intent

In this lab, you'll:

* Get to grips with the first Docker commands,
* Run your first Docker
* Familiarize yourself with port publishing

---

Note: the docker engine must be running

## Task 01 - Get to grips with the first Docker commands

* List all images present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
sail-8.2/app         latest    f297a81d8c7e   2 months ago    978MB
mysql/mysql-server   8.0       1d9c2219ff69   16 months ago   496MB
```

* Get the official Nginx image using this command

[INPUT]
```bash
docker pull nginx
```

[OUTPUT]
```
Using default tag: latest
latest: Pulling from library/nginx
09f376ebb190: Pull complete 
a11fc495bafd: Pull complete 
933cc8470577: Pull complete 
999643392fb7: Pull complete 
971bb7f4fb12: Pull complete 
45337c09cd57: Pull complete 
de3b062c0af7: Pull complete 
Digest: sha256:a484819eb60211f5299034ac80f6a681b06f89e65866ce91f356ed7c72af059c
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

Note : do you see the different layer uploaded ?

TODO  : recherche les layers, 


* List -again- all image present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
nginx                latest    e784f4560448   12 days ago     188MB
sail-8.2/app         latest    f297a81d8c7e   2 months ago    978MB
mysql/mysql-server   8.0       1d9c2219ff69   16 months ago   496MB

```

Note : 188 MB is the size of your image... check it.

```bash
docker inspect --size nginx
WARNING: --size ignored for image
[
    {
        "Id": "sha256:e784f4560448b14a66f55c26e1b4dad2c2877cc73d001b7cd0b18e24a700a070",
        "RepoTags": [
            "nginx:latest"
        ],
        "RepoDigests": [
            "nginx@sha256:a484819eb60211f5299034ac80f6a681b06f89e65866ce91f356ed7c72af059c"
        ],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2024-05-03T19:49:21Z",
        "Container": "",
        "ContainerConfig": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": null,
            "Cmd": null,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.25.5",
                "NJS_VERSION=0.8.4",
                "NJS_RELEASE=3~bookworm",
                "PKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "ArgsEscaped": true,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 187659947,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/7bbfc95cbded45833817f1cb677f3d6c58a24b28109e1c4a851a659d0693d7cc/diff:/var/lib/docker/overlay2/7569d69a51b9a31316b0dceb8d38fdeaade1b856cb08ffa4dcfebf607beb3fe3/diff:/var/lib/docker/overlay2/41ad05a83c1c80b9936582b76e6f9a40323fa390be09ca72efdde2989c95c382/diff:/var/lib/docker/overlay2/392b9055e871a159777149cef3f9c73b82a6e6804f1d05163b304b9b3586c56a/diff:/var/lib/docker/overlay2/afb2dc1416f428e0099504b2c8c55b35dd39fdd4e239fd3b892ff40a0b3bafe3/diff:/var/lib/docker/overlay2/fc4ed918910dd5b013c920ff6d8617dac3caee04a026c0d4f879be7b19be5106/diff",
                "MergedDir": "/var/lib/docker/overlay2/f4445c0641d7586b111d2ab34f087bfc21db260139a89e205b88a443ceb17b7b/merged",
                "UpperDir": "/var/lib/docker/overlay2/f4445c0641d7586b111d2ab34f087bfc21db260139a89e205b88a443ceb17b7b/diff",
                "WorkDir": "/var/lib/docker/overlay2/f4445c0641d7586b111d2ab34f087bfc21db260139a89e205b88a443ceb17b7b/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:5d4427064ecc46e3c2add169e9b5eafc7ed2be7861081ec925938ab628ac0e25",
                "sha256:fc1cf9ca5139883943cc519cc3c57f0855395618f56d6431490fa735461156f1",
                "sha256:747b290aeba888738176dcbf7382eb0f660f27e785b839592918b8ed291d5792",
                "sha256:9f4d73e635f122031c04047f0e87fb224bef098a28700439bb4e72d0619aaad6",
                "sha256:56f8fe6aedcdee31bdee17249b1e18434ce7ab5a1814e2193773b54d7f9db39a",
                "sha256:7d2fd59c368c60f74214fc47399dcc35ef8513e26890a0c6004835bceabeb4c6",
                "sha256:14773070094ddc0debcea4f38f0daa7dd8116858387e0c238fa96ae8047bc07e"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```
Size in byte :  "Size": 187659947

* List -again- all image present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
nginx                latest    e784f4560448   12 days ago     188MB
sail-8.2/app         latest    f297a81d8c7e   2 months ago    978MB
mysql/mysql-server   8.0       1d9c2219ff69   16 months ago   496MB
```

* List all Docker

[INPUT]
```
docker ps -a
```

[OUTPUT]
```
CONTAINER ID   IMAGE                    COMMAND                  CREATED       STATUS                        PORTS                                                    NAMES
17319e1b4720   sail-8.2/app             "start-container"        3 weeks ago   Exited (255) 24 minutes ago   0.0.0.0:5173->5173/tcp, 8000/tcp, 0.0.0.0:8080->80/tcp   matuxor-laravel.test-1
a2e978007b6f   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   3 weeks ago   Exited (255) 24 minutes ago   33060-33061/tcp, 0.0.0.0:3307->3306/tcp                  matuxor-mysql-1
```

## Task 02 - Run the container

* Run Nginx Docker

[INPUT]
```
docker run nginx
```

[OUTPUT]
```
 docker run nginx 
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/05/16 09:59:22 [notice] 1#1: using the "epoll" event method
2024/05/16 09:59:22 [notice] 1#1: nginx/1.25.5
2024/05/16 09:59:22 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/05/16 09:59:22 [notice] 1#1: OS: Linux 6.6.16-linuxkit
2024/05/16 09:59:22 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/05/16 09:59:22 [notice] 1#1: start worker processes
2024/05/16 09:59:22 [notice] 1#1: start worker process 29
2024/05/16 09:59:22 [notice] 1#1: start worker process 30
2024/05/16 09:59:22 [notice] 1#1: start worker process 31
2024/05/16 09:59:22 [notice] 1#1: start worker process 32
2024/05/16 09:59:22 [notice] 1#1: start worker process 33
2024/05/16 09:59:22 [notice] 1#1: start worker process 34
2024/05/16 09:59:22 [notice] 1#1: start worker process 35
```

TODO :  que fait-il ?

* Can you reach the default page of nginx

Note : By default, Nginx is listening on port 80

[INPUT]
```
curl localhost
```

[OUTPUT]
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <!--
    Modified from the Debian original for Ubuntu
    Last updated: 2022-03-22
    See: https://launchpad.net/bugs/1966004
  -->
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Apache2 Ubuntu Default Page: It works</title>
    <style type="text/css" media="screen">
  * {
    margin: 0px 0px 0px 0px;
    padding: 0px 0px 0px 0px;
  }

  body, html {
    padding: 3px 3px 3px 3px;

    background-color: #D8DBE2;

    font-family: Ubuntu, Verdana, sans-serif;
    font-size: 11pt;
    text-align: center;
  }

  div.main_page {
    position: relative;
    display: table;

    width: 800px;

    margin-bottom: 3px;
    margin-left: auto;
    margin-right: auto;
    padding: 0px 0px 0px 0px;

    border-width: 2px;
    border-color: #212738;
    border-style: solid;

    background-color: #FFFFFF;

    text-align: center;
  }

  div.page_header {
    height: 180px;
    width: 100%;

    background-color: #F5F6F7;
  }

  div.page_header span {
    margin: 15px 0px 0px 50px;

    font-size: 180%;
    font-weight: bold;
  }

  div.page_header img {
    margin: 3px 0px 0px 40px;

    border: 0px 0px 0px;
  }

  div.banner {
    padding: 9px 6px 9px 6px;
    background-color: #E9510E;
    color: #FFFFFF;
    font-weight: bold;
    font-size: 112%;
    text-align: center;
    position: absolute;
    left: 40%;
    bottom: 30px;
    width: 20%;
  }

  div.table_of_contents {
    clear: left;

    min-width: 200px;

    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.table_of_contents_item {
    clear: left;

    width: 100%;

    margin: 4px 0px 0px 0px;

    background-color: #FFFFFF;

    color: #000000;
    text-align: left;
  }

  div.table_of_contents_item a {
    margin: 6px 0px 0px 6px;
  }

  div.content_section {
    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.content_section_text {
    padding: 4px 8px 4px 8px;

    color: #000000;
    font-size: 100%;
  }

  div.content_section_text pre {
    margin: 8px 0px 8px 0px;
    padding: 8px 8px 8px 8px;

    border-width: 1px;
    border-style: dotted;
    border-color: #000000;

    background-color: #F5F6F7;

    font-style: italic;
  }

  div.content_section_text p {
    margin-bottom: 6px;
  }

  div.content_section_text ul, div.content_section_text li {
    padding: 4px 8px 4px 16px;
  }

  div.section_header {
    padding: 3px 6px 3px 6px;

    background-color: #8E9CB2;

    color: #FFFFFF;
    font-weight: bold;
    font-size: 112%;
    text-align: center;
  }

  div.section_header_grey {
    background-color: #9F9386;
  }

  .floating_element {
    position: relative;
    float: left;
  }

  div.table_of_contents_item a,
  div.content_section_text a {
    text-decoration: none;
    font-weight: bold;
  }

  div.table_of_contents_item a:link,
  div.table_of_contents_item a:visited,
  div.table_of_contents_item a:active {
    color: #000000;
  }

  div.table_of_contents_item a:hover {
    background-color: #000000;

    color: #FFFFFF;
  }

  div.content_section_text a:link,
  div.content_section_text a:visited,
   div.content_section_text a:active {
    background-color: #DCDFE6;

    color: #000000;
  }

  div.content_section_text a:hover {
    background-color: #000000;

    color: #DCDFE6;
  }

  div.validator {
  }
    </style>
  </head>
  <body>
    <div class="main_page">
      <div class="page_header floating_element">
        <img src="icons/ubuntu-logo.png" alt="Ubuntu Logo"
             style="width:184px;height:146px;" class="floating_element" />
        <div>
          <span style="margin-top: 1.5em;" class="floating_element">
            Apache2 Default Page
          </span>
        </div>
        <div class="banner">
          <div id="about"></div>
          It works!
        </div>

      </div>
      <div class="content_section floating_element">
        <div class="content_section_text">
          <p>
                This is the default welcome page used to test the correct 
                operation of the Apache2 server after installation on Ubuntu systems.
                It is based on the equivalent page on Debian, from which the Ubuntu Apache
                packaging is derived.
                If you can read this page, it means that the Apache HTTP server installed at
                this site is working properly. You should <b>replace this file</b> (located at
                <tt>/var/www/html/index.html</tt>) before continuing to operate your HTTP server.
          </p>

          <p>
                If you are a normal user of this web site and don't know what this page is
                about, this probably means that the site is currently unavailable due to
                maintenance.
                If the problem persists, please contact the site's administrator.
          </p>

        </div>
        <div class="section_header">
          <div id="changes"></div>
                Configuration Overview
        </div>
        <div class="content_section_text">
          <p>
                Ubuntu's Apache2 default configuration is different from the
                upstream default configuration, and split into several files optimized for
                interaction with Ubuntu tools. The configuration system is
                <b>fully documented in
                /usr/share/doc/apache2/README.Debian.gz</b>. Refer to this for the full
                documentation. Documentation for the web server itself can be
                found by accessing the <a href="/manual">manual</a> if the <tt>apache2-doc</tt>
                package was installed on this server.
          </p>
          <p>
                The configuration layout for an Apache2 web server installation on Ubuntu systems is as follows:
          </p>
          <pre>
/etc/apache2/
|-- apache2.conf
|       `--  ports.conf
|-- mods-enabled
|       |-- *.load
|       `-- *.conf
|-- conf-enabled
|       `-- *.conf
|-- sites-enabled
|       `-- *.conf
          </pre>
          <ul>
                        <li>
                           <tt>apache2.conf</tt> is the main configuration
                           file. It puts the pieces together by including all remaining configuration
                           files when starting up the web server.
                        </li>

                        <li>
                           <tt>ports.conf</tt> is always included from the
                           main configuration file. It is used to determine the listening ports for
                           incoming connections, and this file can be customized anytime.
                        </li>

                        <li>
                           Configuration files in the <tt>mods-enabled/</tt>,
                           <tt>conf-enabled/</tt> and <tt>sites-enabled/</tt> directories contain
                           particular configuration snippets which manage modules, global configuration
                           fragments, or virtual host configurations, respectively.
                        </li>

                        <li>
                           They are activated by symlinking available
                           configuration files from their respective
                           *-available/ counterparts. These should be managed
                           by using our helpers
                           <tt>
                                a2enmod,
                                a2dismod,
                           </tt>
                           <tt>
                                a2ensite,
                                a2dissite,
                            </tt>
                                and
                           <tt>
                                a2enconf,
                                a2disconf
                           </tt>. See their respective man pages for detailed information.
                        </li>

                        <li>
                           The binary is called apache2 and is managed using systemd, so to
                           start/stop the service use <tt>systemctl start apache2</tt> and
                           <tt>systemctl stop apache2</tt>, and use <tt>systemctl status apache2</tt>
                           and <tt>journalctl -u apache2</tt> to check status.  <tt>system</tt>
                           and <tt>apache2ctl</tt> can also be used for service management if
                           desired.
                           <b>Calling <tt>/usr/bin/apache2</tt> directly will not work</b> with the
                           default configuration.
                        </li>
          </ul>
        </div>

        <div class="section_header">
            <div id="docroot"></div>
                Document Roots
        </div>

        <div class="content_section_text">
            <p>
                By default, Ubuntu does not allow access through the web browser to
                <em>any</em> file outside of those located in <tt>/var/www</tt>,
                <a href="http://httpd.apache.org/docs/2.4/mod/mod_userdir.html" rel="nofollow">public_html</a>
                directories (when enabled) and <tt>/usr/share</tt> (for web
                applications). If your site is using a web document root
                located elsewhere (such as in <tt>/srv</tt>) you may need to whitelist your
                document root directory in <tt>/etc/apache2/apache2.conf</tt>.
            </p>
            <p>
                The default Ubuntu document root is <tt>/var/www/html</tt>. You
                can make your own virtual hosts under /var/www.
            </p>
        </div>

        <div class="section_header">
          <div id="bugs"></div>
                Reporting Problems
        </div>
        <div class="content_section_text">
          <p>
                Please use the <tt>ubuntu-bug</tt> tool to report bugs in the
                Apache2 package with Ubuntu. However, check <a
                href="https://bugs.launchpad.net/ubuntu/+source/apache2"
                rel="nofollow">existing bug reports</a> before reporting a new bug.
          </p>
          <p>
                Please report bugs specific to modules (such as PHP and others)
                to their respective packages, not to the web server itself.
          </p>
        </div>

      </div>
    </div>
    <div class="validator">
    </div>
  </body>
</html>
```

* Stop this first attempt

[INPUT]
```
docker stop <id>
```

[OUTPUT]
```
//TODO
```

## Task 03 - Familiarize yourself with port publishing

* Make it possible to reach nginx with this command

[Publish a port](https://docs.docker.com/network/#published-ports)

[INPUT]
```
curl localhost:8080
```

[OUTPUT]
```
//TODO
```

* Stop and delete the container

[INPUT]
```
//TODO delete the container
```

[OUTPUT]
```
//TODO
```

* Delete the image

[INPUT]
```
//TODO delete the image
```

[OUTPUT]
```
//TODO
```
