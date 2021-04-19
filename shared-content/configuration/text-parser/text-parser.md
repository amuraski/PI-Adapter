---
uid: TextParser
---

# Text parser

The adapter you are using includes the text parser component which ensures consistent parsing of text from different files. For more information on which file types are supported for your adapter, see the topics in this chapter.

Designed to be a document parser, the text parser parses a semantically complete document in its entirety.
The text parser produces OMF compatible output, which in turn is compatible with the OCS backing SDS (Sequential Data Store) that stores data in streams consisting of multiple values and indexes.

## Data types supported by the text parser

The following data types are supported by the text parser: 

* DateTime
* DateTimeOffset
* TimeSpan
* sbyte
* byte
* short
* ushort
* int
* uint
* long
* ulong
* float
* double
* decimal
* bool
* char
* string

**Note:** Not all data types supported by the text parser are also supported by OMF.

## Culture support

Some numeric values and datetimes support cultures when they are being parsed. The default culture is `en-US (US English)` (InvariantCulture). OSIsoft recommends that you leave the adapter at the default unless you expect culturally variant input.

**Note:** Installed cultures vary by machine with both Linux and Windows. If the specified culture is not installed, the text parser fails to parse input that requires that culture.

## Time zone support

A time zone or offset specified by a time is always used to convert to UTC time. Time zones are only used if there is no offset or time zone specifier in a text date and time string.

For time zones that support time changes between daylight and standard times, a text file may temporarily contain invalid or ambiguous datetimes during the time change, which are possible only for a two-hour period each year. When these time changes occur, the text parser logs them, but the datetime is parsed and passed to the callback. Ambiguous times are reported as standard times, which is the Microsoft recommendation.

## Date and time processing

The text parser can use time zones, cultures, and custom formats to read dates and times from ingress data.

You can specify custom dates and times when you configure data selection. Set the custom date and time using the `TimeFormat` property. If you are using a culture other than default `en-US`, use the name of day or month specific to the culture. For example, use "Juni" instead of "June" for the `de-DE` culture.

The following custom date and time syntaxes are supported.

```text
"MM/dd/yyyy H:mm:ss zzz"         "06/15/2018 15:15:30 -05:00"
"MM/dd/yyyy H:mm:ss.fff zzz"     "06/15/2018 15:15:30.123 -05:00"
"dd/MM/yyyy H:mm:ss.fff K"       "15/06/2018 15:15:30.123 Z"
"MMMM/dd/yyyy H:mm:ss.fff K"     "June/15/2018 15:15:30.123 Z" (InvariantCulture/English)
"MMMM/dd/yyyy H:mm:ss.fff K"     "Juni/15/2018 15:15:30.123 Z" (German)
"MMM/dd/yyyy H:mm:ss.fff K"      "Jun/15/2018 15:15:30.123 Z" 
"MMM-dd-yyyy H:mm:ss.fff K"      "Jun-15-2018 15:15:30.123 Z"
"MMM-dd-yyyy H:mm:ss.fff K"      "Jun-15-2018 15:15:30.123 Z"
"MMM-dd-yyyy H:mm:ss.fff K"      "Jun-15-2018 15:15:30.123 Z"
"yyyy-MM-dd H:mm:ss.fff K"       "2018-06-15 15:15:30.123 Z"
"yyyy-M-d H:mm:ss.fff K"         "2018-6-5 15:15:30.123 Z"
"yyyy-M-d H:mm:ss.fff zzz"       "2018-6-5 15:15:30.123 +05:00"
"ddd dd MMM yyyy h:mm tt zzz"    "Sun 15 Jun 2008 8:30 AM -06:00"
"dddd dd MMM yyyy h:mm tt zzz"   "Sunday 15 Jun 2008 8:30 AM -06:00"
"dddd dd MMM yyyy h:mm tt zzz"   "Sunday 15 Jun 2008 8:30 AM -06:00"
"dddd dd MMMM yyyy h:mm tt zzz"  "Sunday 15 June 2008 8:30 AM -06:00" 
```
