<p>
SOURCE: https://stackoverflow.com/questions/37941475/icinga2-check-mem-plugin-doesnt-accept-parameters

service
apply Service "Memory" {
  import "generic-service"
  check_command = "memory"
  assign where host.address
}
However the plugin cannot check the memory and gives the following output in Icinga Web 2 interface:

​Plugin Output
*** You must define WARN and CRITICAL levels! \ncheck_​mem.​pl v1.​0 - Nagios Plugin\n\nusage:​\n check_​mem.​pl -\ncheck_​mem.​pl comes with absolutely NO WARRANTY either implied or explicit\nThis program is licensed under the terms of the\nMIT License (check source code for details)


Give like this, you command will get values from service at run time.

apply Service "Memory" {
  import "generic-service"
  check_command = "memory"
  vars.mem_used = true
  vars.mem_cache = true
  vars.mem_warning = 85
  vars.mem_critical = 95
  assign where host.address
}
</p>
