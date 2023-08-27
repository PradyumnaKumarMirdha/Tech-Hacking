# Masscan

It is a stateless scanner. It bypasses the kernel to increase speed and reduce resource utilization.

- After sending one SYN packet for a particular IP it moves to another.
- Generates the SYN packet in bulk and sends it all at once. Lastly, wait to get the responses.
- Uses custom TCP/IP stack on kernel to increase speed which requires SUDO privileges.
- It can scan 2^32 address space in 5-6 minutes.

_**The difference between MasScan and NMAP is that nmap goes vertically scale ( how deep can it go in a host ), while masscan uses a horizontal scale approach.**_

```powershell
sudo masscan -p0-1023 10.0.0.0/20 --rate 15000 -v
```

**NOTE:** _Try to decrease the rate as there maybe chances of ignores ports_

`--rate` = Used for throttling ( safe zone is 15000 )


<pre>
NAME
       masscan - Fast scan of the Internet

SYNOPSIS
       masscan &lt;ip addresses/ranges&gt; -p ports options

DESCRIPTION
       masscan  is an Internet-scale port scanner, useful for large scale surveys of the Inter‐
       net, or of internal networks. While the default transmit rate is only  100  packets/sec‐
       ond,  it can optional go as fast as 25 million packets/second, a rate sufficient to scan
       the Internet in 3 minutes for one port.

OPTIONS
       •   &lt;ip/range&gt;: anything on the command-line not prefixed with a ´-´ is assumed to be an
           IP  address  or range. There are three valid formats. The first is a single IPv4 ad‐
           dress like &quot;192.168.0.1&quot;. The second is  a  range  like  &quot;10.0.0.1-10.0.0.100&quot;.  The
           third  is  a  CIDR address, like &quot;0.0.0.0/0&quot;. At least one target must be specified.
           Multiple targets can be specified. This can be specified as multiple  options  sepa‐
           rated  by  space,  or  can  be  separated  by  a  comma  as a single option, such as
           10.0.0.0/8,192.168.0.1.

       •   --range &lt;ip/range&gt;: the same as target range spec described above, except as a named
           parameter instead of an unnamed one.

       •   -p  &lt;ports,  --ports &lt;ports&gt;: specifies the port(s) to be scanned. A single port can
           be specified, like -p80. A range of ports can be specified, like -p 20-25. A list of
           ports/ranges  can  be  specified,  like -p80,20-25. UDP ports can also be specified,
           like --ports U:161,U:1024-1100.

       •   --banners: specifies that banners should be grabbed, like HTTP server versions, HTML
           title fields, and so forth. Only a few protocols are supported.

       •   --rate  &lt;packets-per-second&gt;:  specifies  the desired rate for transmitting packets.
           This can be very small numbers, like 0.1 for transmitting packets at  rates  of  one
           every  10  seconds, for very large numbers like 10000000, which attempts to transmit
           at 10 million packets/second. In my experience, Windows  and  can  do  250  thousand
           packets per second, and latest versions of Linux can do 2.5 million packets per sec‐
           ond. The PF_RING driver is needed to get to 25 million packets/second.

       •   -c &lt;filename&gt;, --conf &lt;filename&gt;: reads in a configuration file. The format  of  the
           configuration file is described below.

       •   --resume &lt;filename&gt;: the same as --conf, except that a few options are automatically
           set, such as --append-output. The format of the configuration file is described  be‐
           low.

       •   --echo:  don´t  run, but instead dump the current configuration to a file. This file
           can then be used with the -c option. The format of this output  is  described  below
           under ´CONFIGURATION FILE´.

       •   -e &lt;ifname&gt;, --adapter &lt;ifname&gt;: use the named raw network interface, such as &quot;eth0&quot;
           or &quot;dna1&quot;. If not specified, the first network interface found with a default  gate‐
           way will be used.

       •   --adapter-ip  &lt;ip-address&gt;:  send  packets  using this IP address. If not specified,
           then the first IP address bound to the network interface will be used. Instead of  a
           single  IP address, a range may be specified. NOTE: The size of the range must be an
           even power of 2, such as 1, 2, 4, 8, 16, 1024 etc. addresses.

       •   --adapter-port &lt;port&gt;: send packets using this port number as  the  source.  If  not
           specified,  a random port will be chosen in the range 40000 through 60000. This port
           should be filtered by the host firewall (like iptables) to prevent the host  network
           stack  from interfering with arriving packets. Instead of a single port, a range can
           be specified, like 40000-40003. NOTE: The size of the range must be an even power of
           2, such as the example above that has a total of 4 addresses.

       •   --adapter-mac  &lt;mac-address&gt;:  send packets using this as the source MAC address. If
           not specified, then the first MAC address bound to the  network  interface  will  be
           used.

       •   --router-mac  &lt;mac address&gt;: send packets to this MAC address as the destination. If
           not specified, then the gateway address of the network interface will be ARPed.

       •   --ping: indicates that the scan should include an ICMP echo request. This may be in‐
           cluded with TCP and UDP scanning.

       •   --exclude  &lt;ip/range&gt;:  blacklist  an  IP address or range, preventing it from being
           scanned. This  overrides  any  target  specification,  guaranteeing  that  this  ad‐
           dress/range won´t be scanned. This has the same format as the normal target specifi‐
           cation.

       •   --excludefile &lt;filename&gt;: reads in a list of exclude ranges, in the same target for‐
           mat  described  above. These ranges override any targets, preventing them from being
           scanned.

       •   --append-output: causes output to append to file, rather than overwriting the file.

       •   --iflist: list the available network interfaces, and then exits.

       •   --retries: the number of retries to send, at 1 second  intervals.  Note  that  since
           this  scanner is stateless, retries are sent regardless if replies have already been
           received.

       •   --nmap: print help about nmap-compatibility alternatives for these options.

       •   --pcap-payloads: read packets from a libpcap file containing packets and extract the
           UDP payloads, and associate those payloads with the destination port. These payloads
           will then be used when sending UDP packets with the matching destination port.  Only
           one payload will be remembered per port. Similar to --nmap-payloads.

       •   --nmap-payloads  &lt;filename&gt;:  read  in  a  file  in the same format as the nmap file
           nmap-payloads. This contains UDP payload, so that we can send useful UDP packets in‐
           stead of empty ones. Similar to --pcap-payloads.

       •   --http-user-agent  &lt;user-agent&gt;: replaces the existing user-agent field with the in‐
           dicated value when doing HTTP requests.

       •   --open-only: report only open ports, not closed ports.

       •   --pcap &lt;filename&gt;: saves received packets (but not transmitted packets) to the libp‐
           cap-format file.

       •   --packet-trace:  prints a summary of those packets sent and received. This is useful
           at low rates, like a few packets per second, but will overwhelm the terminal at high
           rates.

       •   --pfring:  force the use of the PF_RING driver. The program will exit if PF_RING DNA
           drvers are not available.

       •   --resume-index: the point in the scan at when it was paused.

       •   --resume-count: the maximum number of probes to send before exiting. This is  useful
           with  the  --resume-index  to  chop up a scan and split it among multiple instances,
           though the --shards option might be better.

       •   --shards &lt;x&gt;/&lt;y&gt;: splits the scan among instances. x is the id for this scan,  while
           y  is  the total number of instances. For example, --shards 1/2 tells an instance to
           send every other packet, starting with index 0. Likewise, --shards 2/2  sends  every
           other  packet,  but starting with index 1, so that it doesn´t overlap with the first
           example.

       •   --rotate &lt;time&gt;: rotates the output file, renaming it with  the  current  timestamp,
           moving  it to a separate directory. The time is specified in number of seconds, like
           &quot;3600&quot; for an hour. Or, units of  time  can  be  specified,  such  as  &quot;hourly&quot;,  or
           &quot;6hours&quot;, or &quot;10min&quot;. Times are aligned on an even boundary, so if &quot;daily&quot; is speci‐
           fied, then the file will be rotated every day at midnight.

       •   --rotate-offset &lt;time&gt;: an offset in the time. This is to accommodate timezones.

       •   --rotate-dir &lt;directory&gt;: when rotating the file, this specifies which directory  to
           move the file to. A useful directory is /var/log/masscan.

       •   --seed &lt;integer&gt;: an integer that seeds the random number generator. Using a differ‐
           ent seed will cause packets to be sent in a different random order.  Instead  of  an
           integer,  the  string  time can be specified, which seeds using the local timestamp,
           automatically generating a different random order of scans. If  no  seed  specified,
           time is the default.

       •   --regress: run a regression test, returns ´0´ on success and ´1´ on failure.

       •   --ttl &lt;num&gt;: specifies the TTL of outgoing packets, defaults to 255.

       •   --wait &lt;seconds&gt;: specifies the number of seconds after transmit is done to wait for
           receiving packets before exiting the program. The default is 10 seconds. The  string
           forever can be specified to never terminate.

       •   --offline:  don´t  actually  transmit  packets.  This  is useful with a low rate and
           --packet-trace to look at what packets might´ve been transmitted.  Or,  it´s  useful
           with --rate 100000000 in order to benchmark how fast transmit would work (assuming a
           zero-overhead driver). PF_RING is about 20% slower than the  benchmark  result  from
           offline mode.

       •   -sL: this doesn´t do a scan, but instead creates a list of random addresses. This is
           useful for importing into other tools.  The  options  --shard,  --resume-index,  and
           --resume-count can be useful with this feature.

       •   --interactive: show the results in realtime on the console. It has no effect if used
           with --output-format or --output-filename.

       •   --output-format &lt;fmt&gt;: indicates the format of the output file, which  can  be  xml,
           binary, grepable, list, or JSON. The option --output-filename must be specified.

       •   --output-filename  &lt;filename&gt;:  the  file which to save results to. If the parameter
           --output-format is not specified, then the default of xml will be used.

       •   -oB &lt;filename&gt;: sets the output format to binary and saves the output in  the  given
           filename.  This is equivelent to using the --output-format and --output-filename pa‐
           rameters. The option --readscan can then be used to read  the  binary  file.  Binary
           files  are  much  smaller than their XML equivelents, but require a separate step to
           convert back into XML or another readable format.

       •   -oX &lt;filename&gt;: sets the output format to XML and saves  the  output  in  the  given
           filename.  This is equivelent to using the --output-format xml and --output-filename
           parameters.

       •   -oG &lt;filename&gt;: sets the output format to grepable and saves the output in the given
           filename.  This  is  equivelent  to  using  the  --output-format grepable and --out‐
           put-filename parameters.

       •   -oJ &lt;filename&gt;: sets the output format to JSON and saves the  output  in  the  given
           filename. This is equivelent to using the --output-format json and --output-filename
           parameters.

       •   -oL &lt;filename&gt;: sets the output format to a simple list format and saves the  output
           in  the  given  filename.  This  is equivelent to using the --output-format list and
           --output-filename parameters.

       •   --readscan &lt;binary-files&gt;: reads the files created by the -oB option  from  a  scan,
           then outputs them in one of the other formats, depending on command-line parameters.
           In other words, it can take the binary version of the output and convert  it  to  an
           XML or JSON format.

CONFIGURATION FILE FORMAT
       The  configuration file uses the same parameter names as on the commandline, but without
       the -- prefix, and with an = sign between the name and the value. An example  configura‐
       tion file might be:

           # targets
           range = 10.0.0.0/8,192.168.0.0/16
           range = 172.16.0.0/14
           ports = 20-25,80,U:53
           ping = true

           # adapter
           adapter = eth0
           adapter-ip = 192.168.0.1
           router-mac = 66-55-44-33-22-11

           # other
           exclude-file = /etc/masscan/exludes.txt

       By default, the program will read default configuration from the file /etc/masscan/mass‐
       can.conf. This is useful for system-specific settings, such  as  the  --adapter-xxx  op‐
       tions.  This  is  also useful for excluded IP addresses, so that you can scan the entire
       Internet, while skipping dangerous addresses, like those owned by the DoD, and not  make
       an accidental mistake.

CONTROL-C BEHAVIOR
       When the user presses ctrl-c, the scan will stop, and the current state of the scan will
       be saved in the file ´paused.conf´. The scan can be resumed with the --resume option:

           # masscan --resume paused.conf

       The program will not exit immediately, but will wait a default of 10 seconds to  receive
       results  from the Internet and save the results before exiting completely. This time can
       be changed with the --wait option.

SIMPLE EXAMPLES
       The following example scans all private networks for webservers,  and  prints  all  open
       ports that were found.

           # masscan 10.0.0.0/8 192.168.0.0/16 172.16.0.0/12 -p80 --open-only

       The  following  example  scans  the entire Internet for DNS servers, grabbing their ver‐
       sions, then saves the results in an XML file.

           # masscan 0.0.0.0/0 --excludefile no-dod.txt -pU:53 --banners --output-filename dns.xml

       You should be able to import the XML into databases and such.

       The following example reads a binary scan results file called bin-test.scan  and  prints
       results to console.

           # masscan --readscan bin-test.scan

       The  following example reads a binary scan results file called bin-test.scan and creates
       an XML output file called bin-test.xml.

           # masscan --readscan bin-test.scan -oX bin-test.xml

ADVANCED EXAMPLES
       Let´s say that you want to scan the entire Internet and spread the scan across three ma‐
       chines.  Masscan  would  be  launched  on  all  three  machines using the following com‐
       mand-lines:

           # masscan 0.0.0.0/0 -p0-65535 --shard 1/3
           # masscan 0.0.0.0/0 -p0-65535 --shard 2/3
           # masscan 0.0.0.0/0 -p0-65535 --shard 3/3

       An alternative is with the &quot;resume&quot; feature. A scan has an internal index that goes from
       zero  to  the  number  of ports times then number of IP addresses. The following example
       shows splitting up a scan into chunks of a 1000 items each:

           # masscan 0.0.0.0/0 -p0-65535 --resume-index 0 --resume-count 1000
           # masscan 0.0.0.0/0 -p0-65535 --resume-index 1000 --resume-count 1000
           # masscan 0.0.0.0/0 -p0-65535 --resume-index 2000 --resume-count 1000
           # masscan 0.0.0.0/0 -p0-65535 --resume-index 3000 --resume-count 1000

       A script can use this to split smaller tasks across many other machines, such as  Amazon
       EC2  instances.  As  each instance completes a job, the script might send a request to a
       central coordinating server for more work.

SPURIOUS RESETS
       When scanning TCP using the default IP address of your adapter, the built-in stack  will
       generate RST packets. This will prevent banner grabbing. There are are two ways to solve
       this. The first way is to create a firewall rule to block that port from being  seen  by
       the  stack. How this works is dependent on the operating system, but on Linux this looks
       something like:

           # iptables -A INPUT -p tcp -i eth0 --dport 61234 -j DROP

       Then, when scanning, that same port must be used as the source:

           # masscan 10.0.0.0/8 -p80 --banners --adapter-port 61234

       An alternative is to &quot;spoof&quot; a different IP address. This IP address must be within  the
       range of the local network, but must not otherwise be in use by either your own computer
       or another computer on the network. An example of this would look like:

           # masscan 10.0.0.0/8 -p80 --banners --adapter-ip 192.168.1.101

       Setting your source IP address this way is the preferred way of running this scanner.

ABUSE COMPLAINTS
       This scanner is designed for large-scale surveys, of either an organization, or  of  the
       Internet as a whole. This scanning will be noticed by those monitoring their logs, which
       will generate complaints.

       If you are scanning your own organization, this may lead to you being fired. Never  scan
       outside  your local subnet without getting permission from your boss, with a clear writ‐
       ten declaration of why you are scanning.

       The same applies to scanning the Internet from your employer. This is another  good  way
       to  get fired, as your IT department gets flooded with complaints as to why your organi‐
       zation is hacking them.

       When scanning on your own, such as your home Internet or ISP,  this  will  likely  cause
       them to cancel your account due to the abuse complaints.

       One solution is to work with your ISP, to be clear about precisely what we are doing, to
       prove to them that we are researching the Internet, not &quot;hacking&quot; it. We  have  our  ISP
       send  the  abuse  complaints  directly  to  us. For anyone that asks, we add them to our
       &quot;--excludefile&quot;, blacklisting them so that we won´t scan them again.  While  interacting
       with  such people, some instead add us to their whitelist, so that their firewalls won´t
       log us anymore (they´ll still block us, of course, they just  won´t  log  that  fact  to
       avoid filling up their logs with our scans).

       Ultimately,  I don´t know if it´s possible to completely solve this problem. Despite the
       Internet being a public, end-to-end network, you are still &quot;guilty  until  proven  inno‐
       cent&quot; when you do a scan.

COMPATIBILITY
       While  not  listed  in this document, a lot of parameters compatible with nmap will also
       work.

SEE ALSO
       nmap(8), pcap(3)

AUTHORS
       This  tool  was  written  by  Robert  Graham.  The   source   code   is   available   at
       https://github.com/robertdavidgraham/masscan.

</pre>

---

### Output

```powershell
sudo masscan -p0-1023 192.168.0.1 --rate 1500 -oB output.binary

# Read Binary
sudo masscan --readscan output.binary

# Convert Binary to grappable, xml, text
sudo masscan --readscan output.binary -oG output.grepable
```

---

## Conclusion

**`masscan`** is a stateless specialized for high-speed port scanning of large networks, while **`nmap`** is a stateful ( OS discovery, version scanning, scripting engine, enumerate particular port ) versatile tool offering a wide range of scanning techniques and features for comprehensive network reconnaissance.

- **`masscan`**: Ideal for quickly identifying open ports across large IP ranges, making it suitable for network administrators and security researchers who need a high-speed overview.
- **`nmap`**: Suited for more detailed network reconnaissance, vulnerability assessment, and penetration testing. It provides a broader range of analysis and can help identify specific services and vulnerabilities on target systems.