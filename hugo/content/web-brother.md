---
title: "Web Emulator"
date: 2020-03-15T15:52:39-05:00
draft: true
menu:
  main:
    weight: 20
---

<canvas id="canvas" style=""></canvas>
<script type="text/javascript" src="/emulator/es6-promise.js"></script>
<script type="text/javascript" src="/emulator/browserfs.min.js"></script>
<script type="text/javascript" src="/emulator/loader.js"></script>
<script type="text/javascript">
  var emulator = new Emulator(document.querySelector("#canvas"),
    null,
    new JSMAMELoader(JSMAMELoader.driver("wp2450ds"),
      JSMAMELoader.nativeResolution(728, 240),
      JSMAMELoader.scale(1.5),
      JSMAMELoader.emulatorJS("/emulator/mamebrotherwp.js"),
      JSMAMELoader.emulatorWASM("/emulator/mamebrotherwp.wasm"),
      JSMAMELoader.mountFile("/emulator/wp2450ds.zip",
        JSMAMELoader.fetchFile("BIOS File",
          "/emulator/wp2450ds.zip")),
      JSMAMELoader.mountFile("demo.img",
        JSMAMELoader.fetchFile("Disk File",
          "/emulator/demo.img")),
      JSMAMELoader.peripheral("flop", "demo.img"),
      //JSMAMELoader.extraArgs(["-bp ./"]),
      ));
  emulator.start({ waitAfterDownloading: true, hasCustomCSS: true });
</script>