---
api_name: DetectRTC
api_description: Check if your users has microphone, camera or speakers
---

{% capture html %}

  <section>
    <p>Check if your users has microphone, camera or speakers. Check if they are using WebRTC compatible web browser.</p>
    <p>You can try <a href="https://www.webrtc-experiment.com/DetectRTC/" target="_blank">DetectRTC live-demo here</a>.</p>
  </section>

  <section id="detect-microphone">
    <h2><a href="#detect-microphone">Detect Microphone</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">if</span> (connection.DetectRTC.hasMicrophone <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) {
    <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please attach a microphone device.'</span>);

    <span style="color:#919191">// or ignore microphone</span>
    connection.mediaConstraints.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">false</span>;
    connection.session.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">false</span>;
}
</pre>
  </section>

  <section id="detect-camera">
    <h2><a href="#detect-camera">Detect Web-Camera</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">if</span> (connection.DetectRTC.hasWebcam <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) {
    <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please attach a camera device.'</span>);

    <span style="color:#919191">// or ignore camera</span>
    connection.mediaConstraints.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">false</span>;
    connection.session.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">false</span>;
}
</pre>
  </section>

  <section id="detect-speakers">
    <h2><a href="#detect-speakers">Detect Speakers</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">if</span> (connection.DetectRTC.hasSpeakers <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) {
    <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please attach a speaker device. You will unable to hear the incoming audios.'</span>);
}
</pre>
  </section>

  <section id="DetectRTC-load">
    <h2><a href="#DetectRTC-load">Always use "DetectRTC.load"</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#919191">// it is recommended to checked above three features inside "DetectRTC.load" method</span>
connection.DetectRTC.<span style="color:#a535ae">load</span>(<span style="color:#ff5600">function</span>() {
    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasMicrophone <span style="color:#ff5600">===</span> <span style="color:#a535ae">true</span>) {
        <span style="color:#919191">// enable microphone</span>
        connection.mediaConstraints.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
        connection.session.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
    }

    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasWebcam <span style="color:#ff5600">===</span> <span style="color:#a535ae">true</span>) {
        <span style="color:#919191">// enable camera</span>
        connection.mediaConstraints.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
        connection.session.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
    }

    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasSpeakers <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) { <span style="color:#919191">// checking for "false"</span>
        <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please attach a speaker device. You will unable to hear the incoming audios.'</span>);
    }
});
</pre>
  </section>

  <section id="get-microphones-cameras">
    <h2><a href="#get-microphones-cameras">Get list of all microphone and camera devices</a></h2>
    <pre style="background:#fff;color:#000">connection.DetectRTC.<span style="color:#a535ae">load</span>(<span style="color:#ff5600">function</span>() {
    <span style="color:#919191">// you can access all microphones using "DetectRTC.audioInputDevices"</span>
    connection.DetectRTC.audioInputDevices.forEach(<span style="color:#ff5600">function</span>(device) {
        <span style="color:#ff5600">var</span> option <span style="color:#ff5600">=</span> <span style="color:#a535ae">document</span>.<span style="color:#a535ae">createElement</span>(<span style="color:#00a33f">'option'</span>);

        <span style="color:#919191">// this is what people see</span>
        option.innerHTML <span style="color:#ff5600">=</span> device.<span style="color:#a535ae">label</span>;

        <span style="color:#919191">// but this is what inernally used to select relevant device</span>
        option.<span style="color:#a535ae">value</span> <span style="color:#ff5600">=</span> device.<span style="color:#a535ae">id</span>;

        <span style="color:#919191">// append to your choice</span>
        <span style="color:#a535ae">document</span>.querySelector(<span style="color:#00a33f">'select'</span>).<span style="color:#a535ae">appendChild</span>(option);
    });

    <span style="color:#919191">// you can access all cameras using "DetectRTC.videoInputDevices"</span>
    connection.DetectRTC.videoInputDevices.forEach(<span style="color:#ff5600">function</span>(device) {
        <span style="color:#ff5600">var</span> option <span style="color:#ff5600">=</span> <span style="color:#a535ae">document</span>.<span style="color:#a535ae">createElement</span>(<span style="color:#00a33f">'option'</span>);

        <span style="color:#919191">// this is what people see</span>
        option.innerHTML <span style="color:#ff5600">=</span> device.<span style="color:#a535ae">label</span>;

        <span style="color:#919191">// but this is what inernally used to select relevant device</span>
        option.<span style="color:#a535ae">value</span> <span style="color:#ff5600">=</span> device.<span style="color:#a535ae">id</span>;

        <span style="color:#919191">// append to your choice</span>
        <span style="color:#a535ae">document</span>.querySelector(<span style="color:#00a33f">'select'</span>).<span style="color:#a535ae">appendChild</span>(option);
    });
});
</pre>
  </section>

  <section id="choose-webcam-microphone">
    <h2><a href="#choose-webcam-microphone">How to select/use specific microphone or camera</a></h2>
    <pre style="background:#fff;color:#000">connection.mediaConstraints <span style="color:#ff5600">=</span> {
    audio: {
        mandatory: {},
        optional: [{
            sourceId: <span style="color:#00a33f">'your-microphone-id'</span>
        }]
    },
    video: {
        mandatory: {},
        optional: [{
            sourceId: <span style="color:#00a33f">'your-camera-id'</span>
        }]
    }
};

<span style="color:#ff5600">if</span> (connection.DetectRTC.browser.<span style="color:#a535ae">name</span> <span style="color:#ff5600">===</span> <span style="color:#00a33f">'Firefox'</span>) {
    connection.mediaConstraints <span style="color:#ff5600">=</span> {
        audio: {
            deviceId: <span style="color:#00a33f">'your-microphone-id'</span>
        },
        video: {
            deviceId: <span style="color:#00a33f">'your-camera-id'</span>
        }
    };
}
</pre>
  </section>

  <section id="isWebRTCSupported">
    <h2><a href="#isWebRTCSupported">Detect if WebRTC supported</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">if</span> (connection.DetectRTC.isWebRTCSupported <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) {
    <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please try a WebRTC compatible web browser e.g. Chrome, Firefox or Opera.'</span>);
}
</pre>
  </section>

  <section id="DetectRTC">
    <h2><a href="#DetectRTC">DetectRTC Documentation</a></h2>
    <p style="padding-left: 20px;">Please check DetectRTC complete documentation here: <a href="https://github.com/muaz-khan/DetectRTC">https://github.com/muaz-khan/DetectRTC</a></p>
  </section>

  <section id="demo">
    <h2><a href="#demo">Demo</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/dist/RTCMultiConnection.min.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
<span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/socket.io/socket.io.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>

<span style="color:#ff5600">&lt;</span>script<span style="color:#ff5600">></span>
<span style="color:#ff5600">var</span> connection <span style="color:#ff5600">=</span> <span style="color:#ff5600">new</span> <span style="color:#21439c">RTCMultiConnection</span>();

<span style="color:#919191">// this line is VERY_important</span>
connection.socketURL <span style="color:#ff5600">=</span> <span style="color:#00a33f">'https://rtcmulticonnection.herokuapp.com:443/'</span>;

connection.session <span style="color:#ff5600">=</span> {
    audio: <span style="color:#a535ae">false</span>,
    video: <span style="color:#a535ae">false</span>,
    data: <span style="color:#a535ae">true</span> <span style="color:#919191">// at least data-connection must open if he do not have camera+mic</span>
};

connection.DetectRTC.<span style="color:#a535ae">load</span>(<span style="color:#ff5600">function</span>() {
    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasMicrophone <span style="color:#ff5600">===</span> <span style="color:#a535ae">true</span>) {
        <span style="color:#919191">// enable microphone</span>
        connection.mediaConstraints.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
        connection.session.audio <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
    }

    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasWebcam <span style="color:#ff5600">===</span> <span style="color:#a535ae">true</span>) {
        <span style="color:#919191">// enable camera</span>
        connection.mediaConstraints.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
        connection.session.video <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
    }

    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasMicrophone <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span> <span style="color:#ff5600">&amp;</span><span style="color:#ff5600">&amp;</span>
        connection.DetectRTC.hasWebcam <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) {
        <span style="color:#919191">// he do not have microphone or camera</span>
        <span style="color:#919191">// so, ignore capturing his devices</span>
        connection.dontCaptureUserMedia <span style="color:#ff5600">=</span> <span style="color:#a535ae">true</span>;
    }

    <span style="color:#ff5600">if</span> (connection.DetectRTC.hasSpeakers <span style="color:#ff5600">===</span> <span style="color:#a535ae">false</span>) { <span style="color:#919191">// checking for "false"</span>
        <span style="color:#a535ae">alert</span>(<span style="color:#00a33f">'Please attach a speaker device. You will unable to hear the incoming audios.'</span>);
    }

    connection.openOrJoin(<span style="color:#00a33f">'your-room-id'</span>);
});
<span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
</pre>
  </section>

{% endcapture %}
{% include html_snippet.html html=html %}
