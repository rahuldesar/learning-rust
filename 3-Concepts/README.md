# COMMON PROGRAMMING CONCEPTS.

//I'll REFACTOR WHEN I CAN.

1) Variables and Mutability
2) Data Types
3) Functions
4) Comments
5) Control Flow


## 1. Variables. 
=======================================================================

By default variables are immutable. ❓
but still there is an option to make variables mutable.(opt out)

`let x = 5` ✅ 

To opt out of immutablility - we use `mut` 

`let mut mutable_variable = 6` ✅  

-- Constants 
* Not allowed to `mut` with constants.
* Constants aren't just immutable by default. They are always immutable.
* `const` instead of `let` and the type of the value must be annotated.
* constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.
* all UPPERCASE with underscore - Rust's naming convention.

`const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;` ✅

-- Shadowing .
* You can declare a new variable with the same name as a previous variable.
* Second variable <i>overshadows</i> the first, until it itself is overshadowed or the scope ends.

```
fn main() {
    let x = 5; //5 
    let x = x + 1; //6 -> Shadows previous x.
    {
        let x = x * 2; //12
        x = x * 2 ; // ERROR : MUTATION.
        println!("The value of x in the inner scope is: {x}"); //12
    }
    println!("The value of x is: {x}"); //6
}
```

NOTE : shadowing and `mut` is not same.
 * Since we are creating new variable while shadowing, we can change the type of the value but reuse same name.

```
// CHANGING TYPE OF VARIABLE BY SHADOWING
  let spaces = "   "; // string 
  let spaces = spaces.len(); // number
```
```
// ERROR WHEN CHANGING TYPE OF VARIABLE USING MUT
  let mut spaces = "   ";
  spaces = spaces.len (); //  ERROR . mismatched types.
```

## 2. Data Types.

1) Scalar
* Integer types
  * Signed `i`
  * Unsigned `u`

  | Length |	Signed |	Unsigned |
  |---------|-------|---------|
  | 8-bit |	i8 |	u8 |
  | 16-bit |	i16 |	u16 |
  | 32-bit |	i32 |	u32 |
  | 64-bit |	i64 |	u64 | 
  | 128-bit |	i128 |	u128 |
  | arch |	isize |	usize |



each variant has an explicit size.

`isize` and `usize` depends on the architecture of computer your program is running on.

  | Number literals |	Example|
  | ------------- | ------------- |
  | Decimal |	98_222 |
  | Hex	| 0xff |
  | Octal	| 0o77|
  | Binary |	0b1111_0000|
  | Byte (u8 only) |	b'A'|

where `_` is visual seperator. 1000 is same as 1_000.


* Floating-point Types.
  * `f32` 
  * `f64` - default.

  ```
  let x = 2.0; // f64
  let y: f32 = 3.0; // f32
  ```


* Numeric Operations
  ```
  fn main() {
      // addition
      let sum = 5 + 10;

      // subtraction
      let difference = 95.5 - 4.3;

      // multiplication
      let product = 4 * 30;

      // division
      let quotient = 56.7 / 32.2;
      let floored = 2 / 3; // Results in 0

      // remainder
      let remainder = 43 % 5;
  }
  ```

* The Boolean Type.
  ```
  fn main() {
      let t = true;
      let f: bool = false; // with explicit type annotation
  }
  ```

* The Character Type 

  We specify `char` literals with `single quotes`, as opposed to string literals, which uses double quotes. char is 4 bytes in size and represents a Unicode scalar value. i.e It can represent Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces.
  ```
  fn main() {
      let c = 'z';
      let z: char = 'ℤ'; // with explicit type annotation
      let heart_eyed_cat = '😻';
  }
  ```

2) Compound
=======================================================================

* The Tuple Type
  General way of grouping together a number of values with a variety of types into one compound type
  * Tuples have fixed length, once declared they cannot grow or shrink in size.
  * We create a tuple by writing a comma-separated list of values inside parentheses  ie `(val1, val2, val3)`.
  * Each position in the tuple has a type, and the types of the different values in the tuple don’t have to be the same

  ```
  fn main() {
      let tup: (i32, f64, u8) = (500, 6.4, 1);
  }
  ```

  * The variable tup binds to the entire tuple. Tuple is considered a single compound element

-- ACCESSING TUPLE VARIABLE 
  * To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value.
  * We can also access a tuple element by using a period (`.`) .
  ```
  // Destructuring a tuple value.
  fn main() {
      let tup = (500, 6.4, 1);
      let (x, y, z) = tup; // Destructuring tuple into x, y and z.
      println!("The value of y is: {y}"); 
  }
  ```
  ```
  // Using period to access tuple.
  fn main() {
      let x: (i32, f64, u8) = (500, 6.4, 1);
      let five_hundred = x.0;
      let six_point_four = x.1;
      let one = x.2;
  }
  ```

* The Array Type.
  * Unlike a tuple, every element of an array must have the <b>same type</b>
  * Arrays in Rust have <b>fixed length</b>
  * A **vector** is a similar collection type provided by the standard library that is **allowed to grow or shrink in size**

  ```
  // Array initialize ways :- 
  fn main() {
      let a = [1, 2, 3, 4, 5]; // type is implied.
      let b: [i32; 5] = [1, 2, 3, 4, 5]; // with explicit type and size.
      let c = [3; 5]; // [3, 3, 3, 3, 3] - same value for each element

  }
  ```
   * Accessing Array elements.
  ```
  fn main() {
      let a = [1, 2, 3, 4, 5];

      let first = a[0]; // 1
      let second = a[1]; // 2 
  }

  ```

<b>NOTE</b> : Arrays are useful when you want your data allocated on the **stack** rather than the **heap**. (Covered in chap 4) 


## Functions.
  `fn` keyword allows you to declare new functions.
   - snake_case as the convention.

  ```
  fn main() {
      println!("Hello, world!");

      another_function();
  }

  fn another_function() {
      println!("Another function.");
  }
  ```


**Note** that we defined another_function after the main function in the source code; we could have defined it before as well. (must be within scope seen by caller.) (ques. Hoisting??? ❓)

  * Parameters. 

  ```
  fn main() {
      another_function(5); // function call with argument 5.
  }

  fn another_function(x: i32) { // one parameter of type i32 
      println!("The value of x is: {x}");
  }
  ```
  * Statements and Expressions.
    - **Statements** are instructions that perform some action and do not return a value. Expressions evaluate to a resulting value. Let’s look at some examples.
    
      - `let y = 6;` is a statement.
      - **Function definitions** are also statements
      - **Statements** do not return values
        - So, `let x = (let y = 6);` ❌ . This doesnt make sense.
        - Also, `x = y = 6` ❌ this makes sense in C and Ruby, but doesn't work in Rust.
    
    - **Expressions** evaluate the value.
      - consider math operations like `5 + 6`.
      - also, `6` in `let y = 6;`

      ```
      fn main() {
          let y = { // Looks wierd but get used to it.
              let x = 3;
              x + 1  // Note: no ; .
          };

          println!("The value of y is: {y}"); // y = 4 ✅
      }
      ```
      - Expressions do not include ending semicolons. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value

  * Functions with Return Values
    - We don’t name return values, but we must declare their type after an arrow (`->`).
    - In Rust, the return value of the function is synonymous with the value of the final expression in the block of the body of a function.
    - You can return early from a function by using the `return` keyword and specifying a value.

  ```
  fn five() -> i32 { // return type = i32
      5     // PERFECTLY VALID .. returns 5. NOTE- no `;` 
  }

  fn main() {
      let x = five();

      println!("The value of x is: {x}");
  }
  ```
  ```
  // Another Example. 
  fn main() {
      let x = plus_one(5);

      println!("The value of x is: {x}"); // 6
  }

  fn plus_one(x: i32) -> i32 {
      x + 1
  }
  ```

## Comments .

```
// Simple Comment

fn main() {
  //More common than inline comment.
  let x = 7; // ALSO Valid comment. within lines.
}

```

## Control Flow.
  * `if` Expression
    - condition must be bool. 
      - (in JS if condition is falsy or truthy, it is still valid. BUT it doesn't work in RUST)
  ```
  if <condition> {
    // if body
  } else {
    // else body
  }
  ```
  ```
  // Handling Multiple Conditions with else if
  if <condition> {
    // if body
  } else if {
    // else if body
  } else if {
    // else if body
  } else {
    // else body
  }
  ```
  ```
  // Using if in a let Statement. both value must be of same type.
  let number = if condition { 5 } else { 6 };
  ```

  * Loops - Rust has 3 kinds of loops. 
    - `loop`
      - The `loop` keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.
      - Use `break` keyword to stop executing the loop.
      - Use `continue` keyword to skip over any remaining code in current iteration and go to next iteration.
      ```
      // Usage of `loop` 
      fn main() {
          let mut counter = 0;

          let result = loop {
              counter += 1;

              if counter == 10 {
                  break counter * 2;
              }
          };

          println!("The result is {result}"); // result = 20
      }
      ```
      - LOOP LABEL 
        - If you have loops within loops, break and continue apply to the innermost loop at that point.
        - You can optionally specify a loop label on a loop that we can then use with break or continue to specify that those keywords apply to the labeled loop instead of the innermost loop.
        - Loop labels must begin with a single quote
        ```
        fn main() {
            let mut count = 0;
            'counting_up: loop { // LOOP LABEL 🏷️
                println!("count = {count}");
                let mut remaining = 10;

                loop {
                    println!("remaining = {remaining}");
                    if remaining == 9 {
                        break;
                    }
                    if count == 2 {
                        break 'counting_up; // ❗ breaking to 'counting_up.
                    }
                    remaining -= 1;
                }

                count += 1;
            }
            println!("End count = {count}");
        }

        ```

    - `while`
      - while the condition is true, loop runs.
      - while condition ceases to be true, the program calls break. 
      ```
      while <condition>{
        //loop body
      }
      ```

    - `for`
      ```
      for element in array{
        //loop body
      }
      ```

      ```
      //COUNTDOWN APP
      fn main() {
          for number in (1..4).rev() { // rev = reverse the range. , (1..4) -> Range
              println!("{number}!");
          }
          println!("LIFTOFF!!!");
      }
      ```
      - `Range` generates all numbers in sequence starting from one number and ending before another number.