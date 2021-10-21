# Let's Encrypt with CertBot

## Install CertBot

### PreRequisites

The Linux OS version I am using:

```
ubuntu@ip-10-1-1-11:~$ cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.2 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.2 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

Check whether Python exists, and which version:

```
ubuntu@ip-10-1-1-11:~$ python3 --version
Python 3.8.10
```

Check whether CertBot exists:

```
ubuntu@ip-10-1-1-11:~$ certbot --version
Command 'certbot' not found, but can be installed with:
sudo apt install certbot
```

To install CertBot:

```
ubuntu@ip-10-1-1-11:~$ sudo snap install --classic certbot
certbot 1.19.0 from Certbot Project (certbot-eff✓) installed
```

Check CertBot version:

```
ubuntu@ip-10-1-1-11:~$ certbot --version
certbot 1.19.0
```

Check whether there are existing certificates on the system already:

```
ubuntu@ip-10-1-1-11:~$ sudo certbot certificates
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
No certificates found.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

Getting CertBot's help/information:

```
ubuntu@ip-10-1-1-11:~$ sudo certbot --help

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

  certbot [SUBCOMMAND] [options] [-d DOMAIN] [-d DOMAIN] ...

Certbot can obtain and install HTTPS/TLS/SSL certificates.  By default,
it will attempt to use a webserver both for obtaining and installing the
certificate. The most common SUBCOMMANDS and flags are:

obtain, install, and renew certificates:
    (default) run   Obtain & install a certificate in your current webserver
    certonly        Obtain or renew a certificate, but do not install it
    renew           Renew all previously obtained certificates that are near expiry
    enhance         Add security enhancements to your existing configuration
   -d DOMAINS       Comma-separated list of domains to obtain a certificate for

  --apache          Use the Apache plugin for authentication & installation
  --standalone      Run a standalone webserver for authentication
  --nginx           Use the Nginx plugin for authentication & installation
  --webroot         Place files in a server's webroot folder for authentication
  --manual          Obtain certificates interactively, or using shell script hooks

   -n               Run non-interactively
  --test-cert       Obtain a test certificate from a staging server
  --dry-run         Test "renew" or "certonly" without saving any certificates to disk

manage certificates:
    certificates    Display information about certificates you have from Certbot
    revoke          Revoke a certificate (supply --cert-name or --cert-path)
    delete          Delete a certificate (supply --cert-name)

manage your account:
    register        Create an ACME account
    unregister      Deactivate an ACME account
    update_account  Update an ACME account
  --agree-tos       Agree to the ACME server's Subscriber Agreement
   -m EMAIL         Email address for important account notifications

More detailed help:

  -h, --help [TOPIC]    print this message, or detailed help on a topic;
                        the available TOPICS are:

   all, automation, commands, paths, security, testing, or any of the
   subcommands or plugins (certonly, renew, install, register, nginx,
   apache, standalone, webroot, etc.)
  -h all                print a detailed help page including all topics
  --version             print the version number
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

Sample options/parameters :

```
certonly --manual --preferred-challenges=dns --email john@doe.net --agree-tos -d *.domain.xyz
```

Note that `*.domain.xyz` means for example:
`abc.domain.xyz` is valid, but it does ***NOT*** covers for example `abc.def.domain.xyz` .
the wild card (\*) covers only one layer under the `domain.xyz`, not more than that.



sudo certbot certonly --manual --agree-tos --email 'john.hc.doe@web.de' -d *.aadc.link

ubuntu@ip-10-1-1-11:~$ sudo certbot certonly --manual --agree-tos --email 'john.hc.doe@web.de' -d *.aadc.link
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: Y   <<<<<<<<< There is a required key-press >>>>>>>>>
Account registered.
Requesting a certificate for *.aadc.link

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:

_acme-challenge.aadc.link.

with the following value:

5Eown74U76nWOy16HB6r0EaZ3zYxiu8Ilr6bw5nNN4Y

Before continuing, verify the TXT record has been deployed. Depending on the DNS
provider, this may take some time, from a few seconds to multiple minutes. You can
check if it has finished deploying with aid of online tools, such as the Google
Admin Toolbox: https://toolbox.googleapps.com/apps/dig/#TXT/_acme-challenge.aadc.link.
Look for one or more bolded line(s) below the line ';ANSWER'. It should show the
value(s) you've just added.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue   <<<<<<<<< There is a required key-press >>>>>>>>>

Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/aadc.link/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/aadc.link/privkey.pem
This certificate expires on 2022-01-03.
These files will be updated when the certificate renews.

NEXT STEPS:
- This certificate will not be renewed automatically. Autorenewal of --manual certificates requires the use of an authentication hook script (--manual-auth-hook) but one was not provided. To renew this certificate, repeat this same certbot command before the certificate's expiry date.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
ubuntu@ip-10-1-1-11:~$



ubuntu@ip-10-1-1-11:~$ openssl x509 -text -in /etc/letsencrypt/live/aadc.link/cert.pem
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:45:f2:11:40:fe:50:b2:ad:9d:bc:cc:fb:95:65:94:9b:25
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Let's Encrypt, CN = R3
        Validity
            Not Before: Oct  5 07:10:21 2021 GMT
            Not After : Jan  3 07:10:20 2022 GMT
        Subject: CN = *.aadc.link
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:b6:57:59:9a:65:66:5f:a7:4c:69:6a:a7:f5:ce:
                    da:fe:08:37:a0:b4:2b:2f:61:e2:c6:05:ff:68:88:
                    32:f7:63:f2:c0:79:68:ab:72:84:ab:d5:e5:d9:6d:
                    4b:41:e8:36:da:95:8b:ed:ef:15:cb:54:20:d7:75:
                    6d:49:92:11:67:ed:80:8a:35:f8:73:8e:31:7e:c7:
                    6a:af:70:2b:45:de:10:ef:40:c5:e2:a4:fb:f6:5a:
                    40:ff:4c:ee:0a:9b:76:15:aa:46:3c:ea:1c:a4:cd:
                    85:e3:db:60:4f:48:1f:ed:dd:6b:99:c5:51:7b:ab:
                    9e:bb:a6:20:d1:83:61:21:03:78:35:c6:86:1a:c3:
                    86:ec:3a:b5:9a:5f:c5:62:3c:eb:97:af:76:d8:af:
                    f0:39:3b:3e:bc:fb:a3:d4:7c:5b:59:3d:af:fe:ed:
                    7f:d3:0a:f4:c4:7a:a4:13:22:da:cd:98:17:c0:1b:
                    dd:bf:51:9e:d1:d4:0d:33:b5:0c:9a:37:00:93:23:
                    df:fc:a1:5e:a5:d7:50:67:87:48:cf:00:46:b6:7d:
                    59:12:3f:25:a5:35:96:e7:e2:75:1e:67:99:12:74:
                    52:96:63:db:6c:3b:e7:3f:9e:ab:45:d7:ce:d7:91:
                    3e:13:62:1b:7a:b1:fb:3c:d5:88:0f:51:1e:b2:17:
                    4e:45
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier:
                40:4E:EA:67:05:D4:D3:5B:DE:A7:FC:95:6D:FA:72:62:B1:D2:A4:CA
            X509v3 Authority Key Identifier:
                keyid:14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6

            Authority Information Access:
                OCSP - URI:http://r3.o.lencr.org
                CA Issuers - URI:http://r3.i.lencr.org/

            X509v3 Subject Alternative Name:
                DNS:*.aadc.link
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
                  CPS: http://cps.letsencrypt.org

            CT Precertificate SCTs:
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 41:C8:CA:B1:DF:22:46:4A:10:C6:A1:3A:09:42:87:5E:
                                4E:31:8B:1B:03:EB:EB:4B:C7:68:F0:90:62:96:06:F6
                    Timestamp : Oct  5 08:10:21.341 2021 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:3B:FC:9B:93:DE:CB:F1:C0:FD:0A:30:A8:
                                62:60:B5:51:F1:4C:C1:50:CE:55:B3:C9:B8:69:B4:DC:
                                BA:E5:C1:BF:02:20:2A:6E:E0:AB:12:69:8C:70:E3:F8:
                                1F:6A:FA:06:2A:14:98:2F:22:30:78:A5:C3:A0:5E:07:
                                3D:5F:75:F3:43:3B
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 46:A5:55:EB:75:FA:91:20:30:B5:A2:89:69:F4:F3:7D:
                                11:2C:41:74:BE:FD:49:B8:85:AB:F2:FC:70:FE:6D:47
                    Timestamp : Oct  5 08:10:21.883 2021 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:45:02:20:43:94:18:1B:39:95:B7:E0:65:D3:44:84:
                                97:86:47:9C:A7:12:FE:B6:F8:B2:09:B0:92:40:8E:52:
                                6A:95:AD:94:02:21:00:9C:05:F0:27:18:8E:A3:50:91:
                                FD:13:97:99:3A:6B:A3:EF:BB:E1:87:6C:D8:B8:D1:C4:
                                F8:AF:28:91:B4:46:B9
    Signature Algorithm: sha256WithRSAEncryption
         b3:7c:31:4d:5b:10:1d:84:7b:c4:4b:97:eb:32:e1:f3:ce:55:
         c7:1a:86:2c:c5:30:9f:23:b9:34:d4:6d:e4:06:54:2e:ff:b9:
         81:f9:78:51:40:0c:81:43:91:65:87:92:24:c0:cc:7c:98:58:
         4d:54:da:af:b0:28:57:a3:7b:ad:6e:1a:00:77:56:80:f6:cc:
         4d:98:99:c2:0e:c8:ff:0b:89:76:f0:eb:bc:54:66:17:75:5f:
         d4:64:50:e5:80:02:0f:4c:3d:4a:d1:9a:98:cd:e6:ed:af:b0:
         61:9c:cb:3c:f3:71:f1:f1:d4:e2:3d:e2:64:87:7d:44:95:d8:
         98:e3:d2:72:04:69:c8:39:ec:f6:99:f8:58:1e:ff:26:d3:d2:
         5f:7a:30:6b:eb:af:98:69:34:28:df:23:84:c5:63:59:e8:07:
         31:80:46:74:0e:92:c3:93:72:4f:36:7e:e7:7e:47:aa:e4:1d:
         8a:ff:ec:d7:e3:6d:f7:37:ba:6e:f2:d4:dc:0b:cf:d9:7c:eb:
         76:42:31:25:7b:ba:55:94:cc:98:ea:97:ff:e1:cf:8e:b3:43:
         d7:50:2e:fd:d7:31:08:1b:4c:5b:c0:5f:e3:06:1c:f4:ca:81:
         bb:58:29:17:57:f9:53:61:af:2a:9f:55:d3:bf:e8:86:fe:0d:
         33:12:57:e5
-----BEGIN CERTIFICATE-----
MIIFGzCCBAOgAwIBAgISA0XyEUD+ULKtnbzM+5VllJslMA0GCSqGSIb3DQEBCwUA
MDIxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MQswCQYDVQQD
EwJSMzAeFw0yMTEwMDUwNzEwMjFaFw0yMjAxMDMwNzEwMjBaMBYxFDASBgNVBAMM
CyouYWFkYy5saW5rMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtldZ
mmVmX6dMaWqn9c7a/gg3oLQrL2HixgX/aIgy92PywHloq3KEq9Xl2W1LQeg22pWL
7e8Vy1Qg13VtSZIRZ+2AijX4c44xfsdqr3ArRd4Q70DF4qT79lpA/0zuCpt2FapG
POocpM2F49tgT0gf7d1rmcVRe6ueu6Yg0YNhIQN4NcaGGsOG7Dq1ml/FYjzrl692
2K/wOTs+vPuj1HxbWT2v/u1/0wr0xHqkEyLazZgXwBvdv1Ge0dQNM7UMmjcAkyPf
/KFepddQZ4dIzwBGtn1ZEj8lpTWW5+J1HmeZEnRSlmPbbDvnP56rRdfO15E+E2Ib
erH7PNWID1EeshdORQIDAQABo4ICRTCCAkEwDgYDVR0PAQH/BAQDAgWgMB0GA1Ud
JQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjAMBgNVHRMBAf8EAjAAMB0GA1UdDgQW
BBRATupnBdTTW96n/JVt+nJisdKkyjAfBgNVHSMEGDAWgBQULrMXt1hWy65QCUDm
H6+dixTCxjBVBggrBgEFBQcBAQRJMEcwIQYIKwYBBQUHMAGGFWh0dHA6Ly9yMy5v
LmxlbmNyLm9yZzAiBggrBgEFBQcwAoYWaHR0cDovL3IzLmkubGVuY3Iub3JnLzAW
BgNVHREEDzANggsqLmFhZGMubGluazBMBgNVHSAERTBDMAgGBmeBDAECATA3Bgsr
BgEEAYLfEwEBATAoMCYGCCsGAQUFBwIBFhpodHRwOi8vY3BzLmxldHNlbmNyeXB0
Lm9yZzCCAQMGCisGAQQB1nkCBAIEgfQEgfEA7wB1AEHIyrHfIkZKEMahOglCh15O
MYsbA+vrS8do8JBilgb2AAABfE+A6x0AAAQDAEYwRAIgO/ybk97L8cD9CjCoYmC1
UfFMwVDOVbPJuGm03Lrlwb8CICpu4KsSaYxw4/gfavoGKhSYLyIweKXDoF4HPV91
80M7AHYARqVV63X6kSAwtaKJafTzfREsQXS+/Um4havy/HD+bUcAAAF8T4DtOwAA
BAMARzBFAiBDlBgbOZW34GXTRISXhkecpxL+tviyCbCSQI5SapWtlAIhAJwF8CcY
jqNQkf0Tl5k6a6Pvu+GHbNi40cT4ryiRtEa5MA0GCSqGSIb3DQEBCwUAA4IBAQCz
fDFNWxAdhHvES5frMuHzzlXHGoYsxTCfI7k01G3kBlQu/7mB+XhRQAyBQ5Flh5Ik
wMx8mFhNVNqvsChXo3utbhoAd1aA9sxNmJnCDsj/C4l28Ou8VGYXdV/UZFDlgAIP
TD1K0ZqYzebtr7BhnMs883Hx8dTiPeJkh31EldiY49JyBGnIOez2mfhYHv8m09Jf
ejBr66+YaTQo3yOExWNZ6AcxgEZ0DpLDk3JPNn7nfkeq5B2K/+zX4233N7pu8tTc
C8/ZfOt2QjEle7pVlMyY6pf/4c+Os0PXUC791zEIG0xbwF/jBhz0yoG7WCkXV/lT
Ya8qn1XTv+iG/g0zElfl
-----END CERTIFICATE-----
ubuntu@ip-10-1-1-11:~$



--manual-auth-hook manualauthhook.sh

#!/bin/bash -ex

echo "_acme-challenge.$CERTBOT_DOMAIN TXT $CERTBOT_VALIDATION"
env



--manual-cleanup-hook manualcleanuphook.sh

#!/bin/bash -ex

echo "_acme-challenge.$CERTBOT_DOMAIN TXT $CERTBOT_VALIDATION"
env



sudo certbot renew --dry-run --manual-auth-hook /home/ubuntu/manualauthhook.sh --manual-cleanup-hook /home/ubuntu/manualcleanuphook.sh

ubuntu@ip-10-1-1-11:~$ sudo certbot renew --dry-run --manual-auth-hook /home/ubuntu/manualauthhook.sh --manual-cleanup-hook /home/ubuntu/manualcleanuphook.sh
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/aadc.link.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Simulating renewal of an existing certificate for *.aadc.link
Hook '--manual-auth-hook' for aadc.link ran with output:
 _acme-challenge.aadc.link TXT AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SHELL=/bin/bash
 SNAP_REVISION=1434
 SUDO_GID=1000
 SNAP_REAL_HOME=/root
 SNAP_USER_COMMON=/root/snap/certbot/common
 SNAP_INSTANCE_KEY=
 SUDO_COMMAND=/snap/bin/certbot renew --dry-run --manual-auth-hook /home/ubuntu/manualauthhook.sh --manual-cleanup-hook /home/ubuntu/manualcleanuphook.sh
 CERTBOT_DOMAIN=aadc.link
 SUDO_USER=ubuntu
 PWD=/home/ubuntu
 LOGNAME=root
 SNAP_CONTEXT=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 HOME=/root
 CERTBOT_PLUGIN_PATH=
 LANG=C.UTF-8
 LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
 SNAP_ARCH=amd64
 SNAP_INSTANCE_NAME=certbot
 CERTBOT_VALIDATION=AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SNAP_USER_DATA=/root/snap/certbot/1434
 SNAP_REEXEC=
 TERM=xterm
 USER=root
 CERTBOT_AUGEAS_PATH=/snap/certbot/1434/usr/lib/x86_64-linux-gnu/libaugeas.so.0
 SNAP=/snap/certbot/1434
 SNAP_COMMON=/var/snap/certbot/common
 SNAP_VERSION=1.19.0
 SHLVL=1
 SNAP_LIBRARY_PATH=/var/lib/snapd/lib/gl:/var/lib/snapd/lib/gl32:/var/lib/snapd/void
 SNAP_COOKIE=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 AUGEAS_LENS_LIB=/snap/certbot/1434/usr/share/augeas/lenses/dist
 SNAP_DATA=/var/snap/certbot/1434
 CERTBOT_SNAPPED=True
 CERTBOT_ALL_DOMAINS=aadc.link
 SNAP_NAME=certbot
 PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
 SUDO_UID=1000
 MAIL=/var/mail/root
 CERTBOT_REMAINING_CHALLENGES=0
 _=/usr/bin/env
Hook '--manual-auth-hook' for aadc.link ran with error output:
 + echo '_acme-challenge.aadc.link TXT AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw'
 + env

Certbot failed to authenticate some domains (authenticator: manual). The Certificate Authority reported these problems:
  Domain: aadc.link
  Type:   dns
  Detail: DNS problem: NXDOMAIN looking up TXT for _acme-challenge.aadc.link - check that a DNS record exists for this domain

Hint: The Certificate Authority failed to verify the DNS TXT records created by the --manual-auth-hook. Ensure that this hook is functioning correctly and that it waits a sufficient duration of time for DNS propagation. Refer to "certbot --help manual" and the Certbot User Guide.

Hook '--manual-cleanup-hook' for aadc.link ran with output:
 _acme-challenge.aadc.link TXT AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SHELL=/bin/bash
 SNAP_REVISION=1434
 SUDO_GID=1000
 SNAP_REAL_HOME=/root
 SNAP_USER_COMMON=/root/snap/certbot/common
 SNAP_INSTANCE_KEY=
 SUDO_COMMAND=/snap/bin/certbot renew --dry-run --manual-auth-hook /home/ubuntu/manualauthhook.sh --manual-cleanup-hook /home/ubuntu/manualcleanuphook.sh
 CERTBOT_DOMAIN=aadc.link
 SUDO_USER=ubuntu
 PWD=/home/ubuntu
 LOGNAME=root
 SNAP_CONTEXT=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 HOME=/root
 CERTBOT_PLUGIN_PATH=
 LANG=C.UTF-8
 LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
 SNAP_ARCH=amd64
 SNAP_INSTANCE_NAME=certbot
 CERTBOT_VALIDATION=AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SNAP_USER_DATA=/root/snap/certbot/1434
 SNAP_REEXEC=
 TERM=xterm
 USER=root
 CERTBOT_AUGEAS_PATH=/snap/certbot/1434/usr/lib/x86_64-linux-gnu/libaugeas.so.0
 SNAP=/snap/certbot/1434
 SNAP_COMMON=/var/snap/certbot/common
 SNAP_VERSION=1.19.0
 SHLVL=1
 SNAP_LIBRARY_PATH=/var/lib/snapd/lib/gl:/var/lib/snapd/lib/gl32:/var/lib/snapd/void
 SNAP_COOKIE=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 AUGEAS_LENS_LIB=/snap/certbot/1434/usr/share/augeas/lenses/dist
 SNAP_DATA=/var/snap/certbot/1434
 CERTBOT_AUTH_OUTPUT=_acme-challenge.aadc.link TXT AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SHELL=/bin/bash
 SNAP_REVISION=1434
 SUDO_GID=1000
 SNAP_REAL_HOME=/root
 SNAP_USER_COMMON=/root/snap/certbot/common
 SNAP_INSTANCE_KEY=
 SUDO_COMMAND=/snap/bin/certbot renew --dry-run --manual-auth-hook /home/ubuntu/manualauthhook.sh --manual-cleanup-hook /home/ubuntu/manualcleanuphook.sh
 CERTBOT_DOMAIN=aadc.link
 SUDO_USER=ubuntu
 PWD=/home/ubuntu
 LOGNAME=root
 SNAP_CONTEXT=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 HOME=/root
 CERTBOT_PLUGIN_PATH=
 LANG=C.UTF-8
 LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
 SNAP_ARCH=amd64
 SNAP_INSTANCE_NAME=certbot
 CERTBOT_VALIDATION=AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw
 SNAP_USER_DATA=/root/snap/certbot/1434
 SNAP_REEXEC=
 TERM=xterm
 USER=root
 CERTBOT_AUGEAS_PATH=/snap/certbot/1434/usr/lib/x86_64-linux-gnu/libaugeas.so.0
 SNAP=/snap/certbot/1434
 SNAP_COMMON=/var/snap/certbot/common
 SNAP_VERSION=1.19.0
 SHLVL=1
 SNAP_LIBRARY_PATH=/var/lib/snapd/lib/gl:/var/lib/snapd/lib/gl32:/var/lib/snapd/void
 SNAP_COOKIE=rzjZ3BqaWJtu_48tnHEm2_EOHX32G94ZOTe4mtwLn8rXJNbMXZE0
 AUGEAS_LENS_LIB=/snap/certbot/1434/usr/share/augeas/lenses/dist
 SNAP_DATA=/var/snap/certbot/1434
 CERTBOT_SNAPPED=True
 CERTBOT_ALL_DOMAINS=aadc.link
 SNAP_NAME=certbot
 PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
 SUDO_UID=1000
 MAIL=/var/mail/root
 CERTBOT_REMAINING_CHALLENGES=0
 _=/usr/bin/env
 CERTBOT_SNAPPED=True
 CERTBOT_ALL_DOMAINS=aadc.link
 SNAP_NAME=certbot
 PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
 SUDO_UID=1000
 MAIL=/var/mail/root
 CERTBOT_REMAINING_CHALLENGES=0
 _=/usr/bin/env
Hook '--manual-cleanup-hook' for aadc.link ran with error output:
 + echo '_acme-challenge.aadc.link TXT AqqmeS2_EYHQ_ur0iVF9tQmay1XkVzypY9KZhx7oJXw'
 + env
Failed to renew certificate aadc.link with error: Some challenges have failed.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
All simulated renewals failed. The following certificates could not be renewed:
  /etc/letsencrypt/live/aadc.link/fullchain.pem (failure)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1 renew failure(s), 0 parse failure(s)
Ask for help or search for solutions at https://community.letsencrypt.org. See the logfile /var/log/letsencrypt/letsencrypt.log or re-run Certbot with -v for more details.
ubuntu@ip-10-1-1-11:~$



sudo apt install unzip

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install



ubuntu@ip-10-1-1-11:~$ aws --version
aws-cli/2.2.43 Python/3.8.8 Linux/5.4.0-1049-aws exe/x86_64.ubuntu.20 prompt/off
ubuntu@ip-10-1-1-11:~$



file://sample.json
{
 "Comment": "CREATE/DELETE/UPSERT a ResourceRecord",
 "Changes": [{
 "Action": "CREATE",
  "ResourceRecordSet": {
     "Name": "a.example.com",
     "Type": "TXT",
     "TTL": 22,
     "ResourceRecords": [{ "Value": "4.4.4.4"}]
  }
 }]
}

aws route53 change-resource-record-sets --hosted-zone-id ZXXXXXXXXXX --change-batch file://sample.json
{
 "ChangeInfo": {
  "Status": "PENDING", 
  "Comment": "optional comment about the changes in this change batch request", 
  "SubmittedAt": "2018-07-10T19:39:37.757Z", 
  "Id": "/change/C3QYC83OA0KX5K"
 }
}

aws route53  get-change --id /change/C3QYC83OA0KX5K
{
 "ChangeInfo": {
  "Status": "PENDING", 
  "Comment": "optional comment about the changes in this change batch request", 
  "SubmittedAt": "2018-07-10T19:39:37.757Z", 
  "Id": "/change/C3QYC83OA0KX5K"
 }
}

aws route53  get-change --id /change/C3QYC83OA0KX5K
{
 "ChangeInfo": {
  "Status": "INSYNC", 
  "Comment": "optional comment about the changes in this change batch request", 
  "SubmittedAt": "2018-07-10T19:39:37.757Z", 
  "Id": "/change/C3QYC83OA0KX5K"
 }
}







{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "VisualEditor0",
   "Effect": "Allow",
   "Action": [
    "route53:ListTrafficPolicyVersions",
    "route53:TestDNSAnswer",
    "route53:GetHostedZone",
    "route53:GetHealthCheck",
    "route53:CreateQueryLoggingConfig",
    "route53:ListHostedZonesByName",
    "route53:CreateHealthCheck",
    "route53:ListResourceRecordSets",
    "route53:GetHostedZoneCount",
    "route53:UpdateHostedZoneComment",
    "route53:GetHealthCheckCount",
    "route53:DeleteTrafficPolicyInstance",
    "route53:CreateTrafficPolicyVersion",
    "route53:ListReusableDelegationSets",
    "route53:UpdateTrafficPolicyComment",
    "route53:UpdateTrafficPolicyInstance",
    "route53:DeleteKeySigningKey",
    "route53:GetHealthCheckLastFailureReason",
    "route53:ListTrafficPolicyInstancesByHostedZone",
    "route53:ChangeResourceRecordSets",
    "route53:ListVPCAssociationAuthorizations",
    "route53:GetReusableDelegationSetLimit",
    "route53:CreateVPCAssociationAuthorization",
    "route53:DeleteVPCAssociationAuthorization",
    "route53:ListTagsForResources",
    "route53:GetAccountLimit",
    "route53:DeleteReusableDelegationSet",
    "route53:GetGeoLocation",
    "route53:GetHostedZoneLimit",
    "route53:GetTrafficPolicy",
    "route53:ListTrafficPolicyInstances",
    "route53:DeleteTrafficPolicy",
    "route53:GetTrafficPolicyInstanceCount",
    "route53:DisableHostedZoneDNSSEC",
    "route53:GetChange",
    "route53:CreateTrafficPolicy",
    "route53:EnableHostedZoneDNSSEC",
    "route53:UpdateHealthCheck",
    "route53:DeleteHealthCheck",
    "route53:DeactivateKeySigningKey",
    "route53:ListQueryLoggingConfigs",
    "route53:ActivateKeySigningKey",
    "route53:GetCheckerIpRanges",
    "route53:ListTrafficPolicies",
    "route53:ListGeoLocations",
    "route53:DeleteHostedZone",
    "route53:GetTrafficPolicyInstance",
    "route53:GetDNSSEC",
    "route53:GetQueryLoggingConfig",
    "route53:CreateKeySigningKey",
    "route53:GetHealthCheckStatus",
    "route53:CreateReusableDelegationSet",
    "route53:ListHostedZones",
    "route53:GetReusableDelegationSet",
    "route53:CreateTrafficPolicyInstance",
    "route53:ListTagsForResource",
    "route53:ListTrafficPolicyInstancesByPolicy",
    "route53:ListHealthChecks",
    "route53:DeleteQueryLoggingConfig"
   ],
   "Resource": "*",
   "Condition": {
    "IpAddress": {
     "aws:SourceIp": "10.1.1.0/24"
    }
   }
  }
 ]
}






{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "VisualEditor0",
   "Effect": "Allow",
   "Action": [
    "s3:*"
   ],
   "Resource": "*"
  },
  {
   "Sid": "VisualEditor1",
   "Effect": "Allow",
   "Action": "s3:*",
   "Resource": "*"
  }
 ]
}



ubuntu@ip-10-1-1-11:~$ curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1
["ferredoxin"]ubuntu@ip-10-1-1-11:~$

$ echo 'Here is a string, and Here is another string.' | grep -oP '(?<=Here).*(?=string)' # Greedy match
 is a string, and Here is another 
$ echo 'Here is a string, and Here is another string.' | grep -oP '(?<=Here).*?(?=string)' # Non-greedy match (Notice the '?' after '*' in .*)
 is a 
 is another 

grep -oP '(?<=\[\").*?(?=\"\])'

curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'

ubuntu@ip-10-1-1-11:~$ curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'
proa
ubuntu@ip-10-1-1-11:~$ curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'
porkiness
ubuntu@ip-10-1-1-11:~$ curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'
oxalate
ubuntu@ip-10-1-1-11:~$

TestVariable=`curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'` ; echo "TestVariable's value is : $TestVariable"

ubuntu@ip-10-1-1-11:~$ TestVariable=`curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'` ; echo "TestVariable's value is : $TestVariable"
TestVariable's value is : gizzard
ubuntu@ip-10-1-1-11:~$ TestVariable=`curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'` ; echo "TestVariable's value is : $TestVariable"
TestVariable's value is : barrage
ubuntu@ip-10-1-1-11:~$ TestVariable=`curl --retry 333 -s http://random-word-api.herokuapp.com/word?number=1 | grep -oP '(?<=\[\").*?(?=\"\])'` ; echo "TestVariable's value is : $TestVariable"
TestVariable's value is : deadheaded
ubuntu@ip-10-1-1-11:~$




















