这里我会读代码，记录下来。

整个流程是:

TcpServer负责不停地侦听端口，然后阻塞200ms，然后继续侦听。如果侦听到了，就接收Socket.

然后新建一个TcpConnection,把Socket传入。然后调用`TcpConnection.StartRecv()`;然后TcpServer继续侦听端口。

TcpConnection执行StartRecv()，执行Recv().Recv中执行了Socket的BeginReceive(),BeginReceive有个回调函数。回调函数中，执行OnRecvMsg();OnRecvMsg()中就已经能够获得信息了。

![图片](https://github.com/bloodycoder/GuiYangMaJong/blob/master/%E7%9B%AE%E5%89%8D%E4%BB%A3%E7%A0%81%E7%BB%93%E6%9E%84.png)
