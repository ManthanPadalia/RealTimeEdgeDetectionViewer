# 🔍 Real-Time Edge Detection — Short README

A compact guide for the real-time edge detection project (Web first, Android notes included).

## What’s included (implemented)

- Web (implemented)
  - Real‑time webcam processing (TypeScript) with multiple algorithms: Sobel, Canny, Roberts, Prewitt, Laplacian. See [`EdgeDetector.sobel`](src/edge-detection.ts) and [`EdgeDetector.canny`](src/edge-detection.ts).
  - OpenCV C++ via WebAssembly wrapper: [`OpenCVProcessor.initialize`](src/opencv-processor.ts).
  - GPU rendering using WebGL (OpenGL ES 2.0): [`WebGLRenderer.render`](src/webgl-renderer.ts).
  - Main app glue: [`EdgeDetectionApp`](src/app.ts).

Files to inspect:

- [src/app.ts](src/app.ts)
- [src/edge-detection.ts](src/edge-detection.ts)
- [src/opencv-processor.ts](src/opencv-processor.ts)
- [src/webgl-renderer.ts](src/webgl-renderer.ts)
- [src/types.ts](src/types.ts)
- [index.html](index.html)
- [serve.py](serve.py)
- [package.json](package.json)
- [tsconfig.json](tsconfig.json)

## Quick screenshots / GIF

-

## Quick setup (Web)

1. Install deps and build:
   - npm install
   - npm run build
2. Serve:
   - npm run serve
   - or python serve.py
3. Open: http://localhost:8000
   (See [package.json](package.json) and [serve.py](serve.py))

## Android port notes (NDK / JNI / OpenCV)

- Use OpenCV Android SDK and Android NDK.
- Native pipeline idea:
  - Camera frames → native code via JNI → process using OpenCV C++ (same algorithms) → return RGBA buffer → render via Surface/GL.
- Key items to implement on Android:
  - JNI bridge mirroring [`OpenCVProcessor`](src/opencv-processor.ts) behavior.
  - Native modules for Sobel/Canny if you want parity with WASM performance.
- Useful tools: Android NDK, OpenCV Android SDK, Gradle native build.

## Architecture (short)

- Frame flow (Web):
  1. Webcam → 2D input canvas ([src/app.ts](src/app.ts))
  2. Process via:
     - WebAssembly OpenCV: [`OpenCVProcessor`](src/opencv-processor.ts) or
     - TypeScript algorithms: [`EdgeDetector`](src/edge-detection.ts)
  3. Render result to WebGL texture: [`WebGLRenderer.render`](src/webgl-renderer.ts)
- Android mapping:
  - Camera → native (JNI) → OpenCV C++ → Output buffer → GL renderer / SurfaceView.

## References & quick links

- Entry point: [src/app.ts](src/app.ts) — look at initialization and controls.
- Algorithms: [src/edge-detection.ts](src/edge-detection.ts)
- WASM/OpenCV wrapper: [src/opencv-processor.ts](src/opencv-processor.ts)
- Renderer: [src/webgl-renderer.ts](src/webgl-renderer.ts)
- Build config: [tsconfig.json](tsconfig.json)

## Contributing / Commit history

-
