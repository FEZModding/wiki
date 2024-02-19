# Trixel Art Specification

For [Art Objects](/wiki/content/formats/fezao) and [Trile Sets](/wiki/content/formats/fezts), FEZ uses a special type of 3D geometry called **Trixel Art**. It is similar to voxel art in that it produces a mesh made out of smaller cubes - in voxel art, they're just named voxels. However, unlike voxel art, trixel art uses cubemap projection for texture unwrapping. This means that the same trixel can have different colors on each side. However, a trade-off is that all trixel faces along certain direction will always have the same color.

Compiled and triangulated trixel art model is essentially a regular textured 3D model, with some key differences:

- UV texture projection is predetermined by the cubemap algorithm.
- Normal vectors of each face is locked to one of six cardinal directions.

## Cubemap projection

The cubemap is made of six images with equal size arranged horizontally, each representing a different side of a cubemap in a following order: front, right, back, left, top and bottom. The game uses vertex normal vector to determine which side of a cubemap to use, and then projects vertex position onto the corresponding wall of a trixel art's bounding box to calculate texture coordinates. For triles, the size of a bounding box is always 1x1x1, but for art objects it may be bigger. It's worth noting that, in order to keep the trixel size uniform on each face, the bounding box size is equal on each side.

To better illustrate the process of cubemap projection, here's an example cubemap texture of a model:

![ao1.png](/wiki/assets/images/ao/ao1.png)

Here's an image of a geometry which uses this cubemap texture:

![ao2.png](/wiki/assets/images/ao/ao2.png)

Boundaries of this art objects are defined as [4,4,4]. You can imagine a cubemap being a cube with such dimensions extending from origin:

![ao3.png](/wiki/assets/images/ao/ao3.png)

This cubemap is then projected on top of the geometry. Notice how faces which are behind other faces along their normal vector have the same texture (like the grass) as a result of the projection:

![ao4.png](/wiki/assets/images/ao/ao4.png)

For those who bothered looking into this wiki page, here's an Art Object of Suzanne the monkey in Villageville as a reward:

![monke.png](/wiki/assets/images/ao/monke.png)

## Resources

- First Renaud's article on trixels : <http://theinstructionlimit.com/behind-fez-trixels-and-why-we-dont-just-say-voxels>
- Second Renaud's article on trixels : <http://theinstructionlimit.com/behind-fez-trixels-part-two>
