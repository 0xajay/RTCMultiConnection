---
api_name: onstream
api_description: Use this event to receive all local and remote media streams
---

{% capture html %}

  <section id="usage">
    <h2><a href="#usage">Usage</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.mediaElement;

    <span style="color:#919191">// append to &lt;body></span>
    <span style="color:#a535ae">document</span>.<span style="color:#a535ae">body</span>.<span style="color:#a535ae">appendChild</span>(video);
};
</pre>
  </section>

  <section id="description">
    <h2><a href="#description">Description</a></h2>
    <div class="datagrid">
    <table>
    <thead><tr><th>parameter</th><th>description</th></tr></thead>
    <tbody>
      <tr>
        <td>stream</td>
        <td>
            media stream object
            <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    yourOwnVideo.<span style="color:#a535ae">src</span> <span style="color:#ff5600">=</span> URL.createObjectURL(<span style="color:#a535ae">event</span>.stream);

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.stream.isScreen) {
        <span style="color:#919191">// it is screen</span>
    }

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.stream.isAudio) {
        <span style="color:#919191">// it is Audio_Only stream</span>
    }

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.stream.isVideo) {
        <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.stream.getAudioTracks().<span style="color:#a535ae">length</span> <span style="color:#ff5600">&amp;</span><span style="color:#ff5600">&amp;</span> <span style="color:#a535ae">event</span>.stream.getVideoTracks().<span style="color:#a535ae">length</span>) {
            <span style="color:#919191">// Audio+Video stream</span>
        } <span style="color:#ff5600">else</span> {
            <span style="color:#919191">// Video-Only stream</span>
        }
    }
};
</pre>
        </td>
      </tr>

      <tr>
        <td>type</td>
        <td>
          either a "local" or "remote" stream
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.<span style="color:#a535ae">type</span> <span style="color:#ff5600">===</span> <span style="color:#00a33f">'local'</span>) {
        yourOwnVideo.<span style="color:#a535ae">src</span> <span style="color:#ff5600">=</span> URL.createObjectURL(<span style="color:#a535ae">event</span>.stream);
    }

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.<span style="color:#a535ae">type</span> <span style="color:#ff5600">===</span> <span style="color:#00a33f">'remote'</span>) {
        remoteVideo.<span style="color:#a535ae">src</span> <span style="color:#ff5600">=</span> URL.createObjectURL(<span style="color:#a535ae">event</span>.stream);
    }
};
</pre>
        </td>
      </tr>

      <tr>
        <td>streamid</td>
        <td>
          unique identifier for each stream
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.mediaElement;

    <span style="color:#919191">// now you an access it using "document.getElementById"</span>
    video.<span style="color:#a535ae">id</span> <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.streamid;
};
</pre>
        </td>
      </tr>

      <tr>
        <td>mediaElement</td>
        <td>
          either &lt;audio&gt; or &lt;video&gt; element
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.mediaElement;

    <span style="color:#ff5600">if</span> (video.<span style="color:#a535ae">nodeName</span>.<span style="color:#a535ae">toLowerCase</span>() <span style="color:#ff5600">===</span> <span style="color:#00a33f">'video'</span>) {
        <span style="color:#919191">// it is &lt;video> tag</span>
    }

    <span style="color:#ff5600">if</span> (video.<span style="color:#a535ae">nodeName</span>.<span style="color:#a535ae">toLowerCase</span>() <span style="color:#ff5600">===</span> <span style="color:#00a33f">'audio'</span>) {
        <span style="color:#919191">// it is &lt;audio> tag</span>
    }

    <span style="color:#ff5600">$</span>(<span style="color:#00a33f">'body'</span>).prepend(video);
};
</pre>
        </td>
      </tr>

      <tr>
        <td>userid</td>
        <td>
          user who shared the stream
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.mediaElement;

    <span style="color:#919191">// now you can search all &lt;video></span>
    <span style="color:#919191">// whose "data-userid" matches current userid</span>
    <span style="color:#ff5600">$</span>(video).attr(<span style="color:#00a33f">'data-userid'</span>, <span style="color:#a535ae">event</span>.userid);

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.userid <span style="color:#ff5600">===</span> connection.userid) {
        <span style="color:#919191">// you shared this stream</span>
    } <span style="color:#ff5600">else</span> {
        <span style="color:#919191">// someone else (remote-user) shared this stream</span>
    }
};
</pre>
        </td>
      </tr>

      <tr>
        <td>extra</td>
        <td>
          receive extra information from the stream sender
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.userid <span style="color:#ff5600">!</span><span style="color:#ff5600">==</span> connection.userid) {
        <span style="color:#ff5600">var</span> remoteUserId <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.userid;
        <span style="color:#ff5600">var</span> remoteUserExtra <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.extra;
        <span style="color:#ff5600">var</span> hisFullName <span style="color:#ff5600">=</span> remoteUserExtra.fullName;
        <span style="color:#ff5600">var</span> hisEmail <span style="color:#ff5600">=</span> remoteUserExtra.email;
    }
};
</pre>
        </td>
      </tr>

      <tr>
        <td>isScreen</td>
        <td>
          detect if it is a "screen" stream
          <pre style="background:#fff;color:#000"><span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#919191">// using v3</span>
    <span style="color:#ff5600">var</span> isScreen <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.stream.isScreen;

    <span style="color:#919191">// using v2</span>
    <span style="color:#ff5600">var</span> isScreen <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.isScreen;

    <span style="color:#919191">// cross-versions</span>
    <span style="color:#ff5600">var</span> isScreen <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.isScreen <span style="color:#ff5600">||</span> <span style="color:#a535ae">event</span>.stream.isScreen;
};
</pre>
        </td>
      </tr>
    </tbody>
    </table>
    </div>
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

<span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstream</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.mediaElement;
    video.<span style="color:#a535ae">id</span> <span style="color:#ff5600">=</span> <span style="color:#a535ae">event</span>.streamid;
    <span style="color:#a535ae">document</span>.<span style="color:#a535ae">body</span>.<span style="color:#a535ae">insertBefore</span>(video, <span style="color:#a535ae">document</span>.<span style="color:#a535ae">body</span>.<span style="color:#a535ae">firstChild</span>);
};

<span style="color:#a535ae">connection</span>.<span style="color:#21439c">onstreamended</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(event) {
    <span style="color:#ff5600">var</span> video <span style="color:#ff5600">=</span> <span style="color:#a535ae">document</span>.<span style="color:#a535ae">getElementById</span>(<span style="color:#a535ae">event</span>.streamid);
    <span style="color:#ff5600">if</span> (video <span style="color:#ff5600">&amp;</span><span style="color:#ff5600">&amp;</span> video.<span style="color:#a535ae">parentNode</span>) {
        video.<span style="color:#a535ae">parentNode</span>.<span style="color:#a535ae">removeChild</span>(video);
    }
};

connection.openOrJoin(<span style="color:#00a33f">'your-room-id'</span>);
<span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
</pre>
  </section>

{% endcapture %}
{% include html_snippet.html html=html %}
