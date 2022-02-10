# SSH 免登

* 1、先在所有服务器(master,slave1,slave2)上执行命令：

  > ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
* 2、而后在所有服务器上执行命令：

  > cat ~/.ssh/id_dsa.pub >>~/.ssh/authorized_keys

* 3、之后将每台服务器上的id_dsa.pub公钥发送到其他机器的/tmp文件夹下，如在master上执行

  > scp ~/.ssh/id_dsa.pub slave1:/tmp/
  > scp ~/.ssh/id_dsa.pub slave2:/tmp/

* 4、之后在其他的机器上将公钥追加到各自的authorized_keys里，执行以下命令：

  > cat /tmp/id_dsa.pub >>~/.ssh/authorized_keys
  > cat /tmp/id_dsa.pub >>~/.ssh/authorized_keys

* 测试（master服务器）

  > ssh slave