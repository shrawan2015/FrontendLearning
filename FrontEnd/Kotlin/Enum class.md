

# Enum Classes
## **Enum Properties:**
## **Enum Methods:**
## Enum Constructors:
## Enum Extensions:

```
enum class DayOfWeek {  
	MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY  
}

fun getWeekendDays(): List<DayOfWeek> {  
	return listOf(DayOfWeek.SATURDAY, DayOfWeek.SUNDAY)  
}

enum class DayOfWeek(val number: Int) {  
	MONDAY(1),  
	TUESDAY(2),  
	WEDNESDAY(3),  
	THURSDAY(4),  
	FRIDAY(5),  
	SATURDAY(6),  
	SUNDAY(7)  
}

fun getDayNumber(day: DayOfWeek): Int {  
	return day.number  
}

enum class DayOfWeek(val number: Int) {  
	MONDAY(1),  
	TUESDAY(2),  
	WEDNESDAY(3),  
	THURSDAY(4),  
	FRIDAY(5),  
	SATURDAY(6),  
	SUNDAY(7);  
  
	fun isWeekend(): Boolean {  
		return this == SATURDAY || this == SUNDAY  
	}  
}

fun printDayType(day: DayOfWeek) {  
	if (day.isWeekend()) {  
		println("$day is a weekend day.")  
	} else {  
		println("$day is a weekday.")  
	}  
}

enum class DayOfWeek(val number: Int, val displayName: String) {  
	MONDAY(1, "Monday"),  
	TUESDAY(2, "Tuesday"),  
	WEDNESDAY(3, "Wednesday"),  
	THURSDAY(4, "Thursday"),  
	FRIDAY(5, "Friday"),  
	SATURDAY(6, "Saturday"),  
	SUNDAY(7, "Sunday");  
  
	override fun toString(): String {  
		return displayName  
	}  
}

fun printDayName(day: DayOfWeek) {  
   println("The day of the week is ${day.displayName}")  
}

fun DayOfWeek.nextDay(): DayOfWeek {  
    return when (this) {  
        MONDAY -> TUESDAY  
        TUESDAY -> WEDNESDAY  
        WEDNESDAY -> THURSDAY  
        THURSDAY -> FRIDAY  
        FRIDAY -> SATURDAY  
        SATURDAY -> SUNDAY  
        SUNDAY -> MONDAY  
    }  
}

fun printNextDay(day: DayOfWeek) {  
  println("The next day is ${day.nextDay()}")  
}

```

