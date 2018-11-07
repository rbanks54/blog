---
title: 'JSON serialisation/deserialisation with snake_case naming conventions'
date: 2014-12-02T14:38:00.001+11:00
draft: false
tags : [.net, serialisation, json, c#, serialization]
---

#### Couple of notes: 1) You should probably instantiat...
[Marc O. Alfonso](https://www.blogger.com/profile/08022142402400965885 "noreply@blogger.com") - <time datetime="2014-12-26T16:43:58.340+11:00">Dec 5, 2014</time>

Couple of notes:  
1) You should probably instantiate a regex object for reuse  
2) It seems like a variable like MyLLCName would incorrectly be translated to my\_l\_l\_c\_name instead of my\_llc\_name  
3) it seems like a variable like "FirstName99" would incorrect be translated to first\_name\_9\_9 instead of first\_name_99 (for integer separated)  
  
My suggestion is to use:  
Regex converter = new Regex(@"((?<=\[a-z\])(?<b>\[A-Z\])|(?<=\[^_\])(?<b>\[A-Z\]\[a-z\]))");  
protected override string ResolvePropertyName(string propertyName) {  
return converter.Replace(propertyName, "${a}_${b}").ToLower();  
}  
  
and for integer separated  
new Regex(@"((?<=\[a-z\])(?<b>\[A-Z0-9\])|(?<=\[^_\])(?<b>\[A-Z\]\[a-z\]))");
<hr />
#### Correction... return converter.Replace(propertyNam...
[Marc O. Alfonso](https://www.blogger.com/profile/08022142402400965885 "noreply@blogger.com") - <time datetime="2014-12-26T16:49:42.391+11:00">Dec 5, 2014</time>

Correction...  
return converter.Replace(propertyName, "_${b}").ToLower();
<hr />
#### Hi Marc, Thanks for reading and your notes. I...
[Raphael Haddad](https://www.blogger.com/profile/07652960024018187339 "noreply@blogger.com") - <time datetime="2014-12-27T18:26:28.501+11:00">Dec 6, 2014</time>

Hi Marc,  
  
Thanks for reading and your notes.  
  
I've taken a look at naming conventions for acronyms:  
  
http://msdn.microsoft.com/en-us/library/vstudio/ms229043(v=vs.100).aspx  
  
and it seems that an attribute with a naming convention should be lowered except for the first character. Therefor an attribute MyLLCName is correctly translated. However, it should probably be named as MyLlcName anyway.  
  
However, I think you are correct with the integer separated class and I will rectify this. Or better yet. Send through a pull request :)  
  
thanks once again for reading :)
<hr />
#### Excellent article and good examples of the script,...
[Richard Brown](https://www.blogger.com/profile/13930762991630772087 "noreply@blogger.com") - <time datetime="2016-12-07T00:41:50.330+11:00">Dec 3, 2016</time>

Excellent article and good examples of the script, all informative and understandable. It was interesting, thank you for sharing the experience!  
Richard Brown [virtual data room](https://www.idealsvdr.com)
<hr />
#### thank you very much :)
[Raphael Haddad](https://www.blogger.com/profile/07652960024018187339 "noreply@blogger.com") - <time datetime="2017-11-13T09:35:17.371+11:00">Nov 1, 2017</time>

thank you very much :)
<hr />
