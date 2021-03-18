# CS425 - Computer Graphics I (Spring 2021) -Andrea Herrera (aherre57)

## Assignment 1: Triangle meshes rendering
The goal of this assignment is to get you familiar with transformations, and triangle mesh rendering. You will develop an application to render an urban setting described in an external JSON file that must be uploaded by the user through a configuration panel. The JSON file has four layers describing the elements and color of buildings, parks, water and surface of a particular region (see below for a complete description of the file). You should use a unique buffer and VAO for *each* layer.
# Run Program
Run python -m SimpleHTTPServer or python3 -m http.server to create a http://localhost:8000/

# CODE implemented

index.html

Created a configuration panel with four components: 
1) One [slider]
2) One [slider]
3) A [dropdown]
4) A file [input] Upload JSON

gl.js 

Four main classes That were updated:
- `FlatProgram`: handles shading of flat layers (water, parks, surface). inside the constructor set attrib and uniform locations.

- `BuildingProgram`: handles shading of building layer. This layer contains normals. inside the constructor set attrib and uniform locations including normal. 

- `Layer`: handels flat layers. inside the init(), created program, set vertex, and index buffers, vao. inside draw(), used program update (model matrix, view matrix, projection matrix), set uniforms, bind vao and draw elements

- `BuildingLayer`: handles  building layer. inside the init(), created program, set vertex, normal and index buffers, vao. inside draw(), used program update (model matrix, view matrix, projection matrix), set uniforms, bind vao and draw elements

- `Layers`: (collection of layers) Not Changed 

Functions that were updates from the riginal skeleton code:
- `window.handleFile` function so that it properly parses the JSON FILE, and adds the appropriate layer to the layers dictionary. through the for loop and switchcase provided by the skeleton code 
inorder to access all arrays we parsed through the JSON FILE. 
To add the layers from the respective water, parks or sufaces:                     
layers.addLayer(layer, parsed[layer].coordinates, parsed[layer].indices,parsed[layer].color);

To add the buildingLayer:
layers.addBuildingLayer(layer, parsed[layer].coordinates, parsed[layer].indices,parsed[layer].normals,parsed[layer].color);

    The JSON will be in the following format:
    {
    'buildings': 
    {
        'coordinates': [x_1,y_1,z_1,x_2,y_2,z_2,...,x_n,y_n,z_n],
        'indices': [i_1,i_2,...,i_n],
        'normals': [x_1,y_1,z_1,x_2,y_2,z_2,...,x_n,y_n,z_n],
        'color': [r,g,b,a]
    },
    'water': 
    {
        'coordinates': [x_1,y_1,z_1,x_2,y_2,z_2,...,x_n,y_n,z_n],
        'indices': [i_1,i_2,...,i_n],
        'color': [r,g,b,a]
    },
    'parks': 
    {
        'coordinates': [x_1,y_1,z_1,x_2,y_2,z_2,...,x_n,y_n,z_n],
        'indices': [i_1,i_2,...,i_n],
        'color': [r,g,b,a]
    },
    'surface':
    {
        'coordinates': [x_1,y_1,z_1,x_2,y_2,z_2,...,x_n,y_n,z_n],
        'indices': [i_1,i_2,...,i_n],
        'color': [r,g,b,a]
    },
}



For the following functions code from LAB 3 was used.

- `updateModelMatrix` :when the user changes the value of slider (2), the camera rotates around the centerpoint of the layers.
- `updateProjectionMatrix`: two types of projections (orthographic and perspective were implemented using the dropdown functionality from the drop down menu
- `updateViewMatrix`: when the user changes the value of slider (2), the camera rotates around the centerpoint of the layers.

*.vert.js: vertex shaders files
    //set color as the dot product between a light direction, and the vertex normal
    vColor = uColor;
    //& transform position
    gl_Position = uProjection * uView * uModel * vec4(position, 1);


*.frag.js: fragment shaders files
    //set color 
    outColor = vColor;
# GitHub Classroom
git is a version control system, designed to help developers track different versions of your code, synchronize them across different machines, and collaborate with others. Follow the instructions here to install git on your computer. GitHub is a website that supports git as a service. This a nice tutorial on how to get started with git and GitHub.

Use git clone to get a local copy of the newly created repository. After writing your code, you can push your modifications to the server using git commit followed by git push. For example, if your username is uic-user:

git clone git@github.com:uic-cs425/assignment-1-uic-user.git
touch index.html
git add index.html
git commit -am "index.html file"
git push