Filtering can be performed by constructing a search filter using the following syntax:

&lt;parametername&gt;:&lt;comparer&gt;:&lt;comparevalue&gt;[;&lt;parametername&gt;:&lt;comparer&gt;:&lt;comparevalue&gt;]<br/>

| Comparer | Description | Data types |
|----------|-------------|------|
| eq | equal | string, date, number |
| ne | unequal | string, date, number |
| lt | less than | date, number |
| le | less than or equal to | date, number |
| ge | greater than or equal to | date, number |
| gt | greater than | date, number |
| in | item is one of the values in the list | string, number |
| not | item is NOT one of the values in the list | string, number |
| like | String contains the value. | string |
| startswith | String starts with the value. | string |
| endswith | String ends with the value. | string |
| inbbox | Item is within the bounding box, defined by 4 numbers | bbox |
| inpolygon | Item is within the polygon, defined by list of numbers, where each x and y are a numbers in the array | bbox |
| notinbbox | Item is NOT within the bounding box, defined by 4 numbers | polygon |
| notinpolygon | Item is NOT within the polygon, defined by list of numbers, where each x and y are a numbers in the array | polygon |
| wkt | Item is within the Well-known-text definition | Wkt |
| all | all items in the list must be present in the queried item | string, number |

| Formatting |
| --- |
| String compares are NOT case sensitive and must be surrounded by quotes. |
| Arrays are expressed in JSON format. This means that they are surrounded by square brackets ([ and ]) and the array values are separated by comma's. |
| Parameter names are NOT case sensitive. |
| Number formats are in US notation. This means fractional separators are periods. Comma's (thousands-separators) are ignored. |
| Date field notation is yyyy-MM-dd and must be surrounded by quotes. |
| Bbox type requires an array of 4 numeric values. The uneven-numbers represent an X-ordinate, the even-numbers represent an Y-ordinates. The uneven and the following even number represent a coordinate in WGS84. |
| Polygon type requires an array of numeric values. The number of items in the array need to be even. The uneven-numbers represent an X-ordinate, the even-numbers represent an Y-ordinates. The uneven and the following even number represent a coordinate in WGS84. |

| Examples |
| --- |
| location&colon;eq&colon;"NLKAD";parameter&colon;eq&colon;"Eukariota";organisation&colon;eq&colon;"RWS",measuredvalue&colon;gt&colon;1000;measuredunitSymbol&colon;eq&colon;"n" |
| location&colon;in&colon;["NKLAD","NKLBVA","NLKBRA"];parameter&colon;eq&colon;"Eukariota";organisation&colon;eq&colon;"RWS";measuredvalue&colon;gt&colon;1000,measuredunitSymbol&colon;eq&colon;"n" |
| location&colon;in&colon;["NKLAD","NKLBVA","NLKBRA"];parameter&colon;in&colon;["Eukariota [1]","Plantae"];measuredvalue&colon;gt&colon;1000;measuredunitSymbol&colon;eq&colon;"n" |
| locationArea&colon;inpolygon&colon;[1,2,3,4];parameterCode&colon;in&colon;["Eukariota [1]","Plantae"];measuredvalue&colon;gt&colon;1000; |

Example of a filter in a URL:
/organisations/?filter=organisation:eq:"RWS"

Sorting is the responsibility of the caller. It is the responsibility of the provider to always return results in the same order.

General URL syntax:
available parameters on the root level:

| Field |  Meaning |
| --- |  --- |
| filter | See 'FilterSyntax' |
| page | Returns the specified page of records.  |
| pagesize | The maximum number of records returned for the page. |

### Paging logic
#### Initialisation
The minimum page&gt; is 1.
The provider specifies minimum, maximum and default pagesize&gt;.
If pagesize&gt; is not specified, pagesize&gt; is the provider-specified default page size.
If page&gt; is not specified, page&gt; is assumed to be 1.

#### Paging process
* If &lt;filter&gt; is set,  &lt;filter&gt; is applied to the data set.
* ((&lt;page&gt; - 1) * &lt;pagesize&gt;) records are skipped.
* A maximum of &lt;pagesize&gt; records are returned from the resulting data set.

To find out what filters are recognised by the service, the /filters segment can be used on the endpoints. The filters segment does not recognise any additional parameters.

Also see 'Error handling' and 'Filter Syntax'.
