# bash shell
Bash Shell cgi script &amp;&amp; html form parse

## Make file & change configuration parameters "$IP" "$HNAME" "$WORKDIR":
$ vim install.sh

---
IP="1.1.1.1"<br>
HNAME="example.com"<br>
WORKDIR="/var/www/example.com/"<br>
mkdir -p "${WORKDIR}/cgi-bin/"
git clone -l https://github.com/1nvok/bash.git "${WORKDIR}/cgi-bin/"<br>
chown -R apache:apache "${WORKDIR}/cgi-bin/"<br>
chmod +x "${WORKDIR}/cgi-bin/todo"<br>
chmod +x "${WORKDIR}/cgi-bin/addfile"<br>
chmod +x "${WORKDIR}/cgi-bin/delfile"<br>
chmod +x "${WORKDIR}/cgi-bin/delall"<br>

cat <<EOF >> /etc/httpd/conf/httpd.conf<br>
<VirtualHost $IP:80><br>
       ServerName $HNAME<br>
       ServerAlias $HNAME<br>
       ServerAdmin admin@$HNAME<br>
       DocumentRoot $WORKDIR<br>
<br>
        ScriptAlias "/cgi-bin/" "${WORKDIR}cgi-bin/"<br>

</VirtualHost><br>
EOF

if [ "$?" -eq 0 ]; then<br>
echo 'OK'; else<br>
echo 'FAILED =('; fi

---
<br>
$ bash install.sh<br>
$ systemctl reload httpd
