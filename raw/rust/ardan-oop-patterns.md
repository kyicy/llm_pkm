# Unlearning Some Object Oriented Patterns

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Coming from an object-oriented language, you may be tempted to arrange data like this:

```rust
struct Organization {
    pub people: Vec<Person>,
}

struct Person {
    pub resources: Vec<Resource>,
}

impl Person {
    fn give_resource(&mut self, name: &str, org: &mut Organization, recipient: usize) {
        if let Some((idx, resource)) = self.resources.iter().enumerate()
            .find(|(_, item)| name == item.name) {
            self.resources.remove(idx);
            org.people[recipient].resources.push(resource.clone());
        }
    }
}
```

**This won't compile** because you can't borrow `org` mutably while also having a mutable borrow on `self`.

## The Rust Way: Move Ownership Up

Make the operation an organization-level function:

```rust
impl Organization {
    fn move_resource(&mut self, from: usize, to: usize, name: &str) {
        if let Some(resource) = self.people[from].take_resource(name) {
            self.people[to].give_resource(resource);
        }
    }
}

impl Person {
    fn take_resource(&mut self, name: &str) -> Option<Resource> {
        let index = self.resources.iter().position(|r| r.name == name);
        if let Some(index) = index {
            Some(self.resources.remove(index))
        } else {
            None
        }
    }

    fn give_resource(&mut self, resource: Resource) {
        self.resources.push(resource);
    }
}
```

What we did:
* `Organization` owns its workers and resources. A single mutable borrow gives you the ability to give the `Organization` orders.
* Broke the operation into a two-step process: `take_resource` then `give_resource`.
* The `move` semantic matches reality — there's only one stapler, and you know where it is at all times.

## Adding Error Handling

```rust
use thiserror::Error;

#[derive(Error, Debug)]
enum OrgError {
    #[error("The requested person does not exist")]
    PersonDoesNotExist(usize),
    #[error("The requested resource is not allocated to the person")]
    ResourceNotFound,
}

impl Organization {
    fn move_resource(&mut self, from: usize, to: usize, name: &str) -> Result<(), OrgError> {
        if let (Some(id1), Some(id2)) = (self.find_person(from), self.find_person(to)) {
            if let Some(resource) = self.people[id1].take_resource(name) {
                self.people[id2].give_resource(resource);
                Ok(())
            } else {
                Err(OrgError::ResourceNotFound)
            }
        } else if self.find_person(from).is_none() {
            Err(OrgError::PersonDoesNotExist(from))
        } else {
            Err(OrgError::PersonDoesNotExist(to))
        }
    }

    fn find_person(&self, id: usize) -> Option<usize> {
        self.people.iter().position(|p| p.id == id)
    }
}
```

Moving from traditional OOP into Rust-land follows this pattern: move ownership of the operation to a level that *actually owns* all of the parts, and break the work down into simple pieces.

This has:
* Removed the borrow checker error.
* Made it much more obvious what the code does.
* Made the code more robust with specific error handling.
