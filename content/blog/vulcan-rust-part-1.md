---
date: 2020-08-15
title: Starting with Vulkan and Rust
authors: ["porrithsuong"]
categories:
  - graphics
  - vulkan
  - rust
tags:
  - graphics
  - vulkan
  - rust
---

So I've always wanted to learn Rust and Vulkan together. I've done a bit of it before using C++ and Vulkan, but I'd like to 
start recreating that previous C++ Vulkan Renderer with Rust. So in these series of blog posts - I'll write some public notes 
on Rust and how it is interfaced with the Vulkan ash crate.

The implementation of Vulkan will primarily be based on this [tutorial](https://vulkan-tutorial.com/). This blog post 
will cover the [Instance](https://vulkan-tutorial.com/Drawing_a_triangle/Setup/Instance) section of the tutorial series.

Without further ado, let's get started!

## Structs

Structs in Rust are typically styled in a C like fashion. With Vulkan, I ended up defining a `VulkanApp` struct which 
contains an `_entry` and an `_instance` field. 

```rust
use ash::version::{EntryV1_0, InstanceV1_0};
use ash::{vk, Entry, Instance};
use std::{error::Error, ffi::CString, result::Result};

struct VulkanApp
{
    _entry: Entry,
    _instance: Instance
}
```

What's interesting about Rust, is the implementation is typically defined out of the structure using the `impl` keyword. 
Coming from C#/C++, this looks a bit odd since I didn't have to define the function protoypes in a header, but just write 
out the implementation in a different section.

```rust
impl VulkanApp // <- Like a header, I just defined the implemented functions on a type like so
{
    // Some function implementations here
}
```

So with Vulkan, I have to create an instance which I can access. The ash crate follows a Fluent like API, which is also 
commonly referred to as a builder pattern. Here's a page on [Wikipedia](https://en.wikipedia.org/wiki/Fluent_interface) 
about said pattern, I've certainly seen this style around and it is very human readable.

```rust
impl VulkanApp
{
    // Pretty much my constructor written in a function
    fn new() -> Result<Self, Box<dyn Error>>
    {
        log::info!("Creating application");

        let entry = ash::Entry::new().expect("Failed to create entry!");
        let instance = Self::create_instance(&entry)?;

        Ok(Self
           {
               _entry: entry,
               _instance : instance
           })
    }

    fn create_instance(entry: &Entry) -> Result<Instance, Box<dyn Error>>
    {
        // Some really nice Fluent API right here!
        let app_info = vk::ApplicationInfo::builder()
            .application_name(CString::new("Vulkan Application")?.as_c_str())
            .application_version(ash::vk_make_version!(0, 1, 0))
            .engine_name(CString::new("No Engine")?.as_c_str())
            .engine_version(ash::vk_make_version!(0, 1, 0))
            .api_version(ash::vk_make_version!(1, 0, 0))
            .build();

        let extension_names = util::required_extension_names();

        let instance_create_info = vk::InstanceCreateInfo::builder()
            .application_info(&app_info)
            .enabled_extension_names(&extension_names);

        unsafe 
        { 
            Ok(entry.create_instance(&instance_create_info, None)?) 
        }
    }
}
```

## The ? Operator

Okay, so there are some things I need to go over with the `create_instance` function. Let's focus on this line first:

`.application_name(CString::new("Vulkan Application")?.as_c_str())`

> What the heck does the `?` mean?

Well first, we use a type called `CString`, which is a C compatible string (remember that in C, we define strings like so 
`char*`). Rust does not have exceptions per say, what they introduce is something called panics, which have limited functionality. 
Panics are typically non recoverable, but we can perform something similar to a "try-catch" using a `match` statement on 
a `Result` struct (I'll show this later).

The `?` operator is just a short hand similar to the null coalescense operator. If there is no error, then the `as_c_str()` 
function will execute. Otherwise, the function will early out.

## Using Functions Implemented in Another File

It's not very obvious from the code snippet, but the `util:required_extension_names()` is a function implemented in a 
different file. 

Like most programming languages, I typically import the other file using the `mod` keyword (other langauges like C 
will use the `#include` define). Files are typically organized as modules in Rust so a file like `util.rs` will be 
referenced as `mod util` in the import section of the file.

### Per Platform Configurations

Rust is designed to work on major operating systems such as Windows, Linux, and macOS. So for a cross compiled language, 
there will be cases where libraries and extensions are only available on the platform. While C based language can provide 
scripting defines and define locks per platform, Rust provides an attribute called `cfg`. The `cfg` attribute provides 
conditional compilation like in the util.rs file example below.

```rust
use ash::extensions::khr::Surface;

#[cfg(target_so = "windows")]
use ash::extensions::khr::Win32Surface;

#[cfg(target_os = "windows")]
pub fn required_extension_names() -> Vec<*const i8> 
{
    vec![
        Surface::name().as_ptr(), 
        Win32Surface::name().as_ptr()
    ]
}

#[cfg(target_os = "macos")]
use ash::extensions::mvk::MacOSSurface;

#[cfg(target_os = "macos")]
pub fn required_extension_names() -> Vec<*const i8>
{
    vec![
        Surface::name().as_ptr(), 
        MacOSSurface::name().as_ptr()
    ]
}
```

## Unsafe

All safe functions from the standard library are built on "unsafe" functionality, which means that the code isn't inherently 
unsafe to use, but can have unexpected behaviours if used improperly. Pointers, while common in C and C++, are typically 
hidden in languages like Java and C# (although C# provides pointers via unsafe feature too!). Rust provides pointer 
support in the unsafe context, so we can interop Rust with external libraries like Vulkan (which is originally a C 
library). 

In the `unsafe` block, a value of type `Result` is returned. The `Result` is a kind of conditional yield. If the operation 
is successful, then the `Ok` enum will execute, otherwise the `Err` enum will execute.

```rust
unsafe 
{ 
    Ok(entry.create_instance(&instance_create_info, None)?)  // Everything is a-ok to create the Vulkan instance.
}
```

## Implementing the Drop trait for VulkanApp

Langages like C#/C++ allow you to define a destructor, which is a form of cleanup when the structure leaves out of scope. 
This is done with RAII in C++ and C# handled by the GC for managed objects. 

Rust has a form of a destructor called `Drop`, which is exactly like C++ or C# destructor.

```rust
impl Drop for VulkanApp 
{
    fn drop(&mut self) 
    {
        log::debug!("Dropping application.");
        unsafe 
        {
            self._instance.destroy_instance(None);
        }
    }
}
```

## Running the Application

The `run` function is very simple for now. All I am doing at the moment is simply logging that the application is running 
after creating the Vulkan instance.

```rust
fn run(&mut self)
{
    log::debug!("Running Application.");
}
```

Just some additional notes:

Rust by default will always declare variables as ***immutable***. To allow mutability on a variable, you add the `mut` keyword. 

When assigning variables in Rust, like `let x = y`, Rust moves the owner ship of the value of `y` to `x`. When the 
value moves, the previous variable `y` is no cleaned up and has no reference. This ensures `dangling` pointers are properly 
dealt with.

### The main() function

I think by convention, most programming languages will declare a `main` function as the entry point for any program. 

```rust
fn main()
{
    env_logger::init();
    match VulkanApp::new() 
    {
        Ok(mut app) => app.run(),
        Err(error)  => log::error!("Failed to create application. Cause: {}", error),
    }
}
```

I initialize a logger so I can log any kinds of errors and implement the `match` statement. Since the `new()` function 
will return a `Result<T, U>`, I explicitly implement the `Ok` and `Err` states. If the application runs without errors, 
then I run the `app.run()`. Otherwise, I'll log the error.

I'm currently working on the validation layers. Once I'm done with that, I can write the next entry in this blog series 
about implementing validation layers.
