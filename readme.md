# Breath of wife Assets Dumping Guide
## principle
* 0x1 Load all assets into memory
* 0x2 Get assets name and file size through `AssetBundleFileSystem`
* 0x3 Access file content with `File::Read`

## 0x1 
* Hook `GameAssembly.dll!MoleMole::AssetBundleExternalResourceProvider::Tick`
Get `AssetBundleExternalResourceProvider` instance through its first argument `this`
its a main thread function, we should call loadAsset in main thread

* enumrate bundlehash through `AssetBundleExternalResourceProvider.ResourceIndex`

* foreach bundlehash call `GameAssembly.dll!MoleMole::AssetBundleExternalResourceProvider::SyncLoadBundle` in main thread

## 0x2
* enumrate loaded assets through `AssetBundleFileSystem.ArchiveStorge`. Its a multimap object with the RBTree structure.

## 0x3
* foreach loaded assets, add a "archive:/" to it. then call `unityplayer.dll!File::Open` then `unityplayer.dll!File::Read` then `unityplayer.dll!File::Close`

## python script with function and structure offset here:
https://gist.github.com/MoePus/fb6e27e7c58be9fba2d35202921486d8

### CC-BY-NC-SA
