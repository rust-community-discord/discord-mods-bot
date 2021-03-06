# Commands
Commands for the bot are managed using the `Commands` struct.  The `.add` method
is used to define commands for the bot to react to.  

## Defining Commands
Commands are defined using a string and a function.  The string is the command
that the user must type and the function is the handler for that command.  

An example command using an anonymous function as a handler.  
```rust
let mut cmds = Commands::new();

cmds.add("?greet {name}", |args: Args<'_>| -> Result {
  println!("Hello {}!", args.params.get("name").unwrap());
});
```

The same command using a function pointer as a handler.  
```rust
fn print_hello_name(args: Args) -> Result {
  println!("Hello {}!", args.params.get("name").unwrap());
};

let mut cmds = Commands::new();
cmds.add("?greet {name}", print_hello_name);
```

## Command Syntax
Commands use a syntax with 3 different kinds of elements that can be used
together.  

+ Static elements must be matched exactly, these are strings like `?talk` and
  `!ban`.  
+ Dynamic elements match any input other than a space.  To use a dynamic
  element in your command use `{key}` where `key` can be any name that
  represents that particular input element.
+ Quoted elements match any input but must be surrounded by quotes.  To use a
  quoted element in your command use `[key]` where `key` can be any name that
  represents that particular input element.  

## Command Handlers
Functions are used as handlers for commands.  Specifically handler functions
must use the following signature: `(Args<'_>) -> Result`.

## Args
The `Args` type encapsulated the parameters extracted from the input as well as
the `Message` and `Context` types from the Serenity crate.  

### Serenity
The library the bot uses to communicate with discord is called Serenity.
Serenity abstracts all communication with discord into methods available through
the `Message` and `Context` types.  

