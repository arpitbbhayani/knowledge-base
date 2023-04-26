Most databases provide three types of temporal data types to store dates and times: `DATE`, `DATETIME`, and `TIMESTAMP`. While all three data types store date and time information, there are significant differences among them, which we will explore in this article.

The exploration of these types is MySQL-specific, but other databases closely follow the semantics. Do refer to the documentation of the database you are using to get an accurate picture.

## Range of values

The `DATE` data type stores only the date information, excluding the time information, and it can store dates ranging from `1000-01-01` to `9999-12-31`.

The `DATETIME` data type stores both date and time information, and it can store dates ranging from `1000-01-01 00:00:00` to `9999-12-31 23:59:59`. On the other hand, the `TIMESTAMP` data type also stores date and time information, but it is limited to a range from `1970-01-01 00:00:01 UTC` to `2038-01-19 03:14:07 UTC`, holding the number of seconds/microseconds elapsed since UNIX Epoch.

## Storage Requirements

DATETIME takes up 5 bytes to store date and time, but depending on how precise you want seconds to be, it stores it in additional 3 bytes to hold up seconds precise up to 6 decimal places.

- 0 precision requires 0 bytes
- 1,2 digit second precision requires 1 byte
- 3,4 digit second precision requires 2 bytes
- 5,6 digit second precision requires 3 bytes

In contrast, the `TIMESTAMP` data type supports fractional seconds up to six decimal places, with a fixed size of 4 bytes plus the fractional seconds represented in up to 3 bytes as described above.

## Which one should you use?

### `DATETIME`

The DATETIME data type is useful when you need to store an application-specific static timestamp, such as appointment schedules or event schedules.

Most databases have in-built functions to operate on `DATETIME` data, so if your usecase requires datetime operations, like `ADD`, `SUB`, `DIFF`, etc., then prefer going for `DATETIME`.

### `TIMESTAMP`

The `TIMESTAMP` data type is ideal for recording timestamps related to events that happen on your system, such as transaction times, which require efficient storage but no specific timezone specific operation.

`TIMESTAMP` is 1 byte lighter than datetime, making it faster to process. In addition, `TIMESTAMP` also have an extra advantage when it comes to time zone handling, as MySQL, or any database, automatically converts timestamps to the UTC timezone and converts them back to the client's time zone on retrieval, whereas `DATETIME` data type does not support automatic timezone conversion unless specified.

## Conclusion

In conclusion, while both the `DATETIME` and `TIMESTAMP` data types store date and time information, they differ in their range, precision, storage requirements, and use cases.

It's essential to consider these differences when choosing which data type to use in your MySQL database to ensure the accuracy and efficiency of your temporal data storage.
