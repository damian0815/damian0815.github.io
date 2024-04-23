# Devlog

## 23 April 2024

### Making audiocraft magnet work on MPS

* identified that the token outputs on MPS and CPU differ
* rechecked differing with fixed seed
* identified that the token outputs differ after "1" step (actually: 4 steps, but i don't understand the steps yet)
* identified that the conditioning inputs are the same, so the problem is after conditioning

