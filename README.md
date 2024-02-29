## The main snippets for working with isometric dimensions

* [Definitions](https://github.com/neki-dev/isometric-snippets?tab=readme-ov-file#definitions)
* [Render](https://github.com/neki-dev/isometric-snippets?tab=readme-ov-file#render)
* [Conversion](https://github.com/neki-dev/isometric-snippets?tab=readme-ov-file#conversion)
* [Math](https://github.com/neki-dev/isometric-snippets?tab=readme-ov-file#math)

.

# Definitions

![Cube](./cube.png)

* TILE_X (green)
* TILE_Y (red)
* TILE_Z (blue)

* PERSPECTIVE = TILE_Y / TILE_X

# Render

### Get depth
```js
function depth(positionAtWorld) {
  return positionAtWorld.y + positionAtWorld.z;
}
```

# Conversion

### Convert matrix position to world position
```js
function matrixToWorld(positionAtMatrix) {
  const halfSize = {
    x: TILE_X / 2,
    y: TILE_Y / 2,
  };

  return {
    x: (positionAtMatrix.x - positionAtMatrix.y) * halfSize.x,
    y: (positionAtMatrix.x + positionAtMatrix.y) * halfSize.y,
    z: positionAtMatrix.z * TILE_Z,
  };
}
```

### Convert world position to matrix position
```js
function worldToMatrix(positionAtWorld) {
  const halfSize = {
    x: TILE_X / 2,
    y: TILE_Y / 2,
  };
  const n = {
    x: positionAtWorld.x / halfSize.x,
    y: positionAtWorld.y / halfSize.y,
  };

  return {
    x: Math.round((n.x + n.y) / 2),
    y: Math.round((n.y - n.x) / 2),
    z: Math.floor(positionAtWorld.z / TILE_Z),
  };
}
```

### Convert world position to screen position
```js
function worldToScreen(positionAtWorld) {
  return {
    x: positionAtWorld.x,
    y: positionAtWorld.y - positionAtWorld.z,
  };
}
```

# Math

### Get isometric distance
```js
function distance(a, b) {
  return Math.hypot(
    (b.x - a.x),
    (b.y - a.y) / PERSPECTIVE,
  );
}
```

### Get isometric angle
```js
function angle(from, to) {
  return Math.atan2(
    (to.y - from.y) / DIMENSION_PERSPECTIVE,
    (to.x - from.x),
  );
}
```
