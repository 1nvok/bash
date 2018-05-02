# bash
Bash Shell cgi script &amp;&amp; html form parse

### Make file & change configuration parameters "$IP" "$HNAME" "$WORKDIR":
$ vim install.sh

IP="1.1.1.1"

HNAME="example.com"

WORKDIR="/var/www/example.com/"

mkdir -p "${WORKDIR}/cgi-bin/"

git clone -l https://github.com/1nvok/bash.git "${WORKDIR}/cgi-bin/"

chown -R apache:apache "${WORKDIR}/cgi-bin/"

chmod +x "${WORKDIR}/cgi-bin/todo"

chmod +x "${WORKDIR}/cgi-bin/addfile"

chmod +x "${WORKDIR}/cgi-bin/delfile"

chmod +x "${WORKDIR}/cgi-bin/delall"



cat <<EOF >> /etc/httpd/conf/httpd.conf
	
<VirtualHost $IP:80>

        ServerName $HNAME
	
        ServerAlias $HNAME
	
        ServerAdmin admin@$HNAME
	
        DocumentRoot $WORKDIR
	
        ScriptAlias "/cgi-bin/" "${WORKDIR}cgi-bin/"

</VirtualHost>

EOF

if [ "$?" -eq 0 ]; then

echo 'OK'; else

echo 'FAILED =('; fi

$ bash install.sh

$ systemctl reload httpd
