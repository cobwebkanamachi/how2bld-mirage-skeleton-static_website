# how2bld-mirage-skeleton-static_website
This is a tiny tips on building https://github.com/mirage/mirage-skeleton .<BR>
Mainly I refer urls shown bellow.<BR>
http://www.skjegstad.com/blog/2015/01/19/mirageos-xen-virtualbox/ <BR>
https://github.com/ocaml/opam/issues/2110 <BR>
<BR>
1. base info<BR>
1.1 host configuration<BR>
osx yosemite 10.10.5<BR>
vbox 5.0.10 r104061<BR>
ubuntu 14.04.4 LTS, Trusty Tahr (net install with ubuntu desktop)<BR>
2. build steps briefly<BR>
2.1 mainly shown 2 urls above.<BR>
2.2 changes<BR>
I build/install opam from tar ball.<BR>
https://github.com/ocaml/opam/releases<BR>
opam-full-1.2.2.tar.gz<BR>
https://github.com/ocaml/opam/releases/download/1.2.2/opam-full-1.2.2.tar.gz<BR>
gzip -dc opam-full-1.2.2.tar.gz |tar xvf -<BR>
opam make procedures are shown bellow.<BR>
https://github.com/ocaml/opam/issues/2110 <BR>
I install aspcupd seprately by apt-get install.<BR>
2.3 xen etc.<BR>
see bellow.<BR>
http://www.skjegstad.com/blog/2015/01/19/mirageos-xen-virtualbox/ <BR>
test by cmd line bellow.<BR>
xl list<BR>
xl info shows bellow<BR>
<pre>
# xl info
host                   : ubuntu
release                : 3.13.0-86-generic
version                : #131-Ubuntu SMP Thu May 12 23:33:13 UTC 2016
machine                : x86_64
nr_cpus                : 1
max_cpu_id             : 0
nr_nodes               : 1
cores_per_socket       : 1
threads_per_core       : 1
cpu_mhz                : 2294
hw_caps                : (snip:-)
virt_caps              :
total_memory           : 1651
free_memory            : 383
sharing_freed_memory   : 0
sharing_used_memory    : 0
outstanding_claims     : 0
free_cpus              : 0
xen_major              : 4
xen_minor              : 4
xen_extra              : .2
xen_version            : 4.4.2
xen_caps               : xen-3.0-x86_64 xen-3.0-x86_32p 
xen_scheduler          : credit
xen_pagesize           : 4096
platform_params        : virt_start=0xffff800000000000
xen_changeset          : 
xen_commandline        : placeholder
cc_compiler            : gcc (Ubuntu 4.8.2-19ubuntu1) 4.8.2
cc_compile_by          : stefan.bader
cc_compile_domain      : canonical.com
cc_compile_date        : Wed Feb 24 21:00:00 UTC 2016
xend_config_format     : 4
</pre>
2.4 network config<BR>
see bellow.<BR>
http://www.skjegstad.com/blog/2015/01/19/mirageos-xen-virtualbox/ <BR>
I tweak ip address range only.<BR>
And used tanctl and ifconfig.<BR>
eth1 is hostonly network made on vbox side.
on ubuntu, you would better to make tap0 for example 10.0.0.1/255.255.255.0.
I reffer /etc/network/interfaces shown url(then added some).
<BR>
3. mirage_skeleton/static_website
mirage configure cmdline is shown bellow.
http://www.skjegstad.com/blog/2015/01/19/mirageos-xen-virtualbox/ <BR>
you would use opam swith to use up2date ocaml compiler.
4. test result<BR>
xl create www.xl -c<BR>
app's listen port is 8080(default).<BR>
that described on dispatch.ml TCP 8080<BR>
<BR>
    $ curl 10.0.0.2:8080<BR>
    <html>
    <body>
    <h1>Hello Mirage World!</h1>
    </body>
    </html>
dom: www shows bellow:<BR>
Netif.connect 0<BR>
Netfront.create: id=0 domid=0<BR>
 sg:true gso_tcpv4:true rx_copy:true rx_flip:false smart_poll:false<BR>
MAC: xx:xx:xx:xx:xx:xx<BR>
Attempt to open(/dev/urandom)!<BR>
Unsupported function getpid called in Mini-OS kernel<BR>
Unsupported function getppid called in Mini-OS kernel<BR>
Manager: connect<BR>
Manager: configuring<BR>
Manager: Interface to 10.0.0.2 nm 255.255.255.0 gw [10.0.0.1]<BR>
ARP: sending gratuitous from 10.0.0.2<BR>
Manager: configuration done<BR>
ARP responding to: who-has 10.0.0.2?<BR>
ARP: transmitting probe -> 10.0.0.5<BR>
ARP: updating 10.0.0.5 -> xx:xx:xx:xx:xx:xx<BR>
ARP: timeout 10.0.0.5<BR>
ARP: transmitting probe -> 10.0.0.5<BR>
ARP: updating 10.0.0.5 -> xx:xx:xx:xx:xx:xx<BR>
ARP: timeout 10.0.0.5<BR>
ARP: transmitting probe -> 10.0.0.5<BR>
ARP: updating 10.0.0.5 -> xx:xx:xx:xx:xx:xx<BR>
conn 1 closed<BR>
ARP: timeout 10.0.0.5<BR>
