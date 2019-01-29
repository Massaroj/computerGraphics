===================================================
		Author: Jacob Massaro
		File: Assignment 3
===================================================

===================================================
			Overview
===================================================

In this assignment I made shader code that randomizes the rgb values. I applied
this shadder to all three cubes in the scene. After I place a cube in the scene,
I would set newMTL equal to a new THREE.RawShaderMaterial so it would randomize
the values. I placed three cubs in the scene on a black plane.

====================================================
		   Shader code
====================================================

        let newMTL = new THREE.RawShaderMaterial({
            side: THREE.DoubleSide,
            fragmentShader: document.getElementById('fragmentShader').textContent,
            vertexShader: document.getElementById('vertexShader').textContent,
            uniforms:
            {
              r: {type: "f", value: Math.random()},
              g: {type: "f", value: Math.random()},
              b: {type: "f", value: Math.random()},
            }
          });

======================================================
		   Code Location
======================================================
- Created in Assignment3.html
- vertexShader (Lines 11-27)
- fragmentShader (Lines 30-41)
- Shader function (Lines 58-68)
- Used on three cubes (Line 81, Line 99, and Line 117; respectively)