# Custom scalars supported by Maana Q

The following is a list of all custom scalars currently supported by the Maana Q platform:

## JSON <a id="CustomscalarssupportedbyMaanaQPlatform-JSON"></a>

JSON scalar type is a valid JSON string \(see Section 9 of [ECMA-404](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)\), that can be parsed into valid JSON object after unescaping.

Example:

* "5" is valid JSON scalar value, as it can be parsed into JSON Number type value `5`
* "test" is not valid JSON scalar value, as it cannot be parsed into valid JSON, but "\"test\"" is valid JSON scalar literal, as it can be parsed into JSON String `"test"`
* "{\"id\":\"io.maana.portal\",\"name\":\"io.maana.portal\",\"description\":\"GraphQL endpoint for all Knowledge Portal functionality, stitching together and relying upon the other services as appropriate.\"}" is a valid value, as it is properly escaped and after unescaping turns into valid JSON object.

JSON Scalar is stored in KindDB as a String

## Date <a id="CustomscalarssupportedbyMaanaQPlatform-Date"></a>

Date scalar is RFC 3339 compatible Calendar Date representation. The only acceptable Date format is YYYY-MM-DD.

Examples:

* 2016-02-09 is valid date
* 2016-2-9 is invalid - both month and day must be represented as 2 digits.
* 2016-02-29 is valid \(2016 is leap day\), whereas 2018-02-29 is not

Date scalar is stored in KindDB as String

## Time <a id="CustomscalarssupportedbyMaanaQPlatform-Time"></a>

Time scalar is RFC 3339 compatible time representation, with mandatory time zone. Definition of acceptable input type format:

`HH:mm:ss[.SSS]Z` where:

* HH - hours, 2 digits
* mm - minutes, 2 digits
* ss - seconds, 2 digits
* .SSS - 1-3 digits for fractions of a second \(up to a millisecond precision\)
* Z - time zone, in one of the following formats
  * 'Z' - Zulu, UTC time
  * \(+/-\)HH:mm - Time difference with UTC zone, for instance Pacific standard time will be encoded as "-08:00"

Time scalar is stored in KindDB as String in normalized Zulu-based format \(i.e. in UTC, with Z as definition of time zone\), with millisecond precision \(3 digits for fraction of a second\)

## DateTime <a id="CustomscalarssupportedbyMaanaQPlatform-DateTime"></a>

DateTime is RFC 3339 compatible date and time representation, with mandatory time zone. It is defined as full Date and full Time formats, as defined above, separated by T.

DateTime is stored in KindDB as String, normalized and Zulu-based, for instance "2014-07-03T10:13:04.1-23:10" will be stored as "2014-07-04T09:23:04.100Z"

{% hint style="info" %}
Note: If using graphene to create a service which contains a kind with graphene.types.json.JSONString\(\), when the service is added and saved in the Admin Panel, an error will be thrown with the last line: 

_**Type definition for ...Input "}\]; Expected type FieldType at value\[n\].schema\[m\].type; did you mean STRING?**_

The schema\[m\] type must be specified as JSON.
{% endhint %}



