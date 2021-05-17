# Prebuilt V8 8.9.255.24 for Android (armeabi-v7a, arm64-v8a, x86 and x86_64)

Documentation: https://v8.dev/docs


```
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

Add `export PATH=/path/to/depot_tools:$PATH` to `~/.bashrc` and run `source ~/.bashrc`


```
mkdir ~/v8
cd ~/v8
fetch v8
cd v8

# Choose v8_version from https://omahaproxy.appspot.com/
git checkout tags/8.9.255.24

gclient sync

# For linux only:
./build/install-build-deps.sh

# Make sure that x64 release can be compiled:
gm x64.release
```

Add `target_os = ['android']` to `~/v8/.gclient`

Run `gclient sync` to download all dependencies.

##arm

```
gn gen out.gn/arm.release --args='host_cpu="x64" is_clang=true is_component_build=false is_debug=false is_official_build=true strip_debug_info=true symbol_level=0 target_cpu="arm" target_os="android" treat_warnings_as_errors=false v8_enable_i18n_support=false v8_enable_verify_heap=true v8_target_cpu="arm" v8_use_external_startup_data=false use_thin_lto=false use_glib=false use_custom_libcxx=false v8_static_library=true enable_resource_allowlist_generation=false v8_monolithic=true arm_use_neon=false'

ninja -C out.gn/arm.release v8_monolith
```

##arm64

```
gn gen out.gn/arm64.release --args='host_cpu="x64" is_clang=true is_component_build=false is_debug=false is_official_build=true strip_debug_info=true symbol_level=0 target_cpu="arm64" target_os="android" treat_warnings_as_errors=false v8_enable_i18n_support=false v8_enable_verify_heap=true v8_target_cpu="arm64" v8_use_external_startup_data=false use_thin_lto=false use_glib=false use_custom_libcxx=false v8_static_library=true enable_resource_allowlist_generation=false v8_monolithic=true'

ninja -C out.gn/arm64.release v8_monolith
```

##x86

```
gn gen out.gn/x86.release --args='host_cpu="x64" is_clang=true is_component_build=false is_debug=false is_official_build=true strip_debug_info=true symbol_level=0 target_cpu="x86" target_os="android" treat_warnings_as_errors=false v8_enable_i18n_support=false v8_enable_verify_heap=true v8_target_cpu="x86" v8_use_external_startup_data=false use_thin_lto=false use_glib=false use_custom_libcxx=false v8_static_library=true enable_resource_allowlist_generation=false v8_monolithic=true'

ninja -C out.gn/x86.release v8_monolith
```

##x64

```
gn gen out.gn/x64.release --args='host_cpu="x64" is_clang=true is_component_build=false is_debug=false is_official_build=true strip_debug_info=true symbol_level=0 target_cpu="x64" target_os="android" treat_warnings_as_errors=false v8_enable_i18n_support=false v8_enable_verify_heap=true v8_target_cpu="x64" v8_use_external_startup_data=false use_thin_lto=false use_glib=false use_custom_libcxx=false v8_static_library=true enable_resource_allowlist_generation=false v8_monolithic=true'

ninja -C out.gn/x64.release v8_monolith
```

```
cp ./out.gn/arm.release/obj/libv8_monolith.a ~/prebuilt-v8-android/libs/armeabi-v7a/libv8.a
cp ./out.gn/arm64.release/obj/libv8_monolith.a ~/prebuilt-v8-android/libs/arm64-v8a/libv8.a
cp ./out.gn/x86.release/obj/libv8_monolith.a ~/prebuilt-v8-android/libs/x86/libv8.a
cp ./out.gn/x64.release/obj/libv8_monolith.a ~/prebuilt-v8-android/libs/x86_64/libv8.a 

cp -r ./include ~/prebuilt-v8-android/
```