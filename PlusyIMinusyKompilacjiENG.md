# The advantages and disadvantages of compiling programs

## Wrong compilation flags
Starting the adventure of creating programs from sources, we can often copy compilation commands with no explanation of what specific flags are doing.  
When compiling, we can use too "specialized" or simply wrong settings, which will result in a program with reduced performance or containing a huge number of additional features that would only distract us.

![S](https://user-images.githubusercontent.com/41945903/85174478-c1c43300-b275-11ea-9124-eb81835151c9.png)

## Better error descriptions
Often happens that programs that we download because of their smaller size are trimmed from debug symbols and/or have disabled options to help us collect information about errors in the application.  
By compiling the program itself, we can get much more detailed information, e.g. about the exact place where the program has been crashed.

Example of backtrace with Godot Engine without debugging symbols:
```
[1] /lib/x86_64-linux-gnu/libc.so.6(+0x43f60) [0x7f39d24fbf60] (??:0)
[2] /home/user/Godot_v3.2.1-stable_x11.64() [0xbfa51f] (??:?)
[3] /home/user/Godot_v3.2.1-stable_x11.64() [0x1de1d0a] (??:?)
[4] /home/user/Godot_v3.2.1-stable_x11.64() [0x1dd1347] (??:?)
[5] /home/user/Godot_v3.2.1-stable_x11.64() [0x219367e] (:?)
[6] /home/user/Godot_v3.2.1-stable_x11.64() [0x2196a90] (??:?)
[7] /home/user/Godot_v3.2.1-stable_x11.64() [0x219a787] (:?)
[8] /home/user/Godot_v3.2.1-stable_x11.64() [0x219b8ce] (:?)
[9] /home/user/Godot_v3.2.1-stable_x11.64() [0xbc8274] (??:?)
```
and with:
```
[1] /lib/x86_64-linux-gnu/libc.so.6(+0x43f60) [0x7fbb086b6f60] (??:0)
[2] String::parse_utf8(char const*, int) (/godot/core/ustring.cpp:1473)
[3] EditorSceneImporterGLTF::_parse_json(String const&, EditorSceneImporterGLTF::GLTFState&) (/godot/editor/import/editor_scene_importer_gltf.cpp:69)
[4] EditorSceneImporterGLTF::import_scene(String const&, unsigned int, int, List<String, DefaultAllocator>*, Error*) (/godot/editor/import/editor_scene_importer_gltf.cpp:2987)
[5] ResourceImporterScene::import(String const&, String const&, Map<StringName, Variant, Comparator<StringName>, DefaultAllocator> const&, List<String, DefaultAllocator>*, List<String, DefaultAllocator>*, Variant*) (/godot/editor/import/resource_importer_scene.cpp:1322)
[6] EditorFileSystem::_reimport_file(String const&) (/godot/editor/editor_file_system.cpp:1797)
[7] EditorFileSystem::reimport_files(Vector<String> const&) (/godot/editor/editor_file_system.cpp:1993 (discriminator 3))
[8] EditorFileSystem::_update_scan_actions() (/godot/editor/editor_file_system.cpp:591)
[9] EditorFileSystem::_notification(int) (/godot/editor/editor_file_system.cpp:1174)
```

## System jamming
If we want to recompile the program, we usually need a bit of free time (different depending on the size of the project and the tools used), as well as various packages that our application uses.  
Their installation, not only is often quite complicated (due to the requirements of specific versions), but also often is not used by any other application.  
If we already stop compiling a given program or the required dependencies change in the meantime, their old versions, if we don't remove them ourselves, will start to consume our disk space and sometimes resources such as CPU time or RAM.

![S](https://user-images.githubusercontent.com/41945903/85174490-c688e700-b275-11ea-8b4b-08f70bb029d1.png)

## Safety
One of the main arguments raised in the security discussion between Open Source and commercial software is that in first we can easily browse source code.  
When compiling such code ourselves, we can be sure that no one (e.g. in the installer) has added something like viruses or keyloggers to end app.

## The ability to customize the program
When compiling a program ourselves, we are not forced to use only official versions of the program prepared by the creators.  
We can make modifications, e.g. activate flags which will increase the overall performance of the program, which were disabled e.g. because of the need to ensure compatibility with older devices/systems.  
Additionally, in many programs we can enable hidden functions that are still in experimental form.  
Knowing a little bit about programming, we can fix some of the errors that affect us or silence annoying warnings.


![S](https://user-images.githubusercontent.com/41945903/85174698-2a131480-b276-11ea-9061-b71f7b75d0b1.png)
 
## Waste of time
It can happens that if you are stuck in a moment or tempted by other people with potential benefits, you can try to compile the program yourself.  
Often however, it may turn out that a version of the application prepared earlier by the developers, will be a smaller and faster program without unnecessary debugging symbols which will provide a number of unknown to us optimizations (for example by selected compilation flags).

![S](https://user-images.githubusercontent.com/41945903/85174500-c983d780-b275-11ea-9b4a-9336755f7297.png)

## Getting security patches and new features
Usually, the time between creating and including a patch in the repository and delivering it to the user is very different and ranges from a few hours to even several years depending on how the authors treat creating a new version of app.  
However this is cause why users compile programs on their own to take advantage of the latest bug fixes or features, even though the author has not yet released the official binary.  
Additionally, we can compile and test various forks and PRs of new features/fixed bugs even though they are not yet included in a given repository.

[S](https://user-images.githubusercontent.com/41945903/85174510-cbe63180-b275-11ea-8941-67b6ffb7d6f2.png)

## Better bug reports
If we noticed an incorrect operation of the function, which worked correctly in earlier versions of the program, we should include in the bug report information between which versions the bug occurs.  
However, it often happens that subsequent versions of the program are divided by several dozen, several hundred or even several thousand commits, so it is very difficult to find a specific commit that caused the bug.  
In order to speed up fixing of the bug (from experience it's usually speed up ten times), it would be best to indicate a specific commit that caused the wrong behavior.  
For such things, the bisect tool available in the git is very useful, which, moving through history, allows you to treat specific commits as those in which the error occurs or those in which there is no error, so you can point out which changes caused the errors and fix them much faster.


![S](https://user-images.githubusercontent.com/41945903/85174515-cee12200-b275-11ea-86f6-5e7310eae6ee.png)

