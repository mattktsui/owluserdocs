# Standalone Upgrade

#### Manual

1. Copy the contents of the provided package e.g. owl-\<newversion>-\<SPARK301>-package-base.tar.gz to the system being upgraded (extract contents)
2. Stop owlweb using `./owlmanage.sh stop=owlweb`
3. Stop owlagent using `./owlmanage.sh stop=owlagent`
4. Move old jars from `owl/bin`
   1. `mv owl-webapp-<oldversion>-<spark301>.jar /tmp`
   2. `mv owl-agent-<oldversion>-<spark301>.jar /tmp`
   3. `mv owl-core-<oldversion>-<spark301>.jar /tmp`
5. Copy new jars into the `owl/bin` folder from the extracted package
   1. `mv owl-webapp-<newversion>-<spark301>.jar /home/owldq/owl/bin`
   2. `mv owl-agent-<newversion>-<spark301>.jar /home/owldq/owl/bin`
   3. `mv owl-core-<newversion>-<spark301>.jar /home/owldq/owl/bin`
6. run `./owlmanage.sh start=owlweb` to start the owl-web application
7. run `./owlmanage.sh start=owlagent` to start owlagent

#### Automated

Copy the below script into a file called `upgrade.sh` give it execute permissions and run it. 

Example:

```
./upgrade.sh -port=5432 -owlbase=/home/owl -owlpackage=/home/user/packagedir
```

```
#!/bin/bash

usage () {
    echo "Usage: $0 [OPTION]..."
    echo "Owl upgrade script"
    echo ""
    echo "  -owlbase=         set base path to where owl is installed"
    echo "  -owlpackage=      set owl package directory"
    echo "  -help             display this help and exit"
    echo ""
    echo ""
    echo "example:"
    echo "  ./upgrade.sh -owlbase=/home/owl -owlpackage=/home/user/packagedir"
}

start_agent() {
    if [ -f $owlagent ]; then
        if [ -f "$INSTALL_PATH/bin/owlmanage.sh" ]; then
            $INSTALL_PATH/bin/owlmanage.sh start=owlagent
        fi
    else
        __die "Cannot find $owlagent"
    fi
}

start_owlweb() {
    if [ -f $owlweb ]; then
         if [ -f "$INSTALL_PATH/bin/owlmanage.sh" ]; then
              $INSTALL_PATH/bin/owlmanage.sh start=owlweb
         fi
    else
       __die "Cannot find $owlweb"
    fi
}

stop_owlagent(){
    echo Executing stop owl-agent
    if [ -f $INSTALL_PATH/pids/owl-agent.pid ]; then
        kill -9 `cat $INSTALL_PATH/pids/owl-agent.pid`
        rm $INSTALL_PATH/pids/owl-agent.pid
    else
        echo "owl-agent not running"
    fi

}

stop_owlweb(){
    echo Executing stop owl-web
    if [ -f $INSTALL_PATH/pids/owl-web.pid ]; then
        kill -15 `cat $INSTALL_PATH/pids/owl-web.pid`
        rm $INSTALL_PATH/pids/owl-web.pid
    else
        echo "owl-web not running"
    fi

}

owl_upgrade() {

    echo "Removing old files in the $INSTALL_PATH/bin directory"
    search_dir="$INSTALL_PATH/bin"
    for entry in "$search_dir"/*
    do
        if [ -f $entry ]; then
            rm "$entry"
        fi
    done

    echo "Copying in updated files from $PACKAGE_LOCATION to $INSTALL_PATH/bin"
    cp $owlcore $INSTALL_PATH/bin
    cp $owlweb $INSTALL_PATH/bin
    cp $owlagent $INSTALL_PATH/bin
    cp $owlcat $INSTALL_PATH/bin
    cp $owlmanage $INSTALL_PATH/bin
    chmod 777 $INSTALL_PATH/bin/owlmanage.sh
    cp $owlcli $INSTALL_PATH/bin
    chmod 777 $INSTALL_PATH/bin/owlcheck
    
    sleep 15
    start_owlweb
    sleep 15
    start_agent
}

OWL_BASE=""
INSTALL_PATH="${OWL_BASE}/owl"
owlcli=""
owlcat=""
owlmanage=""
bin=`dirname "$0"`
binDir=`cd "$bin"; pwd`
PACKAGE_LOCATION=$binDir

if [[ "$@" != "" ]] ; then
    for i in "$@"
    do
       case $(echo "$1" | awk '{print tolower($0)}') in
        -owlbase=*)
            OWL_BASE=""${1#*=}""
            INSTALL_PATH="${OWL_BASE}"
            ;;
        -owlpackage=*)
            PACKAGE_LOCATION=""${1#*=}""
            ;;
        -h|--help)
            usage
            exit 0
            ;;
        *)
            usage
            exit 1
            ;;
        esac
        shift
    done
else
    echo "Please specify the current location to owl by providing the -owlbase path argument"
    usage
    exit
fi


if [ -f $PACKAGE_LOCATION/owl-core-*-with-dependencies.jar ]; then
    owlcore="$(ls $PACKAGE_LOCATION/owl-core-*-with-dependencies.jar)"
else
    echo "owl-core not found in $PACKAGE_LOCATION"
    exit
fi

if [ -f $PACKAGE_LOCATION/owl-webapp-*.jar ]; then
    owlweb="$(ls $PACKAGE_LOCATION/owl-webapp-*.jar)"
else
    echo "owl-web not found in $PACKAGE_LOCATION"
    exit
fi


if [ -f $PACKAGE_LOCATION/owl-agent-*.jar ]; then
    owlagent="$(ls $PACKAGE_LOCATION/owl-agent-*.jar)"
else
    echo "owl-agent not found in $PACKAGE_LOCATION"
    exit
fi

if [ -f $PACKAGE_LOCATION/catalog.py ]; then
    owlcat="$(ls $PACKAGE_LOCATION/catalog.py)"
else
    echo "catalog.py not found in $PACKAGE_LOCATION"
    exit
fi

if [ -f $PACKAGE_LOCATION/owlcheck ]; then
    owlcli="$(ls $PACKAGE_LOCATION/owlcheck)"
else
    echo "owlcheck not found in $PACKAGE_LOCATION"
    exit
fi

if [ -f $PACKAGE_LOCATION/owlmanage.sh ]; then
    owlmanage="$(ls $PACKAGE_LOCATION/owlmanage.sh)"
else
    echo "owlmanage.sh not found in $PACKAGE_LOCATION"
    exit
fi

echo "Preparing for owl upgrade"
stop_owlweb
stop_owlagent
echo "performing upgrade"
owl_upgrade
echo "upgrade of owl completed"


```
