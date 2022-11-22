The following command fails
```bash
bazel build app/client:build 
```
for
```
Could not find a required file.
  Name: index.js
  Searched in: /private/var/tmp/_bazel_yue.chen/22251a1ad8f3db605269cea809b107e6/sandbox/darwin-sandbox/43/execroot/__main__/bazel-out/darwin-fastbuild/bin/app/client/src
Target //app/client:build failed to build
```
whereas
```bash
/bazel build app/client/src:all
```
succeeds
