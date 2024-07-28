

“The function caller can catch this exception and process it; if it doesn’t, the exception is rethrown further up the stack.”

- “You throw an exception using the throw keyword”



```kotlin

if (percentage !in 0..100) {
    throw IllegalArgumentException(
        "A percentage value must be between 0 and 100: $percentage"
    )
}


fun readNumber(reader: BufferedReader): Int? {    ❶
    try {
        val line = reader.readLine()
        return Integer.parseInt(line)
    } catch (e: NumberFormatException) {          ❷
        return null
    } finally {                                   ❸
        reader.close()
    }
}
 
fun main() {
    val reader = BufferedReader(StringReader("239"))
    println(readNumber(reader))
    // 239
}


fun readNumber(reader: BufferedReader) {
    val number = try {
        Integer.parseInt(reader.readLine())   ❶
    } catch (e: NumberFormatException) {
        return
    }
 
    println(number)
}
 
fun main() {
    val reader = BufferedReader(StringReader("not a number"))
    readNumber(reader)                        ❷
}
```