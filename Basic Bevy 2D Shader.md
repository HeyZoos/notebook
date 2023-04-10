This is the most irreducible program I could make to load a 2D shader. 

```rust
use bevy::{prelude::*, sprite::{MaterialMesh2dBundle, Material2d, Material2dPlugin}, render::render_resource::*, reflect::TypeUuid};

fn main() {
    App::new()
        .add_plugins(DefaultPlugins)
        .add_plugin(Material2dPlugin::<CustomMaterial>::default())
        .add_startup_system(setup)
        .run();
}

fn setup(
    mut commands: Commands,
    mut meshes: ResMut<Assets<Mesh>>,
    mut materials: ResMut<Assets<CustomMaterial>>,
) {
    commands.spawn(Camera2dBundle::default());
    commands.spawn(MaterialMesh2dBundle {
        mesh: meshes.add(Mesh::from(shape::Quad::default())).into(),
        transform: Transform::default().with_scale(Vec3::splat(128.)),
        material: materials.add(CustomMaterial {}),
        ..default()
    });
}

#[derive(AsBindGroup, TypeUuid, Debug, Clone)]
#[uuid = "a3d71c04-d054-4946-80f8-ba6cfbc90cad"]
struct CustomMaterial {}

impl Material2d for CustomMaterial {
    fn fragment_shader() -> ShaderRef {
        "shaders/hello.wgsl".into()
    }
}
```

This is the smallest WGSL shader I could manage. It needs to be stored as `assets/shaders/hello.wgsl` due to how Bevy loads assets.

```wgsl
struct FragmentInput {
    #import bevy_sprite::mesh2d_vertex_output
}

@fragment
fn fragment(in: FragmentInput) -> @location(0) vec4<f32> {
    return vec4<f32>(1.0, 0.0, 1.0, 1.0);
}
```