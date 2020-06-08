Often you will want to send a phishing or malicious email from an attacking/red host through your phishy infrastructure (using the repo (freshdemo/mailanddns).

To facilitate this a local MTA will need to be setup on your attacking/red host, such as Kali Linux. The local MTA will accept mail on TCP port 25 and then send it directly to your smarthost, being freshdemo/mailanddns.

<h3>Step 1 - update /etc/resolv.conf</h3>
Important to note that if you want to use a locally routable domain, in this case example.com, you will also need to add the following to the top line of /etc/resolv.conf. You can use mailanddns for all DNS queries as anything not local to the name server are sent to 1.1.1.1.

<code>
  nameserver IP.address.of.mailanddns
                 </code>

<h3>Step 2 - Setup a local MTA with Smart Host</h3>
On the host run the following commands;
<br>
<code>
    apt-get install exim4<br>
  </code><br>
  <code>
    git clone https://github.com/freshdemo/smarthost /root
  </code><br>
  <code>
    cp update-exim4.conf.conf /etc/exim4
  </code><br>
  <code>
    update-exim4.conf (this is a command)
  </code><br>
  <code>
    service exim4 reload OR /etc/init.d/exim4 restart (depending on your distro)
  </code><br>
