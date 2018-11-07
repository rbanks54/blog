---
title: 'JSON serialisation/deserialisation with snake_case naming conventions'
date: 2014-12-02T14:38:00.001+11:00
draft: false
tags : [.net, serialisation, json, c#, serialization]
---

[GitHub (NuGet package source)](https://github.com/RaphHaddad/Newtonsoft.Json.Serialization.ContractResolverExtentions)  
[GitHub (Usage example)](https://github.com/RaphHaddad/JsonSerializationExample)  
[Nuget Package](https://www.nuget.org/packages/Json.NET.ContractResolverExtentions/)  
  
JSON is quickly becoming the norm for data transfer along the HTTP protocol and for many of us it is a daily task to serialise into and from JSON.  
  
The problem with JSON, however, is the fact that there is no standard associated with its naming conventions. Let me give you an example.  
  
Below is a snipet of JSON from the Twitter API:  
  

     {     "id": 85011021,      "id_str": "85011021",      "name": "Raph",      "screen_name": "RaphHaddadAus",      "location": "Sydney",      "profile_location": null   }  

  
And here is JSON from the Google + API:  
  

     {      "objectType": "person",      "id": "104264388447663009734",      "displayName": "Raphael Haddad"   }  

  
As you can see there is no consistency between the property names in each of the examples. This issue is quite widespread and some providers have their properties as **snake_case**, others are **camelCase** and others are **PascalCase**  
  
What makes things even more complicated is that there are different standards within some naming conventions as well. Let's take **snake_case** as an example:  
  
Below are two naming conventions that can be written in snake_case:  

*   page_section2
*   page\_section\_2

  
So how do we serialise to and from objects in C# while maintaining statically typed classes with proper C# naming conventions?  
  

### Some Solutions

*   change the C# property conventions from **PascalCase** to **snake_case**
*   add an attribute for EACH property

*   example: \[DataMember(Name = "user_id")\]

### A Good Solution

Firstly, I will be using the Json.NET serialisation library to demonstrate how to serialise and deserialise Objects to and from JSON.  
  
In this library. You can specify how you wish to convert property names by creating  JsonSetting object. You also specify how a specific Class's properties should be serialised by setting the ContractResolver property.  
  

           var jsonSettings = new JsonSerializerSettings         {           ContractResolver = new DefaultContractResolver(),           NullValueHandling = NullValueHandling.Ignore         };         var json = JsonConvert.SerializeObject(data, jsonSettings);  

  
Json.NET already comes with a class DefaultContractResolver and CamelCasePropertyNamesContractResolver the former serializes an object strictly on the property naming conventions. While the later changes everything to **camelCase**.   
  
What I have done is created two classes that inherit from the DefaultContractResolverand override the method ResolvePropertyName   
  
  
  

       public class SnakeCasePropertyNamesContractResolver : DefaultContractResolver     {       protected override string ResolvePropertyName(string propertyName)       {         var startUnderscores = System.Text.RegularExpressions.Regex.Match(propertyName, @"^_+");         return startUnderscores + System.Text.RegularExpressions.Regex           .Replace(propertyName, @"([A-Z])", "_$1").ToLower().TrimStart('_');       }     }     public class SnakeCaseIntegerSeperatedPropertyNamesContractResolver : DefaultContractResolver     {       protected override string ResolvePropertyName(string propertyName)       {         var startUnderscores = System.Text.RegularExpressions.Regex.Match(propertyName, @"^_+");         return startUnderscores + System.Text.RegularExpressions.Regex           .Replace(propertyName, @"([A-Z0-9])", "_$1").ToLower().TrimStart('_');       }     }  

  
The class SnakeCasePropertyNamesContractResolver serializes properties into the format **snake_case1**  
  
And SnakeCaseIntegerSeperatedPropertyNamesContractResolver serializes properties into the format **snake\_case\_1 **  
  
You can use these two classes by:  

1.   creating a JsonSerializerSettings object. 
2.  Assigning the property of this object ContractResolver to a new instance of either SnakeCasePropertyNamesContractResolver or SnakeCaseIntegerSeperatedPropertyNamesContractResolver. 
3.  Then serialising and deserialising the object using JsonConvert.SerializeObject() or JsonConvert.DeserializeObject() 

These classes simply work by using Regex to pattern match any occurrence of capital letters (or numbers), pre-fix them with an '_' and then make everything lower case.  
  
Example:  
  
  
  

           var data = new MyClass         {           FName = "Raphael",           First1Name = "Raph",           FirstName = "Raph",           FirstName1 = "Raph",           FirstName_ = "Raph",           _FName = "Raph",           _FirstName = "Raph"         };         var jsonSettings = new JsonSerializerSettings         {           ContractResolver = new SnakeCasePropertyNamesContractResolver(),           NullValueHandling = NullValueHandling.Ignore         };         var json = JsonConvert.SerializeObject(data, jsonSettings);//serialize object to snake_case1         var obj = JsonConvert.DeserializeObject<MyClass>(json, jsonSettings);//desserialize object from snake_case1         jsonSettings.ContractResolver = new SnakeCaseIntegerSeperatedPropertyNamesContractResolver();         json = JsonConvert.SerializeObject(data, jsonSettings);//serialize object to snake_case_2         obj = JsonConvert.DeserializeObject<MyClass>(json,jsonSettings); //deserialize object from snake_case_2  

  
MyClass here is:  
  
  

       public class MyClass     {       public string FirstName       {         get;         set;       }       public string FirstName1       {         get;         set;       }       public string First1Name       {         get;         set;       }       public string FName       {         get;         set;       }       public string _FirstName       {         get;         set;       }       public string FirstName_       {         get;         set;       }       public string _FName       {         get;         set;       }     }  

### The Result

A NuGet Package that contains these two classes, that can be added to your project. They can be used to deserialise a JSON object into a POCO class. Or they can be used to serialise a POCO into JSON.  
  
Here is the link: https://www.nuget.org/packages/Json.NET.ContractResolverExtentions/  
  

### Thanks!

Thank you all for reading and a special thanks has to go to [@Meligy](https://twitter.com/meligy) for helping me write this post :)