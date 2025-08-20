## Instructions:

This link contains chromium gwp-asan build for android. 

https://drive.google.com/file/d/1SY169aEuMhTzuQwZr4YV6Pqo0y8VTodT/view?usp=sharing

## GWP-Asan

It is a tool designed to detect memory safety errors like use-after-free and out-of-bounds reads/writes.
The following args were used to build this chromium:

```
target_os = "android"
target_cpu = "x86"
use_remoteexec = false
is_component_build = false                
symbol_level=1                 
enable_gwp_asan=true           
```

**Note:** Even when GWP‑ASan is compiled in, Chrome only samples allocations when you enable the feature.

## Steps to enable this flag:

1. On your desktop, create cmdline.txt:
```
cat <<EOF > cmdline.txt
_ --enable-features=GwpAsanMalloc<Study \
  --force-fieldtrials=Study/Group1 \
  --force-fieldtrial-params=Study.Group1:AllocationSamplingFrequency/1000/ProcessSamplingProbability/1.0
EOF
```

2. Push it to the device: `adb push cmdline.txt /data/local/tmp/chromium-command-line`
`adb shell chmod 644 /data/local/tmp/chromium-command-line`
3. Restart Chromium and go to chrome://version and check if the flags have been written. It should appear something like this:
<img width="361" height="758" alt="image" src="https://github.com/user-attachments/assets/df30f7f6-da1c-40f8-b60c-163d06e1002d" />

**Note:** There is currently no intentional way of triggering a crash that can be detected by gwp-asan hence, chrome://crash or any debug urls won't work.

If there are any mistakes in any instructions feel free to raise an issue. 

