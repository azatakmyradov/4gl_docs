[Index](index.html)  [Home](getting-started_home.html)

Locales

|  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- |
| [Administration Page](workbench-reference_launching-url.html#native) | Application/Contract | Syracuse/Collaboration | Class | *localePreferences* | Representation | *localePreference* |

**A locale is a set of data associated with a local code assigned by default to a user, but it can be changed using the upper panel. The locale code defines the formats used to display or input localized information such as dates or amounts.**

For every locale that is defined, the following information must be entered:

## Local code

This code identifies the locale. It is recommended to use the normalized code as defined by the standard ISO 639-2 (for example, en-GB is "British English").

## Description

Describes the locale.

## Enabled

If this check box is selected, it allows the user to select this locale.

## Formats for dates and time

Several formats can be entered as a string that integrates separators and formatting patterns. The patterns used are the following:

* d or dd represents the day in a month
* dddd represents the name of the day
* MM represents the month number
* MMM represents the abbreviated English name of the month
* MMMM represents the name of the month
* yy and yyyy represent the year number (on 2 or 4 digits)
* HH, mm, ss represent the hours, minutes, and seconds

## First day of the week

The first day of the week is used to display the calendar.

## Two digit date's max year

When the year is entered in two digits, it defines which year the switch is done between centuries. For example, if this parameter is equal to 2029, entering a date with 29 will convert it as 2019, while entering a date with 30 will convert it as 1930.

## Number decimal separator

Used to separate the decimal places from an integer part of a number. Can be either comma or period.

## Number group separator

Used to separate groups of digits in large numbers.

## Number group size

Defines how many digits are present in a group when large numbers are displayed. For example, if this value is 3, if the number group separator is a comma, and the decimal separator is a period, a number such as pi\*10^15 (rounded to 2 decimals) would be presented as : `3,141,592,653,589,793.23`.

  

[Index](index.html)  [Home](getting-started_home.html)