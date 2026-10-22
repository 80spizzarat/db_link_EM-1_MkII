# Technical findings

Initial db link attempts preserved camera control property `0xD052=2` and failed after the `0xD06D` live-view mode write. Preferring 1280×960 and suppressing competing extended-event control polling did not resolve it. A model-specific transition to `0xD052=1` changed the camera display, but the bulk response never arrived and the camera appeared unresponsive. The command and data OUT bytes and lengths matched the successful Windows capture apart from transaction ID. A 20-second observation still produced no response.

The successful OM Capture trace had an interrupt-IN request pending before D052=1; an event `0xC108` referencing `0xD121` arrived shortly before the matching PTP OK. The accepted experimental build queues an interrupt-IN request before the single D052 write, serializes bulk PTP traffic, verifies the response and D052 readback, and stops on failure. Owner testing confirmed the build works on the stated equipment. This does not prove why interrupt ordering helps, nor that the event acknowledges D052.

Preserve the ordering and the prior fail-closed and reconnect safeguards. The prior hanging behavior warrants care: unplug USB if the camera becomes unresponsive. The accepted run is not evidence of compatibility with every camera, Android device, or firmware version.

