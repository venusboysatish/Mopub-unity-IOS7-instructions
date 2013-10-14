Mopub-unity-IOS7-instructions
=============================

MoPub IOS7 integration. Instructions and bug fixes:

Note : these instructions deal with only the XCode part of building an unity game with Mopub, for the Unity side of importing
the assets, and setting up the project, please refer to this-> https://github.com/mopub/mopub-unity-ios-plugin

A)	Add the following frameworks. These Frameworks can be found at (/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.1.sdk/System/Library/Frameworks/)
	1. AdSupport.framework
	2. StoreKit.framework
	3. CoreTelephony.framework
	4. EventKitUI.framework
	5. EventKit.framework

B)	Add the entire MoPubSDK folder to the Classes Folder. Do this by right-clicking on the Classes folder and selecting "Add Files to …"
	Also add, MoPubBinding.m, MoPubBinding.h, MoPubManager.mm from mopub-unity-ios-plugin-master folder

C) 	Go to Build Settings. Under Apple LLVM compiler 4.2 - Language settings, change the "Enable Objective-C Exceptions" to Yes

D)	In Build Settings, update the Code Signing section appropriately

E)	In Build Settings, under Linking section, expand the Other Linker Flags drop down, and append "-ObjC" to the existing strings for Debug and Release

F)	Incase of Linker errors, add this to the "Library Search Paths" under "Search Paths" section
/Volumes/Projects/Satish/MegaDriver/IOSBuild/MegaDriver_02/Classes/MoPubSDK/AdNetworkSupport/Millennial/SDK /Volumes/Projects/Satish/MegaDriver/IOSBuild/MegaDriver_02/Libraries

G)	Ior IOS7, OS status bar comes on top of your game, fix -
under 
@implementation UnityViewController
of iPhone_View.mm in Classes folder, add the following
- (BOOL)prefersStatusBarHidden
{
    return YES;
}

H) fix for this error:
Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[__NSCFDictionary setObject:forKey:]: attempt to insert nil value (key: WebKitLocalStorageDatabasePathPreferenceKey)'

go to MPHTMLBannerCustomEvent.m and at "self.bannerAgent = …" line, add a breakpoint, set Condition as NSInvalidArgumentException, then Enable, "Automatically continue after evaluating", and then(optional) set Action to "Log Message" and put "NSInvalidArgumentException averted" in the text box.
