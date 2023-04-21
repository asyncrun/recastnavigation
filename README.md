
Recast & Detour
===============

[![Build](https://github.com/recastnavigation/recastnavigation/actions/workflows/Build.yaml/badge.svg)](https://github.com/recastnavigation/recastnavigation/actions/workflows/Build.yaml)
[![Tests](https://github.com/recastnavigation/recastnavigation/actions/workflows/Tests.yaml/badge.svg)](https://github.com/recastnavigation/recastnavigation/actions/workflows/Tests.yaml)

![screenshot of a navmesh baked with the sample program](/Docs/Images/screenshot.png)

## Recast

Recast is state of the art navigation mesh construction toolset for games.

Recast是最先进的游戏导航网格构建工具集

Recast is...
* 🤖 **Automatic** - throw any level geometry at it and you will get a robust navmesh out
* 输入一个关卡几何体，输出一个健壮的导航网格
* 🏎️ **Fast** - swift turnaround times for level designers
* 节约关卡设计师的时间
* 🧘 **Flexible** - easily customize the navmesh generation and runtime navigation systems to suit your specific game's needs.
* 简单的就可以实现自定义导航网格生成，且可以更好的满足你游戏对运行时导航系统的需求

Recast constructs a navmesh through a multi-step rasterization process:

Recast通过多个步骤栅格化处理构建导航网格

1. First Recast voxelizes the input triangle mesh by rasterizing the triangles into a multi-layer heightfield. 
2. Voxels in areas where the character would not be able to move are removed by applying simple voxel data filters.
3. The walkable areas described by the voxel grid are then divided into sets of 2D polygonal regions.
4. The navigation polygons are generated by triangulating and stiching together the generated 2d plygonal regions.


1. 首先，Recast通过栅格化三角形为多层高度场的方式，将输入的三角形网格体素化
2. 角色不能行走的区域，使用体素数据过滤，将被去除掉
3. 可行走区域的体素被划分到由2D多边形区域组成的集合中
4. 通过对2D多边形区域的三角化和缝合，来生成导航多边形

## Detour

Recast is accompanied by Detour, a path-finding and spatial reasoning toolkit. You can use any navigation mesh with Detour, but of course the data generated with Recast fits perfectly.

Recast 是包含Detour、寻路和空间推理工具集，可以使用任何Detour生成的导航网格，前提是生成的数据适合Recast处理

Detour offers a simple static navmesh data representation which is suitable for many simple cases.  It also provides a tiled navigation mesh representation, which allows you to stream of navigation data in and out as the player progresses through the world and regenerate sections of the navmesh data as the world changes.

Detour 提供一种简单的静态导航网格，非常适合一些简单的使用场景，除此之外，还提供了动态导航网格，使导航数据流化处理，当玩家视野的变化，场景发生变化时，同步生成区域的导航网格数据

## RecastDemo

You can find a comprehensive demo project in the `RecastDemo` folder. It's a kitchen sink demo showcasing all the functionality of the library. If you are new to Recast & Detour, check out [Sample_SoloMesh.cpp](/RecastDemo/Source/Sample_SoloMesh.cpp) to get started with building navmeshes and [NavMeshTesterTool.cpp](/RecastDemo/Source/NavMeshTesterTool.cpp) to see how Detour can be used to find paths.

### Building RecastDemo

RecastDemo uses [premake5](http://premake.github.io/) to build platform specific projects. Download it and make sure it's available on your path, or specify the path to it.

#### Linux

- Install SDL2 and its dependencies according to your distro's guidelines.
- Navigate to the `RecastDemo` folder and run `premake5 gmake2`
- Navigate to `RecastDemo/Build/gmake2` and run `make`
- Navigate to `RecastDemo/Bin` and run `./RecastDemo`

#### macOS

- Grab the latest SDL2 development library dmg from [here](https://github.com/libsdl-org/SDL) and place `SDL2.framework` in `RecastDemo/Bin`
- Navigate to the `RecastDemo` folder and run `premake5 xcode4`
- Open `Build/xcode4/recastnavigation.xcworkspace`
- Set the RecastDemo project as the target and build.

#### Windows

- Grab the latest SDL2 development library release from [here](https://github.com/libsdl-org/SDL) and unzip it `RecastDemo\Contrib`.  Rename the SDL folder such that the path `RecastDemo\Contrib\SDL\lib\x86` is valid.
- Navigate to the `RecastDemo` folder and run `premake5 vs2022`
- Open `Build/vs2022/recastnavigation.sln`.
- Set `RecastDemo` as the startup project, build, and run.

### Running Unit tests

- Follow the instructions to build RecastDemo above.  Premake should generate another build target called "Tests".
- Build the "Tests" project.  This will generate an executable named "Tests" in `RecastDemo/Bin/`
- Run the "Tests" executable.  It will execute all the unit tests, indicate those that failed, and display a count of those that succeeded.

## Integrating with your game or engine

It is recommended to add the source directories `DebugUtils`, `Detour`, `DetourCrowd`, `DetourTileCache`, and `Recast` into your own project depending on which parts of the project you need. For example your level building tool could include `DebugUtils`, `Recast`, and `Detour`, and your game runtime could just include `Detour`.

### Install through vcpkg

If you are using the [vcpkg](https://github.com/Microsoft/vcpkg/) dependency manager you can download and install Recast with:

```
vcpkg install recast
```

## Contribute

Check out the [Project Roadmap](Roadmap.md) to see what features and functionality you might be able to help with, and the [Contributing doc](CONTRIBUTING.md) for guidance on making contributions.

## Discuss

- Discuss Recast & Detour: http://groups.google.com/group/recastnavigation
- Development blog: http://digestingduck.blogspot.com/

## License

Recast & Detour is licensed under ZLib license, see License.txt for more information.
