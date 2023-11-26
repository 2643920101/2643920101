# 部署Gateway
 
- 进入baas-gateway目录下，通过docker安装mysql

``sudo docker pull mysql:5.7``
![image name](https://github.com/2643920101/baasmanager/blob/main/d6e5d54a3fb20d9f310ead746fcfe40.png)


- 通过docker启动MySQL容器


**记住添加后返回的容器ID**
```
sudo docker run -p 3306:3306 --name apimysql \
> -e MYSQL_ROOT_PASSWORD=123456 \
> -d mysql:5.7
```
![image name](https://github.com/2643920101/baasmanager/blob/main/2.png)



-  查看所有docker容器，是否有mysql的容器

``sudo docker images``
![image name](https://github.com/2643920101/baasmanager/blob/main/3.png)

- 以容器的形式安装mysql 需要进入容器内部才可以使用mysql

- 进入 MySQL 容器的 shell

``sudo docker exec -it apimysql bash``
![image name](https://github.com/2643920101/baasmanager/blob/main/4.png)

- 将数据库配置文件复制进容器内

```
sudo docker cp mysql.sql 67af2612f19b78061329b3f169def2dc9c4485c6cf3acb7774ac5ad62a203fb8:/root
```
![image name](https://github.com/2643920101/baasmanager/blob/main/5.png)


- 重新进入 MySQL 容器的 shell

``sudo docker exec -it apimysql bash``

- 在容器中使用 mysql 命令登录 MySQL：密码123456

``mysql -u root -p``

- 查看数据库管理系统中的所有数据库

``show databases;``

![image name](https://github.com/2643920101/baasmanager/blob/main/6.png)

- 配置mysql.sql数据库

``source /root/mysql.sql``

![image name](https://github.com/2643920101/baasmanager/blob/main/7.png)

- 再次查看数据库管理系统中的所有数据库

``show databases;``

![image name](https://github.com/2643920101/baasmanager/blob/main/8.png)

- 修改配置文件 gwconfig.yaml

``vim gwconfig.yaml``

![image name](https://github.com/2643920101/baasmanager/blob/main/9.png)

- 配置Go环境

```
go env -w GO111MODULE=on

go env -w GOPROXY=https://goproxy.cn,direct
```
![image name](https://github.com/2643920101/baasmanager/blob/main/10.png)

- 安装gcc，g++
```
sudo apt install gcc

sudo apt install g++
```
![image name](https://github.com/2643920101/baasmanager/blob/main/11.png)

- 更新go运行环境

``go build ./main.go``

- 执行运行

``go run main.go``
![image name](https://github.com/2643920101/baasmanager/blob/main/12.png)
![image name](https://github.com/2643920101/baasmanager/blob/main/13.png)

完成

