#### Java Time classes
1. java.util.Date and SimpleDatetimeFormatter
   1. Aren’t thread-safe, leading to potential concurrency issues for users
   2. Some date and time classes also exhibit quite poor API design.
2. These issues, and several others, have led to the popularity of third-party date and time libraries, such as Joda-Time.
3. In order to address these problems and provide better support in the JDK core, a new date and time API, which is free of these problems, has been designed for Java SE 8.
   1. [Classes](https://www.oracle.com/technical-resources/articles/java/jf14-date-time.html) LocalDate, LocalTime, OffsetDateTime and others.
