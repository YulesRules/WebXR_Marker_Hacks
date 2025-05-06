<h1>WebXR Marker Tracking with Environment-Anchored Cube</h1>
This project extends the original Immersive Web Community Group's camera access + ArUco marker tracking sample by adding the ability to anchor a 3D object in environment space based on a detected marker position. It uses WebXR, OpenCV.js with ArUco support, and WebGL2 for rendering.<br><br>

The motivation behind this project is partly due to frustration: image marker tracking in WebXR has been stuck behind feature flags in Chromium (like #webxr-incubations) for several years and hasn't seen much momentum toward being unflagged. This project is my workaround - using OpenCV.js for marker tracking outside of the WebXR API, and manually converting those positions into a persistent anchor in environment space.

This is also a testbed for future extensions and integrations.

<p><br>
Demo video: Coming soon
<br><br>

<h2>Features</h2> <ul> <li>Marker-based tracking using OpenCV.js and ArUco markers</li> <li>Anchoring of a 3D cube in environment (local) space</li> <li>WebXR 'immersive-ar' session with camera feed and DOM overlay</li> <li>Asynchronous pixel readback to prevent frame blocking</li> </ul> <br> <h2>How it Works</h2>
When an ArUco marker is detected, its pose is extracted and transformed from viewer space into environment space using a matrix chain:

Invert the viewer pose matrix to get world coordinates

Transform to the 'local' (environment) reference space

Store the resulting position and render the cube at that location in future frames

This allows the virtual object to remain in place even after the marker disappears, simulating AR persistence using marker input as a one-time spatial anchor.
<br><br>

<h2>Requirements</h2> <ul> <li>On Android, a browser with WebXR support and camera access (e.g., Chromium-based browsers)</li> <li>Self-hosted build of OpenCV.js including <code>aruco</code> module</li> <li>Secure context (HTTPS or localhost)</li> </ul> <br> <h2>Configuration</h2>
You can enable or disable various options through the UI:

<ul> <li><b><i>Async Read</i></b>: Enables non-blocking image readback and background detection</li> <li><b><i>Delay Camera Image</i></b>: Syncs camera texture with pose updates</li> <li><b><i>Show Debug OpenCV</i></b>: Displays processed OpenCV canvas</li> <li><b><i>Downscale Factor</i></b>: Controls image resolution before detection</li> <li><b><i>Show Environment Cube</i></b>: Toggles the anchored cube</li> </ul> <br> <h2>Usage</h2>
Launch the WebXR AR session using the 'Enter AR' button. The application will begin processing camera frames, detecting markers, and - once a marker is found - anchoring a cube at its last known position in the environment space. The cube rotates and persists independently of further marker detection.

<br> <h2>Limitations</h2>
This project does not currently support:

<ul> <li>Multiple persistent anchors</li>  </ul>
It’s meant as a proof-of-concept for marker-initiated world anchoring using purely client-side JavaScript, with no reliance on cloud anchors or persistent backends.

<br> <h2>Roadmap</h2> <ul> <li>Add an alternative renderer using <b>Three.js</b> for simpler integration and visual upgrades</li> <li>Add support for <b>[Variant3D](https://launch.variant3d.com/) app clip</b> to enable fast-loading marker-driven WebXR overlays</li> <li>Explore anchoring multiple objects or restoring previously stored anchors</li> <li>Add fallback handling for devices that lack WebXR or camera permissions</li> </ul> <br> <h2>Troubleshooting</h2> <ul> <li>Ensure your browser supports WebXR and camera access</li> <li>Use a secure context (localhost or HTTPS)</li> <li>Check your OpenCV.js build includes the <code>aruco</code> module</li> <li>Use a clear, well-lit printed marker like the <a href="https://docs.opencv.org/4.x/d5/dae/tutorial_aruco_detection.html">6x6 ArUco markers</a>, (<a href="https://chev.me/arucogen/">see here for a generator</a>)</li> </ul> <br>
Thanks for checking this out!
<br><br>
– Yulia.M
