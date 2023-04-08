Pretty boring looking to be honest. I should find a way to do something fun with it.

```rust
use nannou::prelude::*;
use shrinkwraprs::Shrinkwrap;

fn main() {
    nannou::app(model).update(update).simple_window(view).run();
}

fn model(_: &App) -> Model {
    Model::default()
}

fn update(_: &App, model: &mut Model, _: Update) {
    match random_range(0, 4) {
        0 => model.x += 1.0,
        1 => model.x -= 1.0,
        2 => model.y += 1.0,
        _ => model.y -= 1.0,
    }
}

fn view(app: &App, model: &Model, frame: Frame) {
    let draw = app.draw();
    draw.rect()
        .xy(model.to_array().into())
        .w_h(1.0, 1.0)
        .color(WHITE);
    draw.to_frame(app, &frame).unwrap();
}

#[derive(Default, Shrinkwrap)]
#[shrinkwrap(mutable)]
struct Model(Vec2);
```