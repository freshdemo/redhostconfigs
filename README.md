Often you will want to send a phishing or malicious email from an attacking/red host through your phishy infrastructure using the repo <a href="https://github.com/freshdemo/mailanddns" target="_blank">https://github.com/freshdemo/mailanddns</a>.

To facilitate this a local MTA will need to be setup on your attacking/red host, such as Kali Linux. The local MTA will accept mail on TCP port 25 and then send it directly to your smarthost, being freshdemo/mailanddns.

<h3>Step 1 - update /etc/resolv.conf</h3>
Important to note that if you want to use a locally routable domain, in this case example.com, you will also need to add the following to the top line of /etc/resolv.conf. You can use mailanddns for all DNS queries as anything not local to the name server are sent to 1.1.1.1.

<br><code>
  nameserver IP.address.of.mailanddns
                 </code>

<h3>Step 2 - Setup a local MTA with Smart Host</h3>

This step is required to forward mail to external domains to the SMTP server in the mailanddns infrastructure. You will likely have to edit the file and change the IP from 10.1.4.4 to the IP of your mail server. Also take note that the port being used in this configuration is 2225, which coincides with the documented way of running mailanddns.

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

<h3>Step 3 - Send a Test Email</h3>

There are a couple of txt files in this repository that each contain a full HTML email you can send from the command line with the following. In order for this to work you must configure the local MTA as described above (or similarly), and have the SMTP/IMAP/DNS server <a href="https://github.com/freshdemo/mailanddns" target="_blank">https://github.com/freshdemo/mailanddns</a>.

<code>
  sendmail -t < phishing-credential-harvest.txt
                                               </code>    
                                           
