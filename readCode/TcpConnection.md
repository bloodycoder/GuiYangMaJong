文件位于TcpServer.cs
### TcpConnectionBase

栈内变量,`Socket::m_socket`,`AsyncCallback::m_sendCallBack`,`AsyncCallback::m_recvCallBack`,`ReceiveBuffer::m_recvBuff`,int `hasClosed`;

    public TcpConnectionBase(Socket socket, int maxmsgsize, int maxbuffsize)
    protected virtual void OnClose() //在Close()调用之后调用。
    protected virtual bool OnRecvMsg(TcpMessageBase msg)  
    public virtual void Close()      //关闭连接。并调用Close()
    public virtual void SendMsg(TcpMessageBase msg)//通过Socket发送信息。
    protected void SendCallBack(IAsyncResult result)
    public void StartRecv() 对Recv()的封装
    protected void Recv()
    protected void RecvCallBack(IAsyncResult result)
    
#### TcpConnection

TcpConnection是一个继承了TcpConnectionBase的类。

栈内变量，User::UserObj，int LastMsgTime 一个int的值

    public TcpConnection(Socket socket, TcpServer.TcpServerConfig config) m_recvBuff定义于基类，赋一个新值，然后用TimeUtil.CurrentUnixTime()刷新一次LastMsgTime.
    public string getIP() 利用m_socket里面的信息，获得IP
    public bool IsConOpen(int dt) 输入当前时间，检测TCP con是否断开。
    protected override bool OnRecvMsg(TcpMessageBase msgbase)
    public void OnLogin(User user)
    protected override void OnClose()
    public void LoginOnOther()
    public void SendKickOffMsg(int reason)
IsConOpen方法. 

OnRecvMsg方法. 定义了一个TcpMessage,它复写了一个Encode方法。 打印了一次日志，刷新一次LastMsgTime。

#### TcpConnectionManager

TcpConnection多次跟TcpConnectionManager.Instance 通信。

     public static TcpConnectionManager Instance = new TcpConnectionManager();
     TcpConnectionManager.Instance.createMsg(this, msg);
     
TcpConnectionManager维护了一个m_conns字典。key是user_id，值是Connection的值。



#### 其他

向Log打印

    Log.Info("hello");
   
Log错误
    Log.Error("error");
    
socket.Shutdown()在socket.Close()之前调用，作用是保证在套接字关闭前信息全收到了。

#### 索引

`TcpManager`用字典管理所有的Tcp链接。Tcp链接的类型是`InnerTcpConnection`，继承自`TcpConnectionBase`.保存在m_conns.

`TcpConnectionManager`
