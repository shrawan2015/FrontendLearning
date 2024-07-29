

**12. What is the difference between a list and an array in Kotlin?**





# Memory allocation

Speed is not the only advantage of using sequences, they can also process large datasets allocating less memory and avoiding potential errors. To illustrate this, consider a small modification to the previous example, where before checking the `_bitCount_` , we double each element in the collection.

with((0..10)) {
  asSequence()
      .onEach { print("seq: $it ") }
      .map { it * 2 }
      .find { it.bitCount() == 2 }
      .let { out ->
          println("\nseq out: $out")
      }

  toList()
      .onEach { print("list: $it ") } //new collection created
      .map { it * 2 }                 //new collection created
      .find { it.bitCount() == 2 }
      .let { out ->
          println("\nlist out: $out")
      }
}

In case we had a dataset with a very large number of entries of even a small dataset with very large entries, this repeated allocation of memory that the list requires would soon become an issue and potentially throw an out of memory error.

Ref:
- https://medium.com/codex/an-intuitive-introduction-to-sequences-in-kotlin-5f4682c5a3cb