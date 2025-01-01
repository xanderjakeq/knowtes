---
title: custom error types in rust
enableToc: false
date: 2024-12-31
lastmod: :git
tags:
  - rust
---
sources:
- [zero to prod](https://www.zero2prod.com/index.html?country_code=US) - error handling section

keep in mind the "orphan rule": it is forbidden to implement a foreign trait on
a foreign type. this is solved using [new type idiom](https://doc.rust-lang.org/rust-by-example/generics/new_types.html),
defining a custom `enum` type to wrap the foreign error type. the advantage of
doing this is that you can name the struct that makes sense for your project.
instead of a general `reqwest::Error` it could be `SendEmailError` defined as

```rust
struct SendEmailError(reqwest::Error)
```
there's more to it. read this [how to code it](https://www.howtocodeit.com/articles/ultimate-guide-rust-newtypes) guide about newtypes.


check the documentation about the `Error` types in the libraries you are using it
should tell you how to instantiate one from `std::error::Error`

all good error types should implement `std::error::Error` trait making it consistent
with all error types in the rust world. it is defined as:
```rust
pub trait Error: Debug + Display {
	/// The lower-level source of this error, if any.
	fn source(&self) -> Option<&(dyn Error + 'static)> {
		None
	}
}
```
the error type needs to implement `Debug` and `Display` traits. they are just
different ways to print the context of an error. one is for developers (people
who work on the internals) and consumers/users (other devs using the library or
end users) respectively.

`dyn Error` is a "trait object". a type where we only know it implements the
Error trait. 

> "generic types are resolved at compile-time (static dispatch) and trait objects
> incur a runtime cost (dynamic dispatch).
> > - zerotoprod

todo: define static dispatch or dispatch 

the `source` method returns the underlying error type of your custom error. in the
case of `SendEmailError`, `reqwest::Error`. implemented by hand like:

```rust

#[derive(Debug)] //Debug trait can implemented with this derive macro
struct SendEmailError(reqwest::Error)

impl std::error::Error for SendEmailError {
	fn source(&self) -> Option<&(dyn Error + 'static)> {
		Some(self.0) //might error, just read the compiler errors xd
	}
}
// or Error use default implementation like:
impl std::error:Error for SendEmailError {}

impl std::fmt::Display for SendEmailError {
	fn fmt(&self, f: std::fmt::Formatter<'_>) -> std::fmt::Result {
		write!(f, "Failed to send email.")
	}
}

// Debug can also be implemented like Display for more control over the printed message
// make sure to only use one implementation, else you'll get a compiler error
impl std::fmt::Debug for SendEmailError {
	fn fmt(&self, f: std::fmt::Formatter<'_>) -> std::fmt::Result {
		
		writeln!(f, "{}\n", self)?;

		//print the error chain into the formatter
		let mut current = self.source();
		while let Some(cause) = current {
			writeln!(f, "Caused by:\n\t{}", cause)?;
			current = cause.source();
		}
		Ok(())
	}
}
```

with the Error trait implemented, it can be used like:

```rust
async fn send_email(email: &str, content: &str) -> Result<(), SendEmailError> {}


let response = send_email("email@gmail.com", "hello").await;

if response.is_err() {
	println!("{}", response); // Failed to send email.
	println!("{:?}", response); //  ... Caused by: [message from reqwest::Error] ... more
}

```

