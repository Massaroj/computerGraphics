========================================================
                        README
========================================================
	Author: Jacob Massaro

========================================================
                     What it Does
========================================================
	This code makes a background by cubemapping textures.
It then applies a shader to a simple cube that reflects the
enviornment on the cube.

========================================================
                         Code
========================================================

--------------------------Vertex (Lines: 11-34)-------------------------------

    <script id="vertexShader" type="x-shader/x-vertex">
    precision highp float;

    attribute vec3 position;
    attribute vec3 normal;

    uniform mat4 viewMatrix;
    uniform mat4 modelViewMatrix;
    uniform mat4 projectionMatrix;

    varying vec3 vPositionEye;
    varying vec3 vNormalEye;

    void main()
    {
      //Get the eye position vector
      vPositionEye = vec3(modelViewMatrix * vec4(position, 1.0));

      //Get the normal eye vector
      vNormalEye = vec3(modelViewMatrix * vec4(normal, 0.0));

      gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
    }
    </script>

--------------------------Fragment(Lines: 36-61)-------------------------------

<script id="fragmentShader" type="x-shader/x-fragment">
    precision highp float;

    uniform samplerCube cubemap;
    uniform mat4 viewMatrix;

    varying vec3 vPositionEye;
    varying vec3 vNormalEye;

    void main()
    {
      //Make the incident and normal vectors
      vec3 incident = normalize(vPositionEye);
      vec3 normal = normalize(vNormalEye);

      //Convert from eye to world space
      vec3 reflected = reflect(incident, normal);
      mat3 vM = mat3(viewMatrix);
      vec3 RInWorldspace = vec3(-dot(vM[0],reflected),dot(vM[1],reflected),dot(vM[2],reflected));

      //Get the environment color
      vec3 envMapColor = textureCube(cubemap, RInWorldspace).rgb;

      gl_FragColor = vec4(envMapColor, reflected);
    }
    </script>

-------------------------------Shader Declaration(Lines: 89-98)---------------

let Custom = new THREE.RawShaderMaterial
        ({
          side: THREE.DoubleSide,
          fragmentShader: document.getElementById('fragmentShader').textContent,
          vertexShader: document.getElementById('vertexShader').textContent,
          uniforms:
          {
            "cubemap" :{type: "t", value: texture},
          }
        });
