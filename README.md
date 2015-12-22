# LNMP
本文主要是介绍使用ansible-playbook来安装LNMP+Memcached+Redis，我们这里选择的为使用yum源的形式进行安装的，通过yum安装的利端是能够很方便快速的解决依赖环境，但其中的弊端为无法选择自己所想安装的版本，因为我们所选的remi仓库安装的程序环境为最新最稳定版本。若使用者对版本有要求请绕行选择使用编译安装。谢谢

Nginx_install
playbook模板
nginx_intsall/
├── common
│   ├── files
│   │   ├── epel.repo
│   │   └── nginx.repo
│   └── tasks
│       ├── copy.yml
│       └── main.yml
├── nginx_install
│   ├── tasks
│   │   ├── copy.yml
│   │   ├── install_nginx.yml
│   │   ├── main.yml
│   │   └── modify_conf.yml
│   └── templates
│       └── nginx.conf.j2
└── nginx_install.yml
安装使用方法
ansible-playbook lnmmrp_install/nginx_install/nginx_install.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。
Mysql_install
playbook模板
mysql_intsall/
├── common
│   ├── files
│   │   ├── epel.repo
│   │   └── remi.repo
│   └── tasks
│       └── main.yml
├── mysql_install
│   ├── tasks
│   │   ├── copy.yml
│   │   ├── delete.yml
│   │   ├── install.yml
│   │   ├── main.yml
│   │   └── modify_conf.yml
│   └── templates
│       └── my.cnf
└── mysql_install.yml
安装使用方法
ansible-playbook lnmmrp_install/mysql_intsall/mysql_install.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。

Php_install
 playbook模板
说明：通过当前模板默认安装的为php5.5的版本，若想安装php5.4可将yum源中的remi55.repo中的enabled=1更换成enabled=0，并将remi.repo中的enabled=0换成enabled=1即可。
php_intsall/
├── common
│   ├── files
│   │   ├── epel.repo
│   │   ├── remi55.repo
│   │   ├── remi.repo
│   │   └── sysctl.sh
│   └── tasks
│       ├── copy.yml
│       ├── main.yml
│       └── sysctl.yml
├── php_install
│   ├── files
│   └── tasks
│       ├── install.yml
│       ├── main.yml
│       └── modify_conf.yml
└── php_install.yml
安装使用方法
ansible-playbook lnmmrp_install/php_intsall/php_install.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。

Memcached_install
playbook模板
memcached_intsall/
├── common
│   ├── files
│   │   ├── epel.repo
│   │   └── remi.repo
│   └── tasks
│       └── main.yml
├── memcached_install
│   ├── files
│   ├── tasks
│   │   ├── install.yml
│   │   ├── log_cut.yml
│   │   └── main.yml
│   └── templates
│       └── memcached
└── memcached_install.yml
安装使用方法
ansible-playbook lnmmrp_install/memcached_intsall/memcached_install.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。

Redis_install
playbook模板
redis_intsall/
├── common
│   ├── files
│   │   ├── epel.repo
│   │   └── remi.repo
│   └── tasks
│       └── main.yml
├── redis_install
│   ├── files
│   └── tasks
│       ├── install.yml
│       ├── main.yml
│       └── modify_conf.yml
└── redis_install.yml
安装使用方法
ansible-playbook lnmmrp_install/redis_intsall/redis_install.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。

LNMP_install
playbook模板
lnmp_intsall/
└── roles
    ├── memcached
    │   ├── files
    │   ├── tasks
    │   │   ├── install.yml
    │   │   ├── log_cut.yml
    │   │   └── main.yml
    │   └── templates
    │       └── memcached
    ├── mysql
    │   ├── files
    │   ├── tasks
    │   │   ├── copy.yml
    │   │   ├── delete.yml
    │   │   ├── install.yml
    │   │   ├── main.yml
    │   │   └── modify_conf.yml
    │   └── templates
    │       └── my.cnf
    ├── nginx
    │   ├── tasks
    │   │   ├── install_nginx.yml
    │   │   ├── main.yml
    │   │   └── modify_conf.yml
    │   └── templates
    │       └── nginx.conf.j2
    ├── php
    │   ├── files
    │   └── tasks
    │       ├── install.yml
    │       ├── main.yml
    │       └── modify_conf.yml
    ├── prepare
    │   ├── files
    │   │   ├── history.sh
    │   │   ├── LNMP.repo
    │   │   └── sysctl.sh
    │   └── tasks
    │       └── main.yml
    └── site.yml
安装使用方法
ansible-playbook lnmp_install/site.yml --extra-vars "host=192.168.1.100 user=deploy" –k
说明：--extra-vars:加载外部变量；host:定义的hosts变量；user:定义的remote_user变量，建议使用root或者拥有sudo权限的用户执行脚本；-k:使用密码认证，若已设置密钥认证可去掉-k参数。








