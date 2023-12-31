# Encode’s ZK bootcamp

Thème: Code - Informatique, Web3
Tags: Formation Complète
Formateur: Encode
Status: En cours
Date de création: July 24, 2023 2:43 PM

**Usefull links**

- **[website](https://www.encode.club/zk-bootcamp)**
- [ZK Bootcamp July 2023](https://www.notion.so/ZK-Bootcamp-July-2023-157fcb1fa18d44eaa5d7c29df74ea074?pvs=21)

Ressource :

- blog : [coders-errand.com](https://coders-errand.com/)
- podcast : [zeroknowledge.fm](https://zeroknowledge.fm/)

****Curriculum****

- Maths and cryptography introduction
- General theory of zero-knowledge proofs
- zk-SNARK / zk-STARK theory
- Development languages and platforms — Zokrates / Cairo / SnarkyJS
- Use of ZK proofs with blockchains — ZK rollups / Mina / snapps
- ZK proofs as proof of computation
- Data privacy
- ZK proofs in cryptocurrencies — Zcash / Monero
- ZK proofs and DeFi — Aztec and StarkEx

## Math Intro

[Introductory_Reading.pdf](https://file.notion.so/f/s/faba0237-8185-492f-944d-d6c46e05db86/Lesson1.pdf?id=d5685c29-eb08-460c-b5f9-494fecfdc371&table=block&spaceId=d0c8094a-e610-4814-9977-ce61e347ef5a&expirationTimestamp=1690466400000&signature=R1apscro5QhcFMBP89CgqM5M6UpP1lNV9LolFdsFxfc&downloadName=Lesson1.pdf)

**numbers**

- Set of Integers is **Z** : {…, -1,0,1,2…}
- Set of rational numbers is **Q** : {…1/2, 1, 3/2…}
- Set of Real Numbers is **R** : { 2, - 4, 4219, Pi, Racine(2)… }

**Also :**

- Fields are denoted by **F**
- we use **Zp*** for a finite field of int mod prime p (with multiplicative. inverses). (ps in french : we use Z/nZ instead of Zp)
- we use **finite fields** for cryptography

![Untitled](./notes-ressources/Untitled.png)

**Group theory**

## Day 1

---

### Homework 1

S = {0,1,2,3,4,5,6}

- 4+4 = 8
- 3 x 5 = 15
- inverse of 3 : ~~-3~~ → 1/3
- Can we consider ‘S’ and operation ‘+’ to be a group ?
- what’s -13 mod 5 ? 2 or -3 (2≡−3(mod5) ) but the remainder should be positive.
- for :

$$
x^3-x^2+4x-12
$$

- positive root ? : 2
- the degree of this polynomial ? : 3

### Homework 2

1. You just need to find examples, not proving:
    - is it true that all odd squares are identical to 1 (mod8) ?
        - odd square : (1^2, 3^2, 5^2…. ) → **YES**
    - what about even squares (mod8) → equal (0 or 4)
2. Try out the vanity btc address example at esecurity

   → it allow to have custom addresses (like : 0xc0ffee254729296a45a3… )

3. what do you understand by :
    1. O(n) → the computation time depends on the length of the input (linear)
    2. O(1) → the computation time is 1, it doesn’t depend on the length of the input and is always the same (constant = ideal case)
    3. O(logn) → better than O(n) but worse than O(1), good for sorting algorithms

   → we want O(1) ideally but O(logn) is ok too

## Day 2-3

---

- the prover Peggy takes a proving key `pk`, a public input `x` and a private witness `w`
- Peggy generates a proof
- the verifier Victor computes `V(vk, x, pr)` (returns the proof is correct and false if not)

The function returns true if Peggy knows a witness `w` satisfying `c(x,w) = true`

**Trusted setups and toxic waste**

- if a prover discover the secret lambda (the secret parameter = toxic waste), then he can create fake proofs
- how to not leak it ? → by doing a trusted setup (tau ceremony), they split the parameter in few persons and if only one person is honest and destroy his own toxic waste then we cannot recreate the parameter

**Polynomials in ZKPs**

If a prover claims to know some polynomial, that the verifier also knows, they can :

- verifier chooses a random value for x and evaluates his polynomial locally
- verifier gives x to the prover and asks to evaluate the polynomial in question
- prover evaluates her polynomial at x and gives the result to the verifier
- verifier checks if the local resylt is eqyal to the prover’s result, and if so then the statement is proven with a high confidence

In general there is a rule that if the local result is equal to the prover’s result, and if so the the statement is proven with high confidence

in general, the is a rule that if a poly P is zero accross a Set then it can be expressed as : P(x) = ….. another polynomial

**Homomorphic Hiding**

if E(x) is a fct with the props :

- given E(x) it’s hard to find x
- different inputs lead to different outputs (if x≠y then E(x)≠E(y))
- we can compute E(x+y)

The group Zp* with operations addition and multiplication allows this

**Example** : Alice wants to prove to Bob she knows x,y such that x+y=7

1. Alice sends E(x) and E(y)
2. Bob computes E(x+y) (possible because E is HH)
3. Bob computes E(7) and checks E(x+y) = E(7), if true then accepted

<aside>
➡️ need to check how bob can computes E(x+y) with on E(x) and E(y)

</aside>

**Zero knowledge proof theory part 1 - zkSNARKS**

- zkSNARKS are most common (zCash)
- process :
    - three algorithms C,P,V
    - Creator takes a secret parameter lambda and program C, and generates 2 publicly available keys (generated once for a program ***C***), also called **Common Reference String** :
        - proving key ***pk***
        - a verification ley : ***vk***

**ZoKrates - a toolbox for Ethereum**

→ presentation with a basic example (by computing, setup, generating a proof and exporting a smart contract)

![Untitled](./notes-ressources/Untitled%201.png)

![Untitled](./notes-ressources/Untitled%202.png)

![Untitled](./notes-ressources/Untitled%203.png)

### Homework 3

**1 - Follow this [tutorial](https://zokrates.github.io/examples/sha256example.html) to prove that you know the pre image of a hash**

```java
import "hashes/sha256/512bitPacked" as sha256packed;

def main(private field a, private field b, private field c, private field d) {
    field[2] h = sha256packed([a, b, c, d]);
    assert(h[0] == 263561599766550617289250058199814760685);
    assert(h[1] == 65303172752238645975888084098459749904);
    return;
}
```

here, the hash pre image is 5 and we assert that a prover knows it without revealing it

**In principle, how could you use Zokrates to verify that an eth adress has more than 1 eth ?**

- get the balance of an eth address
- use a check code like this one :

```java
def main(private field a) -> bool:
  return a > 1
```

## Day 4

---

Usage :

- Dark forest : game using zkp
- Zk microphone (ethglobal Paris)
- KYC
- …

Also, showcase of the funding & the starknet [ecosystem](https://www.starknet-ecosystem.com/)

![Untitled](./notes-ressources/Untitled%204.png)

ps : the sequencer may be centralized (to be validated)

- The Cairo language (rust like) is used for smart contract (like solidity). His syntax changed a lot recently.
- Sierra is bytecode
- process : cairo smart contract → sierra → cairo assembly → proof

Cairo’s statistics : [voyager.online](https://voyager.online/)

### **Intro to Rust**

**Core features**

- memory safety without garbage collection
- concurrecy without data races
- Abstraction without overhead

**variables**

- immutables by default
- but can be overriden using the `mut` modifier

```rust
let x = 1;
let mut y = 1;
```

**Types**

see documentation : [data-types](https://doc.rust-lang.org/book/ch03-02-data-types.html)

**scalar types**

- int : `u8, i32, u64`
- floating point numbers (`f32` (bits) and `f64` (bits))
- booleans (size : 1 bit)
- characters (unique integral)


## Day 5 (week 2)

---

starknet Architecture

![Untitled](./notes-ressources/Untitled%205.png)

![Untitled](./notes-ressources/Untitled%206.png)

### Transaction status

- NOT_RECEIVED
- RECEIVED
- ACCEPTED_ON_L2
- ACCEPTED_ON_L1
- REJECTED

### Transaction structure

![Untitled](./notes-ressources/Untitled%207.png)

### Full nodes

- keep record of all transaction (have more information)

### recursive starks

- bundle multiple transaction

### Rust

- idiomatic Rust
- Memory heap and stack
    - need to clean up memory : the compiler need to remove things from memory, needs to enforce certain rules

    ```rust
    let mut my_vec = vec![1,2,3];
    ```

  `my_vec` owns the vector, we want to avoid :

    - if out of scope, the value points to nothing (or a false)
    - if out of scope, not cleaned up

### **Rust ownership rules**

…

### **Copying**

…

### **Move**

…

```rust
let a = vec![1,2,3];
let b = a;
let c = a;   // <= PROBLEM HERE
// -> a don't have ownership
```

### **Control flow**

```rust
let a = vec![1,2,3];
while f() {
	g(a) // a lost ownership after 1st iteration
}
fn g(x: u8) {
...
}
```

### **References**

- `&a`
- if `a` has type `T`, then `&a` has type `&T`

`&` represent *references :* allow to refer to some value without taking ownership (don’t steal/drop the ownership)

### **2 types of references**

- ***shared*** reference : `&a`
    - read but not mutate the referent
    - can have any shared references
    - shared ref are copies
- ***mutable*** reference : `&mut`
    - can read and **modify** the referent
    - **only one mutable reference** at a time
    - (no ownership so don’t dictate when the value gonna be drop)

### **De referecing**

`*` operator

### **String Data types**

### Traits

Declared with the `trait` keyword

- similar to interface in other languages (allow pollymorphisme)

```rust
pub trait Summary {
		fn summarize(&self) -> String;
}
```

```rust
	pub struct Tweet {
	pub username : String,
}

impl Summary for Tweet {
	fn summarize(&selft) -> String {
		format!("{}: {}", self.username, self.content)
	}
}
```

**Using traits (polymorphism)**

```rust
pub fn notify(item: &impl Summary) {
	println!(”Breaking news {}”,  item.summarize());
}
```

### Intro to generics

allow to parametize accross datatypes, not only one datatype but allow “generic” types

```rust
struct Point<T> {
	x: T,
	y: T,
}

fn main() {
	let my_point = Point { x: 5, y: 6};
}
```

### Intro to vectors

```rust
let vect: Vec<i32> = Vec::new();
let v = vec![41, 42, 7]; // the compiler auto determine the type

// retrieve
v.get(1);

// iterate
for ii in &v {
	println!("{}", ii);
}

// iterate using iterators
let v1 = vec![1, 2, 3];
let mut v1_iter = v1.iter();
assert_eq!(v1_iter.next(), Some(&1));
assert_eq!(v1_iter.next(), Some(&2));
assert_eq!(v1_iter.next(), Some(&3));
assert_eq!(v1_iter.next(), None);
// here we use '&' for '&1' because we want to bring back Some of a ref
```

→ not understood why we are using the & here…)

→ *No, We are taking a reference, into_iter() will take ownership*

Notes : the '!' symbol in `let v = vec![1,2,3]`  : is a macro which means that vec is not a function call but a macro invocation that constructs a vector.

### shadowing

```rust
??
```

### Cairo

similar to rust but they are some differences

```rust
**// loops**
use PrintTrait;
fn main() {
 let mut counter = 0;
 let result = loop {
	 if counter == 10 {
		 break counter * 2;
	 }
	 counter += 1;
 };
 'The result is '.print();
 result.print(); 
}

**// Collection**
use Felt252DictTrait;
fn main() {
 let mut balances: Felt252Dict<u64> = Default::default();
 balances.insert('Alex', 100);
 balances.insert('Maria', 200);
 let alex_balance = balances.get('Alex');
 assert(alex_balance == 100, 'Balance is not 100');
 let maria_balance = balances.get('Maria');
 assert(maria_balance == 200, 'Balance is not 200'); 
}

**// Turning an Array into span**
let span = array.span();
```

Data types

<aside>
➡️ Arithmetic on felt252 is done mod p with p = 2251 + 17 ∗ 2192 + 1 
→ **Division doesn't work as you might expect**

</aside>

| Type | Size |
| --- | --- |
| u8 | 8bits |
| u16 | 16 bits |
| … | … |
| u256 | 256 bits |
| usize | 32 bits |

ps :

- u256 is implemented as a struct
- Booleans are one felt252 in size