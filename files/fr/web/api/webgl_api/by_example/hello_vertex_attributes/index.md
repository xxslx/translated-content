---
title: Introduction aux attributs de vertex
slug: Web/API/WebGL_API/By_example/Hello_vertex_attributes
translation_of: Web/API/WebGL_API/By_example/Hello_vertex_attributes
---

{{PreviousNext("Apprendre/WebGL/Par_exemple/Hello_GLSL","Apprendre/WebGL/Par_exemple/Générer_des_textures_avec_du_code")}}

Avec cet exemple, on voit comment combiner la programmation des _shaders_ et les interactions utilisateurs grâce aux attributs des _vertex_.

{{EmbedLiveSample("Un_Hello_World_en_GLSL",660,425)}}

### Un _Hello World_ en GLSL

Voici comment envoyer des données saisies à un programme de manipulation des _shaders_ en utilisant la mémoire GPU.

```html hidden
<p>
  Voici le premier exemple où on manipule des attributs et où on envoie des
  données au GPU. Cliquez sur le canevas pour modifier la position horizontale
  du carré.
</p>
<canvas
  >Il semblerait que votre navigateur ne supporte pas l'élément HTML5
  canvas.</canvas
>
```

```css hidden
body {
  text-align: center;
}
canvas {
  width: 280px;
  height: 210px;
  margin: auto;
  padding: 0;
  border: none;
  background-color: black;
}
button {
  display: block;
  font-size: inherit;
  margin: auto;
  padding: 0.6em;
}
```

```html
<script type="x-shader/x-vertex" id="vertex-shader">
  #version 100
  precision highp float;

  attribute float position;

  void main() {
    gl_Position = vec4(position, 0.0, 0.0, 1.0);
    gl_PointSize = 64.0;
  }
</script>
```

```html
<script type="x-shader/x-fragment" id="fragment-shader">
  #version 100
  precision mediump float;
  void main() {
    gl_FragColor = vec4(0.18, 0.54, 0.34, 1.0);
  }
</script>
```

```js hidden
;(function(){
```

```js
"use strict";
window.addEventListener("load", setupWebGL, false);
var gl, program;
function setupWebGL(evt) {
  window.removeEventListener(evt.type, setupWebGL, false);
  if (!(gl = getRenderingContext())) return;

  var source = document.querySelector("#vertex-shader").innerHTML;
  var vertexShader = gl.createShader(gl.VERTEX_SHADER);
  gl.shaderSource(vertexShader, source);
  gl.compileShader(vertexShader);
  source = document.querySelector("#fragment-shader").innerHTML;
  var fragmentShader = gl.createShader(gl.FRAGMENT_SHADER);
  gl.shaderSource(fragmentShader, source);
  gl.compileShader(fragmentShader);
  program = gl.createProgram();
  gl.attachShader(program, vertexShader);
  gl.attachShader(program, fragmentShader);
  gl.linkProgram(program);
  gl.detachShader(program, vertexShader);
  gl.detachShader(program, fragmentShader);
  gl.deleteShader(vertexShader);
  gl.deleteShader(fragmentShader);
  if (!gl.getProgramParameter(program, gl.LINK_STATUS)) {
    var linkErrLog = gl.getProgramInfoLog(program);
    cleanup();
    document.querySelector("p").innerHTML =
      "Shader program did not link successfully. " + "Error log: " + linkErrLog;
    return;
  }

  initializeAttributes();
  gl.useProgram(program);
  gl.drawArrays(gl.POINTS, 0, 1);

  document.querySelector("canvas").addEventListener(
    "click",
    function (evt) {
      var clickXrelativToCanvas = evt.pageX - evt.target.offsetLeft;
      var clickXinWebGLCoords =
        (2.0 * (clickXrelativToCanvas - gl.drawingBufferWidth / 2)) /
        gl.drawingBufferWidth;
      gl.bufferData(
        gl.ARRAY_BUFFER,
        new Float32Array([clickXinWebGLCoords]),
        gl.STATIC_DRAW,
      );
      gl.drawArrays(gl.POINTS, 0, 1);
    },
    false,
  );
}

var buffer;
function initializeAttributes() {
  gl.enableVertexAttribArray(0);
  buffer = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([0.0]), gl.STATIC_DRAW);
  gl.vertexAttribPointer(0, 1, gl.FLOAT, false, 0, 0);
}

window.addEventListener("beforeunload", cleanup, true);
function cleanup() {
  gl.useProgram(null);
  if (buffer) gl.deleteBuffer(buffer);
  if (program) gl.deleteProgram(program);
}
```

```js hidden
function getRenderingContext() {
  var canvas = document.querySelector("canvas");
  canvas.width = canvas.clientWidth;
  canvas.height = canvas.clientHeight;
  var gl =
    canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
  if (!gl) {
    var paragraph = document.querySelector("p");
    paragraph.innerHTML =
      "Failed to get WebGL context." +
      "Your browser or device may not support WebGL.";
    return null;
  }
  gl.viewport(0, 0, gl.drawingBufferWidth, gl.drawingBufferHeight);
  gl.clearColor(0.0, 0.0, 0.0, 1.0);
  gl.clear(gl.COLOR_BUFFER_BIT);
  return gl;
}
```

```js hidden
})();
```

Le code source de cet exemple est également disponible sur [GitHub](https://github.com/idofilin/webgl-by-example/tree/master/hello-vertex-attributes).

{{PreviousNext("Apprendre/WebGL/Par_exemple/Hello_GLSL","Apprendre/WebGL/Par_exemple/Générer_des_textures_avec_du_code")}}
