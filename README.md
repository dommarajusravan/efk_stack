# Monitoring Tools

Repository comtains list of SRE tools that will be configured on openshift cluster. All these tools will be stood-up on the specific SRE cluster.

1) Prometheus
2) Grafana
3) efk-stack

## Namespace

Every SRE tools will be brought up under namespace called ```sre-monitoring``` which could be updated in the future.

## Installation

To stand up any tools on this repository should be fairly very simple. There are 2 ways you can perform the installation.

#### 1.  Complete installation
If you want to bring up every tool on this repository just use  below command on root of the repo:

``` $ sre-monitoring-tools: ./installer```

#### 2.  Specific installation
If you want to specifically bring up any tool listed above just use below command on the specific tool folder of the repo. Eg: for prometheus

``` $ sre-monitoring-tools/prometheus: ./installer```

## Uninstall

Uninstall is straight forward as install and also allows two ways :

#### 1.  Complete uninstallaton
If you need to wipe-out all the SRE tools just use the below command and it will remove the namespace and other objects created.:

``` $ sre-monitoring-tools: ./uninstaller```

#### 2.  Specific installation
If you want to specifically remove the tool use below command on the specific tool folder inside the repo. Eg: for prometheus

``` $ sre-monitoring-tools/prometheus: ./uninstaller```

## Dashboards

TBD