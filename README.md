# Network Security - Quiz 1

Tugas Scanning Keamanan Jaringan

## Penyerang:
1. apt-get install nmap

2. nmap <ip_target>

## Admin: (smtp gmail)
1. Setting security akun google menjadi less secure account

## Target: 
1. sudo su

2. apt-get install net-tools portsentry postfix mailutils

3. nano /etc/postfix/sasl_passwd:
[smtp.gmail.com]:587 <alamat_email>:<password>

4. nano /etc/postfix/main.cf
relayhost = [smtp.gmail.com]:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = 
smtp_sasl_security_level = encrypt
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt

5. postmap /etc/postfix/sasl_passwd

6. /etc/init.d/postfix /restart

7. nano /etc/default/portsentry
TCP_MODE="atcp"
UDP_MODE="audp"

8. nano /etc/portsentry/portsentry.conf
BLOCK_UDP="2"
BLOCK_TCP="2"
KILL_RUN_CMD="/usr/local/sbin/scan.sh $TARGET$ $PORT$ $MODE$"

9. nano /usr/local/sbin/scan.sh
#!/bin/bash
iptables -I INPUT -s $1 -j DROP
echo "Ada scanning dari IP $1 $2 $3" | mail -s "scanning" <email_penerima>

10. chmod +x /usr/local/sbin/scan.sh

11. iptables -F

12. /etc/init.d/portsentry restart

DONE
