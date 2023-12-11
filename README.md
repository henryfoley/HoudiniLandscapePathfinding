# Pathfinding Across Terrain Using Houdini

# STILL A WORK IN PROGRESS

## Description

### Goal
The goal of this project is to generate the shortest possible path between two points on a generated landscape. This would allow for fast and dynamic road generation that would follow the terrain.

### Algorithm
1.) Generate Heightfield: By using Houdini’s native heightfield generation, I first create a landscape using a noise

2.) Convert to 2D Plane: The terrain is then converted into a grid mesh and flattened to a 2D plane. Resolution of A* algorithm can be changed by adjusting the subdivisions of procedural landscape mesh

3.) Assign Weights: The height value of the terrain is stored in a point attribute as a -1 to 1 value. The weight value of the terrain can then be later changed to emphasize traversal over higher/lower terrain

4.) User Picks Points: The user picks two points on the 2D plane from which the path will be generated between

5.) A* Pathfinding: Using the weights and a distance traveled cost, the algorithm then finds the shortest distance between the two points

6.) Draw Mesh: The line is smoothed to reduce the sharp turns of the grid. A sweep mesh is then created from the generated path to represent the algorithms result

## Result

![ezgif com-video-to-gif (1)](https://github.com/henryfoley/HoudiniLandscapePathfinding/assets/100539264/d8c2af41-37ae-4483-9fcb-e4317097f572)

## Challenges
### Data Structures
Originally my goal was to implement the A* Algorithm in Houdini from scratch. One of the most glaring challenges that I encountered was the lack of Houdini’s advanced data structures. In order to implement A* properly you need to use the Priority Queue data structure, of which is not in Houdini. After doing some research online I found a potential workaround. Houdini’s Sort node allows you to order points based on a given attribute. Initially this did seem to work as it allowed me to prioritize points with a better weight.

The problem with this approach lies in how the sort node affects the meshes properties. When organizing the points by priority, it swapped their indexes on the procedurally generated mesh. The operation outputted a path that did follow the algorithm's point order, but did not correspond with the original meshes point order, resulting in a generated path that was not following the correct path.

### Overscoping
Frankly I committed much more time to trying to implement the algorithm from scratch when I could have just used a native Houdini node. The results shown here were created using the original approach that I decided to avoid earlier. There was no functionality that I needed to use that wasn’t in the native node and I ended up spending close to 15 hours on a system that I ended up scrapping.

## Application
### Game Application
The primary application of this tool is for large world generation. Game genres that would benefit from using this tool are Racing and Open World games. Procedural tools like this one speed up the rate of development.

### Platform
Whilst this tool is currently only used in Houdini, using Houdini Engine I will be able to utilize it in game engines like Unity and Unreal. The tool is also able to be combined with other tools to improve the final generated result.

## Future Development
### Anisotropic A*
Using an Anisotropic grid I would be able to factor in more neighboring points. The more points I factor into the algorithm the lower the performance gets, but the higher the accuracy. To implement this I would have to use Python within Houdini, which is something that I still need to learn.

### Expanded World Generation
As mentioned earlier, this tool can be combined with other tools to add more functionality. Some ideas for potential improvements include adding landscape terraforming from the generated path, generating a road mesh from the path, and scattering objects along the edge of the path. The system could also be used with a more expanded terrain generation tool.

## References
Galin, Eric & Peytavie, Adrien & Maréchal, Nicolas & Guérin, Eric. (2010). Procedural Generation of Roads. Computer Graphics Forum. 29. 429 - 438. 10.1111/j.1467-8659.2009.01612.x.

“Ghost Recon Wildlands Terrain Tools and Technology.” YouTube, YouTube, 16 May 2017, https://www.youtube.com/watch?v=kzthHcbG9IM. Accessed 10 Dec. 2023. 

Red Blob Games. Implementation of A*, www.redblobgames.com/pathfinding/a-star/implementation.html. Accessed 10 Dec. 2023. 
