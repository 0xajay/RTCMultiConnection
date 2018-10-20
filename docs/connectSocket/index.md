---
api_name: connectSocket
api_description: Open socket.io connection without opening/joining any room
---

{% capture html %}

  <section id="usage">
    <h2><a href="#usage">Usage</a></h2>
    <pre style="background:#fff;color:#000">connection.connectSocket(<span style="color:#ff5600">function</span>() {
    <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Successfully connected to socket.io server.'</span>);

    connection.socket.emit(<span style="color:#00a33f">'howdy'</span>, <span style="color:#00a33f">'hello'</span>);
});
</pre>
  </section>

  <section id="demo">
    <h2><a href="#demo">Demo</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/dist/RTCMultiConnection.min.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
<span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/socket.io/socket.io.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>

<span style="color:#ff5600">&lt;</span>script<span style="color:#ff5600">></span>
<span style="color:#ff5600">var</span> connection <span style="color:#ff5600">=</span> <span style="color:#ff5600">new</span> <span style="color:#21439c">RTCMultiConnection</span>();

<span style="color:#919191">// this line is VERY_important</span>
connection.socketURL <span style="color:#ff5600">=</span> <span style="color:#00a33f">'https://rtcmulticonnection.herokuapp.com:443/'</span>;

<span style="color:#919191">// if you want audio+video conferencing</span>
connection.session <span style="color:#ff5600">=</span> {
    audio: <span style="color:#a535ae">true</span>,
    video: <span style="color:#a535ae">true</span>
};

connection.socketCustomEvent <span style="color:#ff5600">=</span> <span style="color:#00a33f">'private-secure-chat'</span>;
connection.connectSocket(<span style="color:#ff5600">function</span>() {
    <span style="color:#21439c">console</span><span style="color:#a535ae">.info</span>(<span style="color:#00a33f">'Successfully connected to socket.io server.'</span>);

    connection.socket.emit(connection.socketCustomEvent, <span style="color:#00a33f">'anyone-in-the-house?'</span>);
    connection.socket.on(connection.socketCustomEvent, <span style="color:#ff5600">function</span>(message) {
        <span style="color:#ff5600">if</span> (message <span style="color:#ff5600">===</span> <span style="color:#00a33f">'anyone-in-the-house?'</span>) {
            <span style="color:#919191">// because each and every user opened unique-room</span>
            <span style="color:#919191">// their "userid" is always considered "roomid"</span>
            connection.socket.emit(connection.socketCustomEvent, {
                joinMe: connection.userid <span style="color:#919191">// share room-id so they can join</span>
            });
            <span style="color:#ff5600">return</span>;
        }

        <span style="color:#ff5600">if</span> (message.joinMe) {
            <span style="color:#919191">// one can join many rooms</span>
            connection.<span style="color:#a535ae">join</span>(message.joinMe);
        }
    });

    <span style="color:#919191">// each and every user can open unique room</span>
    connection.<span style="color:#a535ae">open</span>(connection.userid);
});
<span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
</pre>
  </section>

{% endcapture %}
{% include html_snippet.html html=html %}
