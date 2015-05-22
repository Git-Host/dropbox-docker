Dropbox的 - 泊坞窗
写的Dropbox的服务器应用程序的一个码头工人的形象。

此图像提供了所谓的后更新挂钩的单一有用的功能。你的应用程序的图像可以提供这样的挂钩，这将会运行时的Dropbox下的文件进行更新。见example/nanoc - 静态站点生成无缝使用Dropbox的。

##快速启动

让自己的Ubuntu14.04的机器，然后：

```bash
# install docker
apt-get -y install docker.io make

# make image
make

# first-time setup; add container to your docker account
make shell
root@3951be1e6b1f:~# launch setup
... go to the URL
... Ctrl-c after "This computer is now linked to Dropbox."

# run forever
make run
```

## Experiment log

### Bittorrent Sync failed

btsync seemed like the perfect solution, but I consistently noticed data loss due to timestamps. This has been discussed in the [BT forum](http://forum.bittorrent.com/topic/20104-reproducible-data-loss-same-as-old-file-overwriting-new-files/).

###Dropbox

Dropbox也不是完美的;如果攻击者能够访问到服务器实例，他得到访问您的Dropbox的所有文件（选择性同步是无解在这里）。 Dropbox的API是不够的我们purposs;其同步API不能从服务器使用，其服务器API似乎没有做无缝同步。这是我从我粗略他们的API文档的阅读聚集。

然而，有一个解决办法，这是我在探索：创建一个辅助的Dropbox帐户和共享的特定文件夹到该帐户。这样一来，如果该服务器实例被泄露，仅该特定文件夹将是脆弱的。

使用Dropbox的一个意想不到的好处是，同步感觉快很多（瞬时）相比，btsync。
