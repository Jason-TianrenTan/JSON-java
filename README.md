# SWE262P JSON-Java
## Milestone 2
You may find the added code on line 749 for XML.java and line 68 for XMLTest.java
## Milestone 3
###Updates
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
