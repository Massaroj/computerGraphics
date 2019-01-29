========================================================
                        README
========================================================
	Author: Jacob Massaro

========================================================
                     What it Does
========================================================
	This code has a simple cube in it with a stone
texturing applied. There is also a Lambert Shader applied
to the cube as well.

========================================================
                         Code
========================================================

--------------------------Vertex (Lines: 11-31)-------------------------------
<script id="vertexShader" type="x-shader/x-vertex">
    precision highp float;

    attribute vec3 position;
    attribute vec3 normal;
    attribute vec2 uv;

    uniform mat4 modelViewMatrix;
    uniform mat4 projectionMatrix;
    uniform mat3 normalMatrix;

    varying vec2 vUV;
    varying vec3 vNormal;

    void main()
    {
      vUV = uv;
      vNormal = normalMatrix * normal;
      gl_Position = projectionMatrix * modelViewMatrix * vec4(position,1);
    }
    </script>

--------------------------Fragment(Lines: 33-58)-------------------------------

<script id="fragmentShader" type="x-shader/x-fragment">
    precision highp float;

    uniform sampler2D tex;
    uniform vec3 light;

    varying vec3 vNormal;
    varying vec2 vUV;

    void main()
    {
      //Take the dot of the normal vector and the light vector
      float lightDotProduct = dot(normalize(vNormal), light );

      //Use that scalar to get the brightness (we max it in case lightDot is < 0)
      float surfaceBrightness = max( 0.0, lightDotProduct );

      //Our texturing
      vec3 color = texture2D(tex, vUV).rgb;

      //Result of brightness with the color of the texture
      vec3 lambResult = color*surfaceBrightness;

      gl_FragColor = vec4(lambResult, 1.0);
    }
    </script>

-------------------------------Shader Declaration(Lines: 75-89)---------------

        let texture = new THREE.TextureLoader().load("stone.jpg");
        texture.wrapS= THREE.RepeatWrapping;
        texture.wrapT= THREE.RepeatWrapping;

        let Custom = new THREE.RawShaderMaterial
        ({
          side: THREE.DoubleSide,
          fragmentShader: document.getElementById('fragmentShader').textContent,
          vertexShader: document.getElementById('vertexShader').textContent,
          uniforms:
          {
            "tex" :{type: "t", value: texture},
            "light" :{type: "vec3", value: new THREE.Vector3(0.8,0.8,1.0)},
          }
        });
