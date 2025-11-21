# Face Motion Demo Walkthrough

This demo uses MediaPipe Face Mesh to track your face and overlays a 3D mask using Three.js.

## How to Run

Because this demo requires access to the camera, modern browsers require it to be served over HTTPS or from `localhost`. You cannot simply open `index.html` as a file.

1.  Open a terminal in the project directory:
    ```bash
    cd /Users/fangyexu/Desktop/dev-s/winterx-antigravity/demo-face-motion
    ```

2.  Start a local server. You can use Python or Node.js:

    **Using Python:**
    ```bash
    python3 -m http.server
    ```

    **Using Node.js (npx):**
    ```bash
    npx http-server
    ```

3.  Open your browser and navigate to the URL shown (usually `http://localhost:8000` or `http://localhost:8080`).

4.  **Allow Camera Access** when prompted.

## What to Expect

-   You should see your webcam feed mirrored.
-   A 3D "Cyberpunk Mask" (green box with a dark visor) should appear on your face.
-   The mask should track your head position, rotation, and scale (distance).
-   If you cover your face or move out of frame, the mask should disappear.

## Implementation Details

-   **MediaPipe Face Mesh**: Tracks 468 3D landmarks.
-   **Three.js**: Renders the 3D scene.
-   **Synchronization**:
    -   **Position**: Calculated from the nose tip landmark, mapped to the Three.js camera view.
    -   **Rotation**: Calculated using vectors derived from landmarks (Temple-to-Temple for X-axis, Chin-to-Forehead for Y-axis).
    -   **Scale**: Estimated from the screen-space distance between temples.
