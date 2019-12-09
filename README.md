# Kubernetes v1.16 高可用集群自动部署（离线版）
>### 确保所有节点系统时间一致
### 1、下载所需文件

> 确保所有节点系统时间一致

下载Ansible部署文件：

```
git clone https://github.com/strive-after/Ansible-K8S.git
cd ansible-install-k8s
```

软件包地址：

```
http://39.105.114.198
找对应的K8S版本
```
### 2、修改Ansible文件

修改hosts文件，根据规划修改对应IP和名称。

```
vi hosts
```
修改group_vars/all.yml文件，修改软件包目录和证书可信任IP。

```
vim group_vars/all.yml
software_dir: '/root/binary_pkg'
...
cert_hosts:
  k8s:
  etcd:
```
## 3、一键部署
### 架构图
单Master架构
![avatar](https://github.com/lizhenliang/ansible-install-k8s/blob/master/single-master.jpg)
多Master架构
![avatar](https://github.com/lizhenliang/ansible-install-k8s/blob/master/multi-master.jpg)
### 部署命令
单Master版：
```
ansible-playbook -i hosts single-master-deploy.yml -uroot -k
```
多Master版：
```
ansible-playbook -i hosts multi-master-deploy.yml -uroot -k
```

## 4、部署控制
如果安装某个阶段失败，可针对性测试.

例如：只运行部署插件
```
ansible-playbook -i hosts single-master-deploy.yml -uroot -k --tags addons
```
