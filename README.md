## Definitions

![Cube](./cube.png)

* TILE_X (green)
* TILE_Y (red)
* TILE_Z (blue)

* PERSPECTIVE = TILE_Y / TILE_X

## Render

<details>
  <summary>Convert matrix position to world position</summary>

  ```js
  function matrixToWorld(position) {
    const halfSize = {
      x: TILE_X / 2,
      y: TILE_Y / 2,
    };
  
    return {
      x: (position.x - position.y) * halfSize.x,
      y: (position.x + position.y) * halfSize.y,
      z: position.z * TILE_Z,
    };
  }
  ```

</details>

<details>
  <summary>Convert world position to matrix position</summary>

  ```js
  function worldToMatrix(position) {
    const halfSize = {
      x: TILE_X / 2,
      y: TILE_Y / 2,
    };
    const n = {
      x: position.x / halfSize.x,
      y: position.y / halfSize.y,
    };
  
    return {
      x: Math.round((n.x + n.y) / 2),
      y: Math.round((n.y - n.x) / 2),
      z: Math.floor(this.z / TILE_Z),
    };
  }
  ```

</details>

<details>
  <summary>Convert world position to screen position</summary>

  ```js
  function worldToScreen(position) {
    return {
      x: position.x,
      y: position.y - position.z,
    };
  }
  ```

</details>

<details>
  <summary>Get render depth</summary>

  ```js
  function depth(position) {
    return position.y + position.z;
  }
  ```

</details>

## Math

<details>
  <summary>Get isometric distance</summary>

  ```js
  function distance(a, b) {
    return Math.hypot(
      (b.x - a.x),
      (b.y - a.y) / PERSPECTIVE,
    );
  }
  ```

</details>

<details>
  <summary>Get isometric angle</summary>

  ```js
  function angle(from, to) {
    return Math.atan2(
      (to.y - from.y) / DIMENSION_PERSPECTIVE,
      (to.x - from.x),
    );
  }
  ```

</details>
