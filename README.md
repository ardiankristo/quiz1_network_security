
# Network Security - Quiz 1

Scanning


## Admin: (smtp gmail)
#### 1. Setup google account to "Less Secure"


## Target: 
#### 1. sudo su

#### 2. apt-get install net-tools portsentry postfix mailutils

#### 3. nano /etc/postfix/sasl_passwd:
- [smtp.gmail.com]:587 <alamat_email>:<password>

#### 4. nano /etc/postfix/main.cf
- relayhost = [smtp.gmail.com]:587
- smtp_use_tls = yes
- smtp_sasl_auth_enable = yes
- smtp_sasl_security_options = 
- smtp_sasl_security_level = encrypt
- smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
- smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt

#### 5. postmap /etc/postfix/sasl_passwd

#### 6. /etc/init.d/postfix /restart

#### 7. nano /etc/default/portsentry
- TCP_MODE="atcp"
- UDP_MODE="audp"

#### 8. nano /etc/portsentry/portsentry.conf
- BLOCK_UDP="2"
- BLOCK_TCP="2"
- KILL_RUN_CMD="/usr/local/sbin/scan.sh $TARGET$ $PORT$ $MODE$"

#### 9. nano /usr/local/sbin/scan.sh
- #!/bin/bash
- iptables -I INPUT -s $1 -j DROP
- echo "There is a scan from IP address: $1 $2 $3" | mail -s "<email_subject>" <receiver_email_address>

#### 10. chmod +x /usr/local/sbin/scan.sh

#### 11. iptables -F

#### 12. /etc/init.d/portsentry restart

## Attacker:
#### 1. apt-get install nmap

#### 2. nmap <ip_target>

DONE
