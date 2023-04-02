A tool for printing out Bevy system schedules and render graphs in the [[DOT]] file format. To install:

```bash
cargo add bevy_mod_debugdump
```

Logging must be disabled. Because the format is sent to STDOUT, any logs will interfere with the file format.

```rust
let mut app = App::new();
app.add_plugins(
	DefaultPlugins
		.set(ImagePlugin::default_nearest())
		.build()
		.disable::<LogPlugin>(),
);
```

After that, I can follow any one of these [examples](https://github.com/jakobhellermann/bevy_mod_debugdump/tree/main/examples) to produce a DOT file. Here are some useful ones.

Print the main schedule:

```rust
bevy_mod_debugdump::print_main_schedule(&mut app);
```

Print the render graph:

```rust
bevy_mod_debugdump::print_render_graph(&mut app);
```

Filter the main schedule for my crate:

```rust
let settings = Settings::default().filter_in_crate("latierra");
let dot = bevy_mod_debugdump::schedule_graph_dot(&mut app, CoreSchedule::Main, &settings);
println!("{dot}");
```

Finally, I have to make sure to either remove `app.run()` or call it after the creation of the DOT file. Once the file contents are sent to STDOUT, it can be redirected to a file:

```bash
cargo run > graph.dot
```

I desribed some visualization tools in the [[DOT]] note.