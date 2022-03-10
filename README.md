# SWE262P JSON-Java
## Milestone 2
You may find the added code on line 749 for XML.java and line 68 for XMLTest.java
## Milestone 3
### Updates
Added function
```java
toJSONObject(Reader reader, Function<String, String> keyTransformer)
```
to XML.java at line 887 and two JUnit test functions
```java
shouldReplaceXML()
```
and
```java
shouldReverseTags()
```
correspondingly at line 91 and line 106, each performs a different 
string operation on each of the tags found during parsing the raw XML string.
### Code Analysis
In my implementation, I look for existing open and closing tags in the XML
string. Whenever a tag is found, the tag string is pushed into
a tag stack, and the temporary JSONObject inside is also saved in a
JSONObject stack. Whenever the corresponding closing tag is found, we first check
if the tags are legally closed. If so, we can pop the tag name and then perform the
specified string manipulation. We then save the transformed tag name and the JSONObject
it points to into the father JSONObject. 
</br>
Through this recursive process, all tags we discover will be transformed. The overall process is a one-pass, meaning we don't
need to look back and worry about previous tags. 
</br>
Comparing to first parsing into object then manually replace each tag with a new tag name,
the overall time complexity is the same, but in our case we still reduce the time from
traversing the whole XML two times to only one time. This may be a significant improvement
when handling large XML files.

## Milestone 4
### Updates
Added function `public Stream<JSONObject> toStream()` to JSONObject.java (line 103) and JSONArray.java (line 93).</br>
Added unit test `_testPlainXMLObj()` and `_testStreamArray()`, to run the tests please run `public void testStream()` on line 93 of JSONObjectTest.java.

### About
I decided to set all return values of `toStream()` to `JSONObject`, in respect of the original `JSONObject` format. The core idea is to traverse through the `JSONObject` using DFS, and ignore generic values such as Integers or Strings, and only extract `JSONObjects`. If a `JSONObject` is confronted, we recursively extract nested objects inside that. On the other hand, for `JSONArray` we traverse the array by index and recursively extract the `JSONObject` inside.

## Milestone 5
### Updates
Added two functions `public static void toJSONObject(Reader reader, Consumer<JSONObject> callback, Consumer<Exception> exceptionHandler)`(line 941) and 
`public static Future<JSONObject> toJSONObjectFuture(Reader reader)`(line 957) in `XML.java`. Added two corresponding unit tests `shouldHandleAsyncFunctions()`(line 133)
and `shouldHandleAsyncFunctionsWithFuture()`(line 143) in `XMLTest.java`.

### About
For this milestone I used the built-in `toJSONObject(Reader reader)` provided by the original author.
I wrote two async functions on reading a JSON string. The first one takes two lambda functions as inputs
and performs callback functionalities after the `JSONObject` is parsed, while the second simply returns
a `Future<JSONObject>`.
