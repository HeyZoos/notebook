### Cartesian to Polar

```rust
fn cartesian_to_polar(x: f32, y: f32) -> (f32, f32) {
    let r = (x.powf(2.0) + y.powf(2.0)).sqrt();
    let phi = y.atan2(x);
    (r, phi)
}
```

### Polar to Cartesian

```rust
fn polar_to_cartesian(r: f32, phi: f32) -> (f32, f32) {
	let x = r * phi.cos();
	let y = r * phi.sin();
	(x, y)
}
```