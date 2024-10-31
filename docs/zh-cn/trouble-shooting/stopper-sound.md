# Stopper没有声音

自制地图中的Stopper即使正确归组后，仍然没有声音的问题，主要是由于Ballance的一个Bug导致的。由于Ballance原版脚本编写的失误，只有位于`Phys_FloorStopper`组中的第一个物体才会发出声音。

所以为了让地图中所有Stopper都有声音，解决方案是在地图发布前将所有Stopper合并成一个物体（建议在地图发布前做是因为合并了后的Stopper，如果想再分别移动，操作上会显得比较麻烦，而且还可能会误操作），即在Blender中选中所有Stopper然后`Ctrl + J`即可。