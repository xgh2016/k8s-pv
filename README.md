k8s-pv
链接：https://share.weiyun.com/56qguvn 密码：wzku78

### 一、K8S二进制集群安装
K8S环境规划

ip规划
172.16.8.81        k8s-master01
172.16.8.82        k8s-master02
172.16.8.83        k8s-nodes01
172.16.8.84        k8s-nodes02
172.16.8.85        k8s-harbor

软件版本
OS: Centos7.5
Kubernetes 1.12
Docker  18.-ce
Etcd    3.x
Flannel  0.10

硬件
CPU:2C
内存:2G
磁盘:40G

安装ansible
安装epel源
yum install epel-release -y
yum -y install ansible

自签EtdSSL证书




cat > ca-config.json <<EOF
{
  "signing": {
    "default": {
      "expiry": "87600h"
    },
    "profiles": {
      "www": {
         "expiry": "87600h",
         "usages": [
            "signing",
            "key encipherment",
            "server auth",
            "client auth"
        ]
      }
    }
  }
}
EOF

cat > ca-csr.json <<EOF
{
    "CN": "etcd CA",
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "ShenZhen",
            "ST": "ShenZhen"
        }
    ]
}
EOF

cat > server-csr.json <<EOF
{
    "CN": "etcd",
    "hosts": [
    "172.16.8.81",
    "172.16.8.82",
    "172.16.8.83"
    ],
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "ShenZhen",
            "ST": "ShenZhen"
        }
    ]
}
EOF



二、

