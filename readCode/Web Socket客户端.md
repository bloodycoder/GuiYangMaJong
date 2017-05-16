#### 下面是Javascript用WebSocket的代码
    var ws = new WebSocket("ws://127.0.0.1:xx/service")
    ws.onopen = function(){}
    ws.onmessage = function(evt){window.alert(evt.data);}
    ws.onclose = function(){}
    ws.send("hello world")

  
