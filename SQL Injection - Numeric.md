
This challenge involves a SQLi that does not like it when characters are requested directly, only utilising the `char()` feature we can convert ASCII values into strings without sending strings

Depending on the Database backend will determine if the strings are taken as a function instead of just strings.

This is good for WAF evasion and filter bypass