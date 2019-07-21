SOURCE: https://kifarunix.com/how-to-install-nagios-plugins-and-nrpe-agents-on-centos-7-rhel-7-fedora-29/

Step 1: Install the icinga repo and then icinga using:
<p>
yum install https://packages.icinga.com/epel/icinga-rpm-release-7-latest.noarch.rpm -y
yum install icinga2 -y
systemctl enable icinga2
systemctl start icinga2
yum install epel-release -y
yum install nrpe -y
yum install nagios-plugins-all.x86_64

 </p>

Step 2: Get hostname of machine using hostname command.

Step 3: Login to the icinga server and using this hostname, generate token from icinga server:
<br>icinga2 pki ticket --cn <Specify the machine hostname here>

Step 4: Now on the linux node, do the following steps as it is, changing the hostname to its actual name of course:

<p>[root@prometheusdb yum.repos.d]# icinga2 node wizard
Welcome to the Icinga 2 Setup Wizard!

We will guide you through all required configuration details.

Please specify if this is a satellite/client setup ('n' installs a master setup) [Y/n]: y

Starting the Client/Satellite setup routine...
Please specify the common name (CN) [prometheusdb]: <Specify the machine hostname here>

Please specify the parent endpoint(s) (master or satellite) where this node should connect to:
Master/Satellite Common Name (CN from your master/satellite node): icinga2

Do you want to establish a connection to the parent node from this node? [Y/n]: y
Please specify the master/satellite connection information:
Master/Satellite endpoint host (IP address or FQDN): 172.16.0.23
Master/Satellite endpoint port [5665]:

Add more master/satellite endpoints? [y/N]: n
Parent certificate information:

 Subject:     CN = icinga2
 Issuer:      CN = Icinga CA
 Valid From:  Jun 15 10:01:06 2019 GMT
 Valid Until: Jun 11 10:01:06 2034 GMT
 Fingerprint: 78 B8 A3 5F 3C 38 3B F3 ED 3F 48 C1 01 77 A2 24 70 5A 0C F4

Is this information correct? [y/N]: y

Please specify the request ticket generated on your Icinga 2 master (optional).
 (Hint: # icinga2 pki ticket --cn 'prometheusdb'): <Paste the token that you generated from the icinga server in step 3>
Please specify the API bind host/port (optional):
Bind Host []:
Bind Port []:

Accept config from parent node? [y/N]: y
Accept commands from parent node? [y/N]: y

Reconfiguring Icinga...
Disabling feature notification. Make sure to restart Icinga 2 for these changes to take effect.
Enabling feature api. Make sure to restart Icinga 2 for these changes to take effect.

Local zone name [prometheusdb]: <Press enter here>
Parent zone name [master]: <Press enter here>

Default global zones: global-templates director-global
Do you want to specify additional global zones? [y/N]: n

Do you want to disable the inclusion of the conf.d directory [Y/n]: y
Disabling the inclusion of the conf.d directory...

Done.

Now restart your Icinga 2 daemon to finish the installation!
</p>

Step 5: Now restart icinga service:
[root@prometheusdb yum.repos.d]# systemctl restart icinga2

Step 6: Now install the nscp plugins on the node: [Check this error](errors/nscp.md)
<br>yum install https://github.com/mickem/nscp/releases/download/0.4.3.143/NSCP-0.4.3.143-1.el7.x86_64.rpm  -y

Step 7: now login to the icinga server and make the following files step by step.
Change the value prometheusdb to the actual hostname of the machine on which you are configuring icinga:
Make the following files on the icinga server:
1. /etc/icinga2/conf.d/hostgroups/prom.conf

object HostGroup "prometheus" {
  display_name = "prometheus"

  assign where match("*.prometheus.*", host.notes)

}

<br>Replace ${1} with the hostname and ${2} with the IP:
<br>Ex:
<br>object Endpoint "${1}" {
<br>  host = "${2}"
<br>}
<br>
<br>becomes:
<br>
<br>object Endpoint "TomcatNode1" {
<br>  host = "172.16.0.90"
<br>}
2. /etc/icinga2/conf.d/services/prom.conf

apply Service "procs-${1}" {
  import "generic-service"
  check_command = "procs"
  command_endpoint =  "${1}"
  assign where "${1}" in host.groups
}

apply Service "users-${1}" {
  import "generic-service"
  check_command = "users"
  command_endpoint =  "${1}"
  assign where "${1}" in host.groups
}

apply Service "swap-${1}" {
  import "generic-service"
  check_command = "swap"
  command_endpoint =  "${1}"
  assign where "${1}" in host.groups
}

apply Service "disk-${1}" {
  import "generic-service"
  check_command = "disk"
  command_endpoint =  "${1}"
  assign where "${1}" in host.groups
}

apply Service "load-{$1}" {
  import "generic-service"
  check_command = "load"
  command_endpoint =  "${1}"
  assign where "${1}" in host.groups
}
memory: [Check this error](errors/memory.md)
object Endpoint "${1}" {
  host = "${2}"
}

object Zone "${1}" {
  endpoints = [ "${1}" ]
  parent = "master"
}


3. /etc/icinga2/conf.d/hosts/prom.conf

object Host "prometheus" {
    import "generic-host"
        vars.os="Linux"
address = "172.16.0.189"
    notes = "group:.prometheus.:end"

}

Step8: After that restart icinga server process using: systemctl restart icinga2

The node and the related services should show up on the gui now: http://172.16.0.23/icingaweb2/monitoring/list/hosts
